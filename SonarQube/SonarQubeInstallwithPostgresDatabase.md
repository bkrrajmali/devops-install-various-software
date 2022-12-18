1. Install OpenJDK 11

  SSH to your Ubuntu server as a non-root user with sudo access.
  Install OpenJDK 11 and create user as postgres
  
  ```bash
 sudo useradd postgres
 ``` 
  ```bash
  sudo apt-get install openjdk-11-jdk -y
  ```
2. Install and Configure PostgreSQL

    Add the PostgreSQL repository.
```bash
    sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
```
  
3. Add the PostgreSQL signing key.

```bash
    wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -
```

4. Install PostgreSQL.

```bash
sudo apt install postgresql postgresql-contrib -y
```
5. Enable the database server to start automatically on reboot.
```bash
    $ sudo systemctl enable postgresql
```
6. Start the database server.
```bash
   sudo systemctl start postgresql
```
7 Change the default PostgreSQL password.

    sudo passwd postgres
8 Switch to the postgres user.

    su - postgres
9 Create a user named sonar.

    createuser sonar

10 Log in to PostgreSQL.

    psql
11 Set a password for the sonar user. Use a strong password in place of my_strong_password.

    ALTER USER sonar WITH ENCRYPTED password 'sonar';

12 Create a sonarqube database and set the owner to sonar.

   ```bash
    CREATE DATABASE sonarqube OWNER sonar;
```
  Grant all the privileges on the qube database to the sonar user.

    GRANT ALL PRIVILEGES ON DATABASE sonarqube to sonar;

13 Exit PostgreSQL.

    \q

14 Return to your non-root sudo user account.

    $ exit

15. Download and Install SonarQube

    Install the zip utility, which is needed to unzip the SonarQube files.
```
    sudo apt-get install zip -y
```
 16 Locate the latest download URL from the SonarQube official download page.

    Download the SonarQube distribution files.

    sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.7.1.62043.zip

  17 Unzip the downloaded file.

    sudo unzip sonarqube-<VERSION_NUMBER>.zip

  18 Move the unzipped files to /opt/sonarqube directory

    sudo mv sonarqube-<VERSION_NUMBER> /opt/sonarqube

19. Add SonarQube Group and User

20 Create a dedicated user and group for SonarQube, which can not run as the root user.

    Create a sonar group.

    sudo groupadd sonar

    Create a sonar user and set /opt/sonarqube as the home directory.

    sudo useradd -d /opt/sonarqube -g sonar sonar

    Grant the sonar user access to the /opt/sonarqube directory.

    sudo chown sonar:sonar /opt/sonarqube -R

21. Configure SonarQube

    Edit the SonarQube configuration file.
```bash
    sudo nano /opt/sonarqube/conf/sonar.properties

    Find the following lines:

    #sonar.jdbc.username=

    #sonar.jdbc.password=

    Uncomment the lines, and add the database user and password you created in Step 2.

    sonar.jdbc.username=sonar

    sonar.jdbc.password=sonar
```

Below those two lines, add the sonar.jdbc.url.

    sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube

 Save and exit the file.
 
 Start the SonarQube service.
```
  sudo systemctl start sonar

  Check the service status.

  sudo systemctl status sonar
 ```  
  22. Modify Kernel System Limits

    sudo nano /etc/sysctl.conf

    Add the following lines.

    vm.max_map_count=262144

    fs.file-max=65536

    ulimit -n 65536

    ulimit -u 4096

    Save and exit the file.

    Reboot the system to apply the changes.

    $ sudo reboot
```
23. Access SonarQube Web Interface

Access SonarQube in a web browser at your server's IP address on port 9000. For example:

http://192.0.2.123:9000

