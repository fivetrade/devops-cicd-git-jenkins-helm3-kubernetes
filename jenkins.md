# Jenkins server Installation for CI CD 
### Java
1. Install Java
```sh
sudo apt install openjdk-8-jdk openjdk-8-jre 
```

2. Verify Java Installation
```sh 
java --version 
```

3. Setup JAVA_HOME 
  a. Find the java path
```sh
find /usr/lib/jvm/java-1.8.*
sudo vim /etc/profile.d/environment.sh
```
  b. create an environment.sh file and set the export JAVA_HOME
```sh
sudo vim /etc/profile.d/environment.sh
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64
```
  c. Make the script executable
```sh
sudo chmod +x /etc/profile.d/environment.sh
```  
  d. Load environment variables
```sh
source /etc/profile.d/environment.sh
```
