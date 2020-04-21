# Installing Docker on Amazon EC2 Instance

1. Access the EC2 as a root user
   ```sh
   sudo su -
   ```
1. Install docker and start docker services
   ```sh 
   yum install docker -y
   docker --version 
   
   # start docker services
   service docker start
   service docker status
   ```
1. Create a user called dockeradmin
   ```sh
   useradd dockeradmin
   passwd dockeradmin
   ```
1. add a user to docker group to manage docker 
   ```
   cat /etc/group
   usermod -aG docker dockeradmin
   
   # confirm
   id dockeradmin
   ```
### Test
1. Create a tomcat docker container by pulling a docker image from the public docker registry
   ```sh
   docker pull tomcat:latest
   
   #then run in detach mode (-d)
   docker run -d --name tomcat-container -p 8080:8080 tomcat:latest
   ```
 1. Incase you have an error, then configure the container
     ```sh
   docker exec -it tomcat-container /bin/bash
   
   #navigate to webapps.dist folder
   cd /webapp.dist
   
   #copy contents into the webapps folder
   cp -R * ../webapps
   ``
