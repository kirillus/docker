# Install docker latest version for Centos


## Delete old docker engine.

```
sudo yum remove docker \
  docker-client \
  docker-client-latest \
  docker-common \
  docker-latest \
  docker-latest-logrotate \
  docker-logrotate \
  docker-engine
```


## Install repo & docker

```
sudo yum install -y yum-utils
sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

sudo yum install docker-ce docker-ce-cli containerd.io
sudo yum install docker-ce-20.10.6 docker-ce-cli-20.10.6 containerd.io
sudo systemctl start docker
sudo docker -v
```

*Docker version 20.10.6, build 370c289*


## Troubleshoots
*Docker upgrade restart container error Unknown runtime specified docker-run*
The Docker version is 1.13.1. After upgrading its version to 18.06.1, I encountered this error when starting the container created by the old version:
```
grep -rl 'docker-runc' /var/lib/docker/containers/ | xargs sed -i 's/docker-runc/runc/g'
systemctl restart docker
```
```
