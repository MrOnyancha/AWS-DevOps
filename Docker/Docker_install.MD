# Install Docker on AWS EC2 | Add Dockeradmin | Configure Jenkins-Docker Job

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
   
   # navigate to webapps.dist folder
    cd /webapp.dist
   
   # copy contents into the webapps folder
    cp -R * ../webapps
   ```
   
   ### Deploy on Container: Jenkins Job
1. Add this to the Post-build Action: Exec command
   ```sh
   cd /home/dockeradmin;
   docker build -t jenkins-job-image .;
   docker run -d --name jenkins-job-container -p 8080:8080 jenkins-job-image;
   ```
  NB: The rest of the configurations remain the same as of Deploy-on-Docker Job
  We just added commands to enable automatic: Var file upload >> Build the image >> Run the container out of the image.
  
    
