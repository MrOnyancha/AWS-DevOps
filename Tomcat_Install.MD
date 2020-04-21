# Tomcat installation on the Second EC2 instance

### Pre-requisites
1. EC2 instance with Java v1.8.x 
ie Download Java-8 & add to PATH

### Install Apache Tomcat (use 8.5.x) 
1. Download tomcat packages from  https://tomcat.apache.org/download-80.cgi onto /opt on EC2 instance
   ```sh 
   # Create tomcat directory
   cd /opt
   wget http://mirror.ucu.ac.ug/apache/tomcat/tomcat-8/v8.5.54/bin/apache-tomcat-8.5.54.tar.gz
   tar -xvzf /opt/apache-tomcat-8.5.35.tar.gz
   ```
1. navigate into ./bin, startup.sh to start server
   ```sh
   cd /opt/apache-tomcat-8.5.35/bin/startup.sh 
   ./startup.sh
   ```
  #### View the Server :
access tomcat application from browser on port 8080  
 - http://<Public_IP>:8080

### NB:
Using unique ports for each application is a best practice in an environment. 
But tomcat and Jenkins runs on ports number 8080. Hence we had to set up another EC2 instance,, however you can change tomcat port number to 8090 in conf/server.xml file under tomcat home, incase you to set up on the same EC2 instance.


1. now application is accessible on port 8080. but tomcat application doesnt allow to login from browser. changing a default parameter in context.xml does address this issue
   ```sh
   #search for context.xml
   find / -name context.xml
   ```
1. above command gives 3 context.xml files. comment (<!-- & -->) `Value ClassName` field on files which are under webapp directory. 

After that restart tomcat services to effect these changes
   ```sh 
   tomcatdown
   tomcatup
   ```
1. Update users information in the tomcat-users.xml file
goto tomcat home directory then config folder
   ```sh
    cd conf/tomcat-user.xml
   ```
  ### Add below users to conf/tomcat-user.xml file
   ```sh
	<role rolename="manager-gui"/>
	<role rolename="manager-script"/>
	<role rolename="manager-jmx"/>
	<role rolename="manager-status"/>
	<user username="admin" password="admin" roles="manager-gui, manager-script, manager-jmx, manager-status"/>
	<user username="deployer" password="deployer" roles="manager-script"/>
	<user username="tomcat" password="tomcat" roles="manager-gui"/>
   ```
1. Restart serivce and try to login to tomcat application from the browser. This time it should be Successful
