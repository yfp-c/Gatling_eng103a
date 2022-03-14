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