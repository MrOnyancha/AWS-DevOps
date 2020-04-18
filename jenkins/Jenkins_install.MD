# Install Jenkins on AWS EC2
Jenkins is a leading open source automation server, Jenkins provides hundreds of plugins to support building, deploying and automating any project


### Prerequisites
1. EC2 Instance 
   - With Internet Access
   - Create a Security Group with Port `8080` open for internet
1. Java v1.8.x 

## Install Java & add to PATH
First access the bash as a root user
   ```sh
   sudo su - 
   ```
1. We use open java from http://openjdk.java.net/install/
   ```sh
   yum install java-1.8*
   #yum -y install java-1.8.0-openjdk-devel
   ```

1. Confirm Java Version and set the java to PATH
   ```sh
   java -version
   # Output installation location
   find /usr/lib/jvm/java-1.8* | head -n 3
   # Paste in the .bash_profile file
   nano .bash_profile
   JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.212.b04-1.el8_0.x86_64
   export JAVA_HOME
   PATH=$PATH:$JAVA_HOME
   ```

## Install Jenkins
1. Get the latest version from https://pkg.jenkins.io/redhat-stable/ and install
   ```sh
   yum -y install wget
   sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
   sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
   #Then
   yum install jenkins
   ```

   ### Start Jenkins
   Upon installation, Jenkins is not running, so we need to start the service
   ```sh
   # Start jenkins service
   service jenkins start

   # Setup Jenkins to start at boot,
   chkconfig jenkins on
   ```

   ### View the service
   By default jenkins runs at port `8080`, You can access jenkins at
   ```sh
   http://<YOUR-SERVER-PUBLIC-IP>:8080
   ```
  #### Configure Jenkins
- The default Username is `admin`
- Grab the default password 
  #Paste the path below to see the password
- Password Location:`/var/lib/jenkins/secrets/initialAdminPassword`
- At times you need to run this 
  `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`
- `Skip` Plugin Installation; _We can do it later_
- Change admin password
   - `Admin` > `Configure` > `Password`
- Configure `java` path
  - `Manage Jenkins` > `Global Tool Configuration` > `JDK`  
- Create another admin user id

### Test Jenkins Jobs
1. Create “new item”
1. Enter an item name – `My-First-Project`
   - Chose `Freestyle` project
1. Under the Build section
	Execute shell: echo "Welcome to Jenkins Demo"
1. Save your job 
1. Build job
1. Check "console output"
