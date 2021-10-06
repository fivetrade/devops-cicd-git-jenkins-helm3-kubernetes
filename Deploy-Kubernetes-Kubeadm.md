# Deploy Kubernetes Cluster with Kubeadm  
This documentation guides you in setting up a kubernetes cluster on __Ubuntu 20.04 LTS__ with one master node and two workers nodes.

## Requirements
| Role | IP | OS | Ram  | CPU |
| --- | --- | --- | --- | --- |
| Master | 192.168.1. | Ubuntu 20.04 | 4G | 2 |
| worker1 | 192.168.1. | Ubuntu 20.04 | 2G | 2 |
| worker2 | 192.168.1. | Ubuntu 20.04 | 2G | 2 |

## Step1 - On master and workers
### Login as root user 
```
sudo su -
```
### Disable Firewall 
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
#### Install docker engine
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
