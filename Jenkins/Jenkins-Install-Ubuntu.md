# Install Jenkins on Ubuntu 22.04 LTS

Step-1-First, open a terminal window and update the system package repository by running:

  ```bash 
    sudo apt update  
   ```
Step-2- To install OpenJDK 8, run:
  ```bash 
  sudo apt install openjdk-8-jdk -y
  ```
Step-3- First, add the repository key to the system:
```bash
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
```
Step-4- Next, let’s append the Debian package repository address to the server’s sources.list:
```bash
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
```
Step-5- After both commands have been entered, we’ll run update so that apt will use the new repository.
```bash
sudo apt update
```
Step-6- Finally, we’ll install Jenkins and its dependencies.
```bash
sudo apt install jenkins
```

Step-7- sudo systemctl start jenkins 
```bash
sudo systemctl status jenkins -y
```
Step-8- Open the port if its blocked
```bash
sudo ufw allow 8080
sudo ufw enable
```
Step-9- Check the status 
```bash
sudo ufw status
```
