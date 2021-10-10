# Installation et configurationde Helm3 in jankins server
## Helm2 vs Helm3
#### Tiller is Removed
The most apparent change is the removal of Tiller. The server-side component, Tiller, is now removed.
Why was tiller removed then?
Previously, Helm 2  takes the maximum permission to make changes in Kubernetes. This can cause security issues in the cluster if Helm has not been properly deployed.
##### Tiller is Removed Helm v2 vs v3 commands
example 
| Command | Helm2 | Helm3 |
| --- | --- | --- |
| Download a chart to your local directory	| fetch	| pull |
| Given a release name, delete the release from Kubernetes | delete| uninstall |

## Add Jenkins user into sudoers file to get sudo access
#### Login as root user
```
sudo su -
```
#### Add Jenkins user into sudoers file to get sudo access
```
vi /etc/sudoers
```
#### Add Jenkins user into sudoers file to get sudo access
```
jenkins ALL=(ALL) NOPASSWD: ALL
```
#### Login as jenkins user account
```
su - jenkins
```
## Install Helm 3 on Linux | macOS
#### Download Helm 3 installation script.
```
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
```
Give the script execute permissions.
```
chmod 700 get_helm.sh
```
#### Run the installer.
```
./get_helm.sh
```
####  Install a specific version
```
./get_helm.sh  -v v3.7.0
```
#### Confirm installation of Helm 3
```
helm version
```


