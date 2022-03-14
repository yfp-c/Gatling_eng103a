# Gatling_eng103a
------------------------
## Installing Gatling on Ubuntu (specifically on AWS EC2)

### Step 1: Package updates
```
sudo apt update
sudo apt -y upgrade && sudo systemctl reboot
# server will reboot, give it some time
```
### Step 2: Install java
- Check Java -version
```
java -version
```
- Install open jdk
```
sudo apt-get install openjdk-8-jdk
```
- Verify version of JDK
```
java -version
```
### Step 3: Install Gatling
The command:
```
sudo apt-get install -y gatling
```
### Step 4: Setting JAVA_HOME Env Variable
Set JAVA_HOME
```
export JAVA_HOME=jdk-install-dir
export PATH=$JAVA_HOME/bin:$PATH
```
To check env variable
```
printenv JAVA_HOME
```
### Step 5: Copy the [gatling folder](https://gatling.io/open-source/) from localhost to EC2 AWS
e.g.
```
scp -i "key_name" -r "local_host_path" ec2-user@<ec2 ip>:/home/ubuntu
```
### Step 6: Execute basic load test
Open up the new folder, and browse to the bin directory. From here, run:
```
./gatling.sh
```
Gatling will load, choose a simulation you'd like to run. Gatling will go ahead and run the script that you choose. 
![image](https://user-images.githubusercontent.com/98178943/158238201-51ff225a-c11d-4db5-aa5b-9d3ef93abfd3.png)
![image](https://user-images.githubusercontent.com/98178943/158238317-def01f53-6da2-4ed1-91cc-e9acd004dbdc.png)
