# Configure Git pulgin on Jenkins
Git is one of the most popular tools for version control system. you can pull code from git repositories using jenkins if you use github plugin. 

The plugin is added on the Jenkins server installed on EC2  

#### Install Git
1. First access the bash as a root user
   ```sh
   sudo su -
   ```
2. Install git packages on jenkin server
   ```sh
   yum install git -y
   ```

#### Setup Git on jenkins console
- Install git plugin without restart  
  - `Manage Jenkins` > `Jenkins Plugins` > `available` > `github`

- Configure git path
  - `Manage Jenkins` > `Global Tool Configuration` > `git`
