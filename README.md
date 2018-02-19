# My docker stack

Install notes: git clone to /srv/docker/

## Prepping the Alpine Docker host

First we install the server from vanilla ISO. 

```Bash
setup-alpine
us
us-intl
dhcp
eth0
```

### setup ssh keys

Enable ssh login using password, copy keys, disable password login again. 

```Bash
vi /etc/ssh/sshd_config
/etc/init.d/sshd restart
ssh-copy-id root@127.0.0.1
```

### add repo

Uncomment `http://dl-4.alpinelinux.org/alpine/edge/community`

```Bash
vi /etc/apk/repositories
```

### prep docker for Prometheus

```Bash
vi /etc/docker/daemon.json
```

#### /etc/docker/daemon.json:

```json
{
  "metrics-addr" : "0.0.0.0:9323",
  "experimental" : true
}
```

### Install dependencies

```Bash
apk update
apk add docker py-pip vim git
rm -rf /etc/timezone
echo "Europe/Amsterdam" >> /etc/timezone
```

### install docker & docker compose

```Bash
rc-update add docker boot
service docker start
pip install docker-compose
```

### Clone repo

```Bash
git clone git@github.com:javydekoning/my-docker-stack.git /srv/docker
mkdir /srv/docker/downloads && chmod -R a+rw /srv/docker/downloads/
chmod -R a+rw /srv/docker/prometheus/
cd /srv/docker
```