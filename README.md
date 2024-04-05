# Jenkins, Nexus, and SonarQube Installation Script

## Introduction

This script automates the installation of Jenkins, Nexus, and SonarQube on a single EC2 instance. It is designed to save costs on AWS by consolidating multiple tools onto one server for practicing building CI/CD pipelines with Jenkins.

## System Requirements

-   **Instance Type:** T2 or T3 Large (T3 Large Recommended)
-   **Storage:** 30GB root volume
-   **Operating System:** Ubuntu

![Screenshot 2024-04-03 at 15 49 42](https://github.com/Chriscloudaz/nexus-sonar-jenkins-install/assets/142612223/b9027ea7-cb05-4f93-b0a7-c3c08cedc852)


## Tools Installed
-   Jenkins
-   Docker
-   Nexus (Docker container)
-   SonarQube (Docker container)

## Usage

1.  Clone this repository to your local machine:
    
    ```git clone https://github.com/gitgo23/Jenkins-Nexus-Sonarqube-install.git``` 
    
2.  Navigate to the directory containing the script:
    
    `cd your-repo` 
    
3.  Execute the script:
    
    `sudo bash install_tools.sh` 
    
4.  After installation, ensure that the default ports for the tools are allowed under the inbound rules of your EC2 instance:
    
    -   **Jenkins:** Port 8080
    -   **Nexus:** Port 8081
    -   **SonarQube:** Port 9000
    -   **SSH:** Port 22 

![Screenshot 2024-04-03 at 15 45 12](https://github.com/Chriscloudaz/nexus-sonar-jenkins-install/assets/142612223/99467a8a-90c8-4b2d-8b9a-53802b1912e2)


## Important Note

Containers will stop whenever the instance is stopped. You can use the `start_containers.sh` script provided in this repository to start both containers again when you start your instance.

To access the shell of your container, please run the command `docker exec -it "name of container" bash`

You can get the name of your container by running `docker ps` 

### If you run into permission issues, do the following:
- Run the command `sudo usermod -aG docker ${USER}` 
- Run `sudo su ubuntu` 
- Try again 

However to avoid manually executing your start_containers.sh anytime you start your EC2 instance, follow these steps
- Run `sudo mv start_containers.sh /bin`
- Run `sudo vi /etc/systemd/system/start-containers.service`
- Copy and paste the content of the start-containers.service script
- Save and quit
- Run `sudo systemctl daemon-reload`
- Run `sudo systemctl enable start-containers.service`
- Run `sudo systemctl start start-containers.service`

## Access URLs

After the installation is complete, you can access the following URLs to use the newly installed tools:

-   **Jenkins:** http://your-ec2-instance-ip:8080
-   **Nexus:** http://your-ec2-instance-ip:8081
-   **SonarQube:** http://your-ec2-instance-ip:9000

Please feel free to reach out on www.gyenoch@gmail.com

## License

This project is licensed under the MIT License - see the [LICENSE.md](https://chat.openai.com/c/LICENSE.md) file for details.
