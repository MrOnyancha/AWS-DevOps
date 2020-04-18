#  Install Maven build tool in the EC2 sever & configure in Jenkins tool 
Maven is a code build tool which used to convert your code to an artifact. this is a widely used plugin to build in continuous integration

- Ensure you have a Jenkins server installed in the EC2 
- access the bash as a root user 
```sh
sudo su -
```

#### Install Maven & Add to PATH
1. Download maven packages https://maven.apache.org/download.cgi onto Jenkins server. 
cd /opt/maven as the installation directory
 - Link : https://maven.apache.org/download.cgi
    ```sh
     # Creating maven directory under /opt
     mkdir /opt/maven
     cd /opt/maven
     # downloading maven version 3.6.0
     wget http://mirrors.estointernet.in/apache/maven/maven-3/3.6.1/binaries/apache-maven-3.6.1-bin.tar.gz
     # unzip
     tar -xvzf apache-maven-3.6.1-bin.tar.gz
     ```
	
2. Setup M2_HOME and M2 paths in .bash_profile also add these to the path variable
We arledy have Java added in the same file
   ```sh
   vi ~/.bash_profile
   M2_HOME=/opt/maven/apache-maven-3.6.1
   M2=$M2_HOME/bin
   PATH=<Existing_PATH>:$M2_HOME:$M2
   ```
#### Check: 
3. logoff and login as root user to check maven version
  
    ```sh
    mvn --version
    ```
So far we have completed the installation of maven software to support maven plugin on the jenkins console. Let's jump onto Jenkins to complete the remaining steps. 

### Setup maven on Jenkins console
4. Install maven plugin without restart  
  - `Manage Jenkins` > `Jenkins Plugins` > `available` > `Maven Invoker`
  - `Manage Jenkins` > `Jenkins Plugins` > `available` > `Maven Integration`

5. Configure maven path
  - `Manage Jenkins` > `Global Tool Configuration` > `Maven`
