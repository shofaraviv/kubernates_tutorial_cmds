# kubernates_tutorial_cmds

```
https://www.youtube.com/watch?v=a_sQuL2mOAY
https://www.youtube.com/watch?v=4ht22ReBjno
```
## UBUNTU
```
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
```
## DOCKER
```
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
```

## DOCKER-COMPOSE
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.22.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod -x /usr/local/bin/docker-compose 
docker-compose up -d
```
## KUBERNATES

```sudo su
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
cat <<EOF >/etc/apt/sources.list.d/kubernetes.list
deb https://apt.kubernetes.io/ kubernetes-xenial main
EOF
apt-get update
sudo apt-get install -y kubernetes-cni=0.6.0-00
sudo apt-get install -y kubelet=1.11.3-00
sudo apt-get install -y kubeadm=1.11.3-00
sudo apt-get install -y kubectl=1.11.3-00
apt-mark hold kubelet kubeadm kubectl
exit
```
```
sudo swapoff -a
sudo kubeadm reset
sudo kubeadm init --pod-network-cidr=10.244.0.0/16
 ```
 ```
 Your Kubernetes master has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

You can now join any number of machines by running the following on each node
as root:

  kubeadm join 192.154.1.156:6443 --token 94ymzj.rgke5qwaru3in6t4 --discovery-token-ca-cert-hash sha256:c6f5a13b51ed7b08e2323df2309c302b5222a9cae4dc0cc5a90ccc29b4e9ccaa
 ```
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
kubectl cluster-info
```

<details><summary>CLICK ME</summary>
<p>

#### We can hide anything, even code!

```ruby
   puts "Hello World"
   Kubernetes control plane is running at https://192.154.1.156:6443
   KubeDNS is running at https://192.154.1.156:6443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy
   To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```

</p>
</details>

