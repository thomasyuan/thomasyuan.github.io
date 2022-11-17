---
title: "Certbot on Oracle Cloud VM"
excerpt_separator: "<!--more-->"
toc: true
categories:
  - Blog
tags:
  - certbot
  - certificate
---


Try to get a certificate from Let's encrypt on Oracle's compute instance (vm) with command `certbot certonly --standalone` but keeps getting error: 
```
Certbot failed to authenticate some domains (authenticator: standalone). The Certificate Authority reported these problems:
  Domain: xxxxxxxx
  Type:   connection
  Detail: xxx.xxx.xxx.xxx: Fetching http://xxxxxxxxx/.well-known/acme-challenge/mi-unJr-CSHn8IIlKjrEvaySgitsK9-kgK42pjI8nHo: Error getting validation data

Hint: The Certificate Authority failed to download the challenge files from the temporary standalone webserver started by Certbot on port 80. Ensure that the listed domains point to this machine and that it can accept inbound connections from the internet.
```

Checking the logs, seems something wrong with binding 80 on ipv4
```
2022-11-16 22:04:01,102:DEBUG:acme.standalone:Successfully bound to :80 using IPv6
2022-11-16 22:04:01,102:DEBUG:acme.standalone:Certbot wasn't able to bind to :80 using IPv4, this is often expected due to the dual stack nature of IPv6 socket implementations.
```

But IPv6 works fine.
Tried to disable IPv6 (assume certbot will then switch to IPv4 only) and run the certbot again, same error. (Didn't check ip addresses though).
```
sudo sysctl -w net.ipv6.conf.all.disable_ipv6=1
sudo sysctl -w net.ipv6.conf.default.disable_ipv6=1
sudo sysctl -w net.ipv6.conf.lo.disable_ipv6=1
```

Since 80 can be bind to IPv6, next try will be using IPv6 on my VM.
This video helps https://www.youtube.com/watch?v=yxm3Bn7uHyw
Basicly, you need to 

1. Create IPv6 subnet

   Networking -> Virtual Cloud Networks -> <Your VCN> -> CIDR Blocks/Prefixes -> Add CIDR Blocks/Prefixes -> IPv6 Prefixes
 
2. Enable IPv6 subnet on your Virtual Clould Networks.
  
    Networking -> Virtual Cloud Networks -> <Your VCN> -> Subnets, `Edit` your subnet, and `Enable IPv6`

3. Add IPv6 route
 
    Networking -> Virtual Cloud Networks -> <Your VCN> -> Route Tables -> <Your route table> -> Add Route Rules, select IPv6, type is `Internet Gateway`, dest is `::/0` means all IPv6 ip adresses.

4. Add IPv6 Ingress/Engress

    Allow all IPv6 Engress, and maybe only enable service you allowed for Ingress. In my case, for certbot, I need TCP port 80. I also enabled IPv6 ICMP so I can ping it from outside.
  
5. Assign IPv6 address to your vm
  
    Compute -> Instances -> <your vm instance> -> Attached VNICs -> IPv6 Addresses -> Assign IPv6 Address, you should see your IPv6 address.

6. Verify 
  
    Login to your VM, check `ens3` interface, see if you get the IPv6 Address you see on the management UI. If not, then run `sudo dhclient -6 ens3`, you should get the IPv6 address. Now you can try to ping `google.com`.
  
    On my VM, the output is something like this:
    ```
    PING google.com(yyz12s08-in-x0e.1e100.net (2607:f8b0:400b:803::200e)) 56 data bytes
    64 bytes from yyz12s08-in-x0e.1e100.net (2607:f8b0:400b:803::200e): icmp_seq=1 ttl=122 time=1.56 ms
    64 bytes from yyz12s08-in-x0e.1e100.net (2607:f8b0:400b:803::200e): icmp_seq=2 ttl=122 time=1.62 ms
    64 bytes from yyz12s08-in-x0e.1e100.net (2607:f8b0:400b:803::200e): icmp_seq=3 ttl=122 time=1.57 ms

    ```
 
That's all to enable IPv6 on your Oracle VM.
  
Next we should set DNS for the IPv6 address. Go to your DNS provider management UI, add one `AAAA` record.
> DNS AAAA records match a domain name to an IPv6 address. DNS AAAA records are exactly like DNS A records, except that they store a domain's IPv6 address instead of its IPv4 address.

Now run certbot again, finally it works!!!

