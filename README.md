# kubernates_tutorial_cmds

## UBUNTU
´´´
< ubuntu-18.04.3-live-server-amd64.iso >
:~$ uname -a
Linux vm-ubuntu 4.15.0-202-generic #213-Ubuntu SMP Thu Jan 5 19:19:12 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux

:~$ lsb
lsb_release  lsblk        
vm-ubuntu@vm-ubuntu:~$ lsb_release -a
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 18.04.3 LTS
Release:	18.04
Codename:	bionic
´´´
DOCKER
´´´
sudo apt-get update  
sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo apt-key fingerprint 0EBFCD88
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable"
sudo apt-get update
sudo apt-get install -y docker-ce=17.03.2~ce-0~ubuntu-xenial

sudo groupadd docker
sudo usermod -aG docker ${USER}
newgrp docker
´´´

## DOCKER-COMPOSE
´´´´
sudo curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod -x /usr/local/bin/docker-compose 
docker-compose up -d
´´´
