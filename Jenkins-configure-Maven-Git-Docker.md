# Install and configure Maven, Git and Docker in jenkins 
### Installing Apache Maven on Ubuntu 20.04 with apt
1. Download & install maven : https://maven.apache.org/download.cgi
```sh
mkdir /home/jenkins/tools
cd /home/jenkins/tools
wget https://dlcdn.apache.org/maven/maven-3/3.8.3/binaries/apache-maven-3.8.3-bin.tar.gz
tar -xvzf apache-maven-3.8.3-bin.tar.gz
mv apache-maven-3.8.3 mvn
sudo vim /etc/profile.d/environment.sh
```
2. Export environment variables
```sh
export M2_HOME=/home/jenkins/tools/mvn
export MAVEN_HOME=/home/jenkins/tools/mvn
export PATH=${M2_HOME}/bin:${PATH}
```
3. Make the script executable
```sh
sudo chmod +x /etc/profile.d/environment.sh
source /etc/profile.d/environment.sh
```
4. Check maven version
```sh
mvn -version
```
### Install Git
```sh
apt install git 
```
### Install docker: https://docs.docker.com/engine/install/ubuntu/
1. Uninstall old versions
```sh
sudo apt-get remove docker docker-engine docker.io containerd runc
```
2. Set up the repository
```sh
sudo apt-get update
sudo apt-get install \
    apt-transport-https \
ca-certificates \
curl \
gnupg \
lsb-release
```
2.	Add Docker’s official GPG key
```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo \
  "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
3.	Enable docker in boot
```sh
systemctl enable docker
```
4.	Enable docker in boot
```sh
systemctl enable docker
```
5. Chedk docker version
```sh
docker --version
```
6. Install Docker Engine
```sh
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```
7. Verify that Docker Engine is installed correctly by running the hello-world image.
```sh
sudo docker run hello-world
```
8. Give permissions to jenkins user in jenkins server to access docker
```sh
sudo groupadd docker
sudo usermod -aG docker jenkins
sudo chmod 777 /var/run/docker.sock
```













