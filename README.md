# kubernates_tutorial_cmds

```
https://www.youtube.com/watch?v=a_sQuL2mOAY
https://www.youtube.com/watch?v=4ht22ReBjno
```
```
sudo dpkg -i docker-ce_17.03.2~ce-0~ubuntu-xenial_amd64.deb
/usr/local/bin/docker-compose

/usr/bin/kubectl
/usr/bin/kubeadm
/usr/bin/kubelet
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
rm -rf $HOME/.kube/config
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

```
kubectl get node
```
```
NAME        STATUS     ROLES    AGE   VERSION
vm-ubuntu   NotReady   master   1h    v1.11.3
```

```
watch kubectl

```

```
watch kubectl get all --all-namespaces
```

```
Every 2.0s: kubectl get all --all-namespaces                                                                                                                                                              vm-ubuntu: Fri Feb  3 17:53:47 2023

NAMESPACE     NAME                                    READY   STATUS    RESTARTS   AGE
kube-system   pod/coredns-78fcdf6894-7g8n7            0/1     Pending   0          1h
kube-system   pod/coredns-78fcdf6894-fw8jh            0/1     Pending   0          1h
kube-system   pod/etcd-vm-ubuntu                      1/1     Running   0          1h
kube-system   pod/kube-apiserver-vm-ubuntu            1/1     Running   0          1h
kube-system   pod/kube-controller-manager-vm-ubuntu   1/1     Running   0          1h
kube-system   pod/kube-proxy-sjlms                    1/1     Running   0          1h
kube-system   pod/kube-scheduler-vm-ubuntu            1/1     Running   0          1h

NAMESPACE     NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)         AGE
default       service/kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP         1h
kube-system   service/kube-dns     ClusterIP   10.96.0.10   <none>        53/UDP,53/TCP   1h

NAMESPACE     NAME                        DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR                   AGE
kube-system   daemonset.apps/kube-proxy   1         1         1       1            1           beta.kubernetes.io/arch=amd64   1h

NAMESPACE     NAME                      DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
kube-system   deployment.apps/coredns   2         2         2            0           1h

NAMESPACE     NAME                                 DESIRED   CURRENT   READY   AGE
kube-system   replicaset.apps/coredns-78fcdf6894   2         2         0       1h

```
```
kubectl get nodes
kubectl get pods
```
### FLANNEL
```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/v0.10.0/Documentation/kube-flannel.yml
```
```
kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/bc79dd1505b0c8681ece4de4c0d86c5cd2643275/Documentation/kube-flannel.yml
```
```
:~$ kubectl get nodes
NAME        STATUS   ROLES    AGE   VERSION
vm-ubuntu   Ready    master   2h    v1.11.3
```
```
master como master e worker
kubectl taint nodes --all node-role.kubernetes.io/master-
```
```
kubectl run kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1 --port=8080
kubectl get deploy
kubectl get  pod/kubernetes-bootcamp
```
```
$ kubectl get pods
NAME                  READY   STATUS    RESTARTS   AGE
kubernetes-bootcamp   1/1     Running   0          5m
```
```
kubectl logs kubernetes-bootcamp -f
```
```
kubectl proxy
```
```
curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/proxy/
```
```
curl http://localhost:8001/api/v1/namespaces/default/pods/kubernetes-bootcamp/proxy/
```
```
Hello Kubernetes bootcamp! | Running on: kubernetes-bootcamp | v=1
```

```
kubectl get pod/kubernetes-bootcamp -o yaml
```
```
kubectl edit pod/kubernetes-bootcamp -o yaml
```

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v1.10.1/src/deploy/recommended/kubernetes-dashboard.yaml
```
#### expose porta
```
kubectl expose deployment kubernetes-dashboard --name=kubernetes-dashboard-nodeport --port=443 --target-port=8443 --type=NodePort -n kube-system
```
#### sevice account
```
kubectl describe sa kubernetes-dashboard -n kube-system
```
```
kubectl get secret <TOKEN-ID> -n kube-system -o yaml
```
```
kubectl get secret kubernetes-dashboard-token-f8pcf -n kube-system
kubectl get secret kubernetes-dashboard-token-f8pcf -n kube-system -o yaml
```
```
echo `echo <TOKEN> | base64 --decode`
```
```
vm-ubuntu@vm-ubuntu:~$ echo `echo  ZXlKaGJHY2lPaUpTVXpJMU5pSXNJbXRwWkNJNklpSjkuZXlKcGMzTWlPaUpyZFdKbGNtNWxkR1Z6TDNObGNuWnBZMlZoWTJOdmRXNTBJaXdpYTNWaVpYSnVaWFJsY3k1cGJ5OXpaWEoyYVdObFlXTmpiM1Z1ZEM5dVlXMWxjM0JoWTJVaU9pSnJkV0psTFhONWMzUmxiU0lzSW10MVltVnlibVYwWlhNdWFXOHZjMlZ5ZG1salpXRmpZMjkxYm5RdmMyVmpjbVYwTG01aGJXVWlPaUpyZFdKbGNtNWxkR1Z6TFdSaGMyaGliMkZ5WkMxMGIydGxiaTFtT0hCalppSXNJbXQxWW1WeWJtVjBaWE11YVc4dmMyVnlkbWxqWldGalkyOTFiblF2YzJWeWRtbGpaUzFoWTJOdmRXNTBMbTVoYldVaU9pSnJkV0psY201bGRHVnpMV1JoYzJoaWIyRnlaQ0lzSW10MVltVnlibVYwWlhNdWFXOHZjMlZ5ZG1salpXRmpZMjkxYm5RdmMyVnlkbWxqWlMxaFkyTnZkVzUwTG5WcFpDSTZJbVEzWWpBNU5XWTRMV0ZpT1dNdE1URmxaQzFpTm1RMExUQXdNR015T1RjMk1UWXlOaUlzSW5OMVlpSTZJbk41YzNSbGJUcHpaWEoyYVdObFlXTmpiM1Z1ZERwcmRXSmxMWE41YzNSbGJUcHJkV0psY201bGRHVnpMV1JoYzJoaWIyRnlaQ0o5LldlV0FnVENEYTdlNGpCZ0ZBeFA2NmkyaTBCdUlFMUUxRVEwVmR1dVhtYzQyREJ1OHdjUGlEVEFWdFdjSjg4M1JSN0o1TTZZNHZ0b3J0aW5Lb2hKRy13Tm40QVJDNUd3NUw4ZDFTaGdKZDRoTS1MQ002cEZwMTVweEl4Z3BzSmJvWndhdllvYUVvSGpxMVNwM0ZyRzB6Rjd3d2JmVHM4UmxjbmJuX1JjMk44dldiSW1nM0hGdUM5OFNRQWJmcnZITGVMb2t1WnNTZHNyeEFUeUFLSnI1SnFwbmhkbHNsbHIyd0Rrb1BRaUhsTERsN01hVmY3UUFGOERDV0tyQmJzdmVtS2VrdWl6VmxNYUVoVXo3UmE2SUtVenBHZ045cW5JdnBMZmJ3YmJhYTM5a01DUGFVZU11TkM5OU41ODlZTHhnSi1YdEJwT0dGS3JBLWxCVXZRTXBVUQ== | base64 --decode`
```
```
eyJhbGciOiJSUzI1NiIsImtpZCI6IiJ9.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlLXN5c3RlbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJrdWJlcm5ldGVzLWRhc2hib2FyZC10b2tlbi1mOHBjZiIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50Lm5hbWUiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50LnVpZCI6ImQ3YjA5NWY4LWFiOWMtMTFlZC1iNmQ0LTAwMGMyOTc2MTYyNiIsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDprdWJlLXN5c3RlbTprdWJlcm5ldGVzLWRhc2hib2FyZCJ9.WeWAgTCDa7e4jBgFAxP66i2i0BuIE1E1EQ0VduuXmc42DBu8wcPiDTAVtWcJ883RR7J5M6Y4vtortinKohJG-wNn4ARC5Gw5L8d1ShgJd4hM-LCM6pFp15pxIxgpsJboZwavYoaEoHjq1Sp3FrG0zF7wwbfTs8Rlcnbn_Rc2N8vWbImg3HFuC98SQAbfrvHLeLokuZsSdsrxATyAKJr5Jqpnhdlsllr2wDkoPQiHlLDl7MaVf7QAF8DCWKrBbsvemKekuizVlMaEhUz7Ra6IKUzpGgN9qnIvpLfbwbbaa39kMCPaUeMuNC99N589YLxgJ-XtBpOGFKrA-lBUvQMpUQ
```
