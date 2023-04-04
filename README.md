# JavaWebApp

Fully automated CI/CD pipeline using Jenkins, AWS EC2, Docker. This project automaically built, tested, deloyed to AWS EC2 instance every time you push the code to repository.

# Environment Setup
* Jenkins:
  * First install java jdk 11 or above
     * apt install openjdk-17-jdk -y
  * next install Jenkins
    * follow this link https://www.jenkins.io/doc/book/installing/linux/
* If you are going for Master slave architecture then install java-17/maven/git/docker in slave/worker node or else install in same Jenkins node.
* For this project java-17 and mvn 3.9 are required
* Maven:
  * apt-get install -y maven
* Git:
	* apt-get install -y git
* Docker: 
    * curl -fsSL get.docker.com -o get-docker.sh | sh
    * add the user you will use to create/run docker
      * sudo usermod -aG <group> <user-name>

# Configure Jenkins
  * Credentails:
    * EC2 instance:
      * Create SSH key for a new user or existing user in EC2 instance where you are going to deploy and use that private key to create credentials in Jenkins
      	  * ssh-keygen -t rsa // click enter
    * DockerHub:
      * Got dockerhub -> setting and create a key. Use this key to create credentials in Jenkins.
      * Create a repository as well to upload the images created.
    * GitHub:
      * if you are using private repo then you need to add credentials in Jenkins.
      * create SSH key in github using this key add credentials in Jenkins.
      
