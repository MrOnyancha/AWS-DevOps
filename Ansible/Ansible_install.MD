# Ansible Installation

Ansible is an open-source automation platform. It is very, very simple to set up and yet powerful. Ansible can help you with configuration management, application deployment, task automation.

### Pre-requisites

1. An AWS EC2 instance (on Control node)

### Installation steps:
#### on Amazon EC2 instance

1. Install python and python-pip
   ```sh
   yum install python
   yum install python-pip
   ```
   #At times, Python is already installed in the EC2 instance
   
1. Install ansible using pip, then check for version
    ```sh
    pip install ansible
   ansible --version
   ```
   
1. Create a user called ansibleadmin (on Control node and Managed host)  
   ```sh
   useradd ansibleadmin
   passwd *********
   ```
1. Below command grant sudo access to ansadmin user. But we strongly recommended using "visudo" command if you are aware vi or nano editor.  (on Control node and Managed host)
   ```sh
   echo "ansibleadmin ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
   ```
   or Add this: ansibleadmin ALL=(ALL) NOPASSWD: ALL , to last file line.
   ```sh
   visudo
   ```
   
1. Log in as a ansibleadmin user on master and generate ssh key (on Control node)
   ```sh 
   sudo su - ansibleadmin
   ssh-keygen
   ```
1. Move into .ssh folder, copy keys onto all ansible managed hosts (on Control node)
   ```sh 
   ls -la
   cd .ssh
   ssh-copy-id ansadmin@<target-server>
   ```

1. Ansible server used to create images and store on docker registry. Hence install docker, start docker services and add ansadmin to the docker group. 
   ```sh
   yum install docker
   
   # start docker services 
   service docker status
   service docker start 
   
   # add user to docker group 
   usermod -aG docker ansadmin

   ```
1. Create a directory /etc/ansible and create an inventory file called "hosts" add control node and managed hosts IP addresses to it. 
 
### Validation test

   
1. Run ansible command as ansadmin user it should be successful (Master)
   ```sh 
   ansible all -m ping
   ```
