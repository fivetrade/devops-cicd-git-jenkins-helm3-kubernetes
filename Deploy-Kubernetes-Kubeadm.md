# Deploy Kubernetes Cluster with Kubeadm  
This documentation guides you in setting up a kubernetes cluster on __Ubuntu 20.04 LTS__ with one master node and two workers nodes.

## Requirements
| Role | IP | OS | Ram  | CPU |
| --- | --- | --- | --- | --- |
| Master | 192.168.1. | Ubuntu 20.04 | 4G | 2 |
| worker1 | 192.168.1. | Ubuntu 20.04 | 2G | 2 |
| worker2 | 192.168.1. | Ubuntu 20.04 | 2G | 2 |

## Step1 - On master and workers
### Login as root user (on master and workers)
```
sudo su -
```
### Disable Firewall (on master and workers)
```
ufw disable
```
#### Disable swap (on master and workers)
```
swapoff -a; sed -i '/swap/d' /etc/fstab
```
