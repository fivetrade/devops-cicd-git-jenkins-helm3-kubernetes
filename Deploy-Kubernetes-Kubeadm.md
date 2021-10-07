# Deploy Kubernetes Cluster with Kubeadm  
This documentation guides you in setting up a kubernetes cluster on __Ubuntu 20.04 LTS__ with one master node and two workers nodes.
##  What is Kubeadm ?
Kubeadm is a tool built to provide best-practice "fast paths" for creating Kubernetes clusters. It performs the actions necessary to get a minimum viable, secure cluster up and running in a user friendly way. Kubeadm's scope is limited to the local node filesystem and the Kubernetes API, and it is intended to be a composable building block of higher level tools.
## Requirements
| Role |Ram  | CPU |
| --- | --- | --- |
| Master | 4G | 2 |
| worker1 | 2G | 2 |
| worker2 | 2G | 2 |

## Step1 - On master and workers
#### Login as root user 
```
sudo su -
```
#### Disable Firewall 
```
ufw disable
```
#### Disable swap 
```
swapoff -a; sed -i '/swap/d' /etc/fstab
```
#### Update sysctl settings for Kubernetes networking
```
cat >>/etc/sysctl.d/kubernetes.conf<<EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
sysctl --system
```
####Install docker engine
```
  apt install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
  add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
  apt update
  apt install -y docker-ce=5:19.03.10~3-0~ubuntu-focal containerd.io
```
### Kubernetes Setup
#### Add Apt repository
```
  curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
  echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" > /etc/apt/sources.list.d/kubernetes.list
```
#### Install Kubernetes components
```
apt update && apt install -y kubeadm=1.18.5-00 kubelet=1.18.5-00 kubectl=1.18.5-00
```
## Step2 - On master only
##### Initialize Kubernetes Cluster
Update the command with the ip address of master
```
kubeadm init --apiserver-advertise-address=192.168.1.120 --pod-network-cidr=192.168.0.0/16  --ignore-preflight-errors=all
```
Please update the ip apiser with your owner ip
##### Deploy Calico network
```
kubectl --kubeconfig=/etc/kubernetes/admin.conf create -f https://docs.projectcalico.org/v3.14/manifests/calico.yaml
```

##### Cluster join command (don't forget to save output)
```
kubeadm token create --print-join-command
```
##### To be able to run kubectl commands as non-root user
If you want to be able to run kubectl commands as non-root user, then as a non-root user perform these
```
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
## Step3 - On Kworkers (worker01 & worker02)
##### Join the cluster
Use the output from __kubeadm token create__  command (saved output) in previous step from the master server and run here.

## Step4 - Verifying the cluster (On master)
##### Get Nodes status
```
kubectl get nodes
```
##### Get component status
```
kubectl get cs
```
Winner :)
