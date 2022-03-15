# Gatling_eng103a
[Installing Gatling on Ubuntu (specifically on AWS EC2)](#installing-gatling-on-ubuntu--specifically-on-aws-ec2-)

[Installing Gatling on Windows](#installing-gatling-on-windows)

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

## Installing Gatling on Windows
-------------------
### Install JDK
Go to the [oracle website](https://www.oracle.com/java/technologies/downloads/) and download and install JDK 8. You may need to create an account to download the file.
![image](https://user-images.githubusercontent.com/98178943/158434045-73140c61-44bd-46f6-82a8-557b1189c2e5.png)

### Set Java as env variable

Search 'env' in the windows search bar and click 'edit the system environment variables`
![image](https://user-images.githubusercontent.com/98178943/158434929-e5a02e86-71fb-42b6-9c50-4bf8f4285331.png)

 Under the 'Advanced' tab, choose the “Environment Variables…” button.
 ![sdfsdf](https://cdn2.hubspot.net/hubfs/208250/Blog_Images/gatwin11.png)

 If we want the environment variable for java to be used only by the current windows user, go to the User Variables for <user> section. If we want the environment variable for java to be used by all windows users, go to the System variables section. In this example we will choose the System variables and click on the  “New...” button, as shown below:
 ![asdfsf](https://cdn2.hubspot.net/hubfs/208250/Blog_Images/gatwin12.png)

 Type in “Variable name” and “Variable value” with the variable name as the name of the environment variable for java and the variable value as the path directory of jdk8.
```
Variable name: JAVA_HOME
Variable value: C:\Program Files\Java\jdk1.8.0_171
```
![asdasd](https://cdn2.hubspot.net/hubfs/208250/Blog_Images/gatwin13.png)

Then we have:
![sa\fa](https://cdn2.hubspot.net/hubfs/208250/Blog_Images/gatwin14.png)

Click on the “Path” variable as shown below.

![asfas](https://cdn2.hubspot.net/hubfs/208250/Blog_Images/gatwin15.png)

 Add a new line and type in %JAVA_HOME%\bin.
![adasd](https://cdn2.hubspot.net/hubfs/208250/Blog_Images/gatwin16.png) 

To verify java is installed, go to your command prompt and type in `java`.

### Install Gatling

Go to the [Gatling website](http://gatling.io/#/download) and download open source.

Unzip into a folder or directory of your choice.

### Installing IntelliJ
Very simple, just download [Intellij](https://www.jetbrains.com/idea/download/#section=windows) and install it to edit java and scala files.

## Testing Gatling on Windows

[Follow this guide](https://www.blazemeter.com/blog/how-to-run-a-simple-load-test-with-gatling) to run a simple gatling test and to see how it works. 

Follow up to `Load Testing with Different Scenarios` as we will need to adjust the script using Java and not scala. 

We can edit the java scripts by entering the user-files > simulations > <your-simulation>. 

Open in Intellij and add code such as below:

```java
    setUp(
              scn.injectOpen(
                      atOnceUsers(10), // 2
                      rampUsers(10).during(5), // 3
                      constantUsersPerSec(20).during(15), // 4
                      constantUsersPerSec(20).during(15).randomized(), // 5
                      rampUsersPerSec(10).to(20).during(10), // 6
                      rampUsersPerSec(10).to(20).during(10).randomized() // 7
              ).protocols(httpProtocol)
```

The third line above can lead to more interesting simulation data such as the image below, to add users over a period of defined seconds:

![image](https://user-images.githubusercontent.com/98178943/158441161-50ea1440-ad5a-44e2-8a2e-5fa849cc7130.png)

### Testing your app/website

Open your webpage on [Google Chrome](https://www.google.com/intl/en_uk/chrome/) and go to `more tools > developer tools` on the top right. 

Go to the `Network` tab and click `preserve log`. Record the actions on the page that you want to do. Once done, finish recording and download as HAR file. 

![image](https://user-images.githubusercontent.com/98178943/158441902-a8af30a4-a8ae-4e72-bc1a-0a1231e99857.png)

Run recorder.bat from your gatling `bin` folder. Enter your generated HAR file and click start to create a scala/java file that we can run gatling with.

![image](https://user-images.githubusercontent.com/98178943/158443140-df5871d4-5e11-4a6b-9ad9-92b38d32602f.png)

Navigate to the gatling bin folder and run your tests, adjusting the java code if necessary.