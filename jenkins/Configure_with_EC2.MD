## Plugins added
1. Maven Integration
1. Maven Invoker
1. GitHub 
1. Oracle Java SE Development Kit Installer Plugin
1. Deploy to container
1. Publish Over SSH

## Jobs configurations
1. Deploy-on-Tomcat-Server
    <br>
  a. Git Repo
    ```sh
   https://github.com/TrevorNathan/hello-world.git
    ```
  b. BUILD: Goals and options
  <br>
    ```sh
    clean install package
    ```
    <br><br>
  c. Post-build Actions: Deploy war/ear to a container
  <br>
    ```sh
    WAR FILE: **/*.war
    Credentials: deployer
    ```
