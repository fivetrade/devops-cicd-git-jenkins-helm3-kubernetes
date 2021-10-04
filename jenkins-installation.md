# Jenkins server Installation for CI CD 
### Java Installation
1. Install Java
```sh
sudo apt update
sudo apt install openjdk-8-jdk
```

2. Verify Java Installation
```sh 
java -version 
```

3. Setup JAVA_HOME 
Find the java path
```sh
find /usr/lib/jvm/java-1.8.*
sudo vim /etc/profile.d/environment.sh
```
Create an environment.sh file and set the export JAVA_HOME
```sh
sudo vim /etc/profile.d/environment.sh
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64
```
Make the script executable
```sh
sudo chmod +x /etc/profile.d/environment.sh
```  
Load environment variables
```sh
source /etc/profile.d/environment.sh
echo $JAVA_HOME
```
### Jenkins Installation : https://www.jenkins.io/doc/book/installing/linux/#debianubuntu
1. Long Term Support release
```sh
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \
    /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
sudo apt-get install jenkins
```
2. Start Jenkins
Jenkins status
```sh
systemctl status jenkins
```
Start Jenkins service
```sh
systemctl start jenkins
```
Setup jenkins to start at boot
```sh
systemctl enable jenkins
```
