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

> https://www.unixmen.com/45713-2/ > https://www.serverlab.ca/tutorials/linux/administration-linux/how-to-set-the-proxy-for-apt-for-ubuntu-18-04/

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

### Gradle

Add your proxy settings to ~/.gradle/gradle.properties

```
systemProp.http.proxyHost=www.somehost.org
systemProp.http.proxyPort=8080
systemProp.http.proxyUser=userid
systemProp.http.proxyPassword=password
systemProp.http.nonProxyHosts=*.nonproxyrepos.com|localhost
```

> https://docs.gradle.org/current/userguide/build_environment.html#sec:accessing_the_web_via_a_proxy

### VS Code Remote

If your remote host is behind a proxy, you may need to set the HTTP_PROXY or HTTPS_PROXY environment variable on the SSH host. Open your ~/.bashrc file add the following (replacing proxy.fqdn.or.ip:3128 with the appropriate hostname / IP and port):

```
export HTTP_PROXY=http://proxy.fqdn.or.ip:3128
export HTTPS_PROXY=$HTTP_PROXY

# Or if an authenticated proxy
export HTTP_PROXY=http://username:password@proxy.fqdn.or.ip:3128
export HTTPS_PROXY=$HTTP_PROXY
```

**In my case, when enabled java extension, I need gradle proxy setup as well.**

> Check "Set HTTP_PROXY / HTTPS_PROXY on the remote host" in [here](https://www.serverlab.ca/tutorials/containers/docker/how-to-set-the-proxy-for-docker-on-ubuntu/)
