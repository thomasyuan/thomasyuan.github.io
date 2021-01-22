---
title: "Work Behind Proxy"
excerpt_separator: "<!--more-->"
toc: true
categories:
  - Blog
tags:
  - Proxy
  - Network
---


## Work Behind Proxy

Many easy tasks can't be easily done if you work behind proxy.

### Snap 
```
sudo snap set system proxy.http=http://<username>:<password>@<proxy_address>:<proxy_port>
sudo snap set system proxy.https=https://<username>:<password>@<proxy_address>:<proxy_port>
```

### Pip
> Reference https://leifengblog.net/blog/how-to-use-pip-behind-a-proxy/
```
sudo pip install --proxy=https://<username>:<password>@<proxy_address>:<proxy_port> somepackage
```

### Git
```
git config --global http.proxy http://<username>:<password>@<proxy_address>:<proxy_port>
git config --global https.proxy https://<username>:<password>@<proxy_address>:<proxy_port>
```

### Apt
> https://www.unixmen.com/45713-2/
> https://www.serverlab.ca/tutorials/linux/administration-linux/how-to-set-the-proxy-for-apt-for-ubuntu-18-04/

### Docker
```
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo vi /etc/systemd/system/docker.service.d/proxy.conf
```
Add the following contents, changing the values to match your environment.
```
[Service]
Environment="HTTP_PROXY=http://<username>:<password>@<proxy_address>:<proxy_port>/"
Environment="HTTPS_PROXY=https://<username>:<password>@<proxy_address>:<proxy_port>/"
Environment="NO_PROXY="localhost,127.0.0.1,::1"
```
```
## Reload the daemon configuration.
sudo systemctl daemon-reload
## Restart Docker to apply our changes.
sudo systemctl restart docker.service
## run docker without sudo
sudo usermod -aG docker ${USER}
su - ${USER}
```

> https://www.serverlab.ca/tutorials/containers/docker/how-to-set-the-proxy-for-docker-on-ubuntu/
