1. Install OpenJDK 11

  SSH to your Ubuntu server as a non-root user with sudo access.
  Install OpenJDK 11 and create groups for both sonar and postgres users as below:
  
  ```bash
 sudo groupadd sonar
 sudo groupadd postgres
 ``` 
  ```bash
sudo apt-get install openjdk-11-jdk -y
  ```
2. Create both sonar and postgres users as below:

```bash
sudo useradd -m -s /bin/bash sonar -g sonar
sudo useradd -m -s /bin/bash postgres -g postgres

```
3. Create Passwords for both sonar and postgres as below:

```bash
sudo passwd sonar
sudo passwd postgres
```
4. visudo from root any sudo user and add both users to sudoers as below. Add sonar user and postgres user below root:
```bash
# User privilege specification
root    ALL=(ALL:ALL) ALL
sonar   ALL=(ALL:ALL) ALL
postgres ALL=(ALL:ALL) ALL
```
5. Change permissions on /opt as below using root user or any user whose have sudo access
```bash
 sudo chmod 777 /opt
```
6. Login to sonar using as below and provide password
```bash
   su - sonar 
   cd /opt
```
7 Now download sonarqube software using below in /opt directory

    sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.7.1.62043.zip
    
8 unzip the sonarqube zip file using below and rename the directory

    unzip sonarqube-9.7.1.62043.zip
    mv sonarqube-9.7.1.62043 sonarqube

9 Now add the paraeters the /etc/sysctl.conf params using below

    sudo nano /etc/sysctl.conf
    add below
    
    vm.max_map_count=262144
    fs.file-max=65536
    ulimit -n 65536
    ulimit -u 4096

reboot the server using sudo reboot

10 Once done with rebooting login into sonar user using su - sonar

12 Now start the sonar using below

sh /opt/sonarqube/bin/linux-x86-64/sonar.sh start

 As this is running on Hd database which is for evaluation purpose we need to configure postgres database for sonarqube

Embedded database should be used for evaluation purposes only

The embedded database will not scale, it will not support upgrading to newer versions of SonarQube, and there is no support for migrating your data out of it into a different database engine.

 Stop the sonarqube using below
  ```
  sh /opt/sonarqube/bin/linux-x86-64/sonar.sh stop
```
13  Install and Configure PostgreSQL
    Add the PostgreSQL repository.

    sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'
    
14 Add the PostgreSQL signing key

    wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -

15 Install PostgreSQL.

    sudo apt install postgresql postgresql-contrib -y

16 Start the Postgres database as below

    sudo systemctl start postgresql

17 Enable the database server to start automatically on reboot.

    sudo systemctl enable postgresql
    
19. Now login to postgres user
 ```   
    su - postgres
```
20 Create a user named sonar.

    createuser sonar

21 Log in to PostgreSQL.

    psql

22 Set a password for the sonar user. Use a strong password in place of my_strong_password.
```
    ALTER USER sonar WITH ENCRYPTED password 'sonar';
```
23 Create a sonarqube database and set the owner to sonar.

     CREATE DATABASE sonarqube OWNER sonar;

24 Grant all the privileges on the sonarqube database to the sonar user.

    GRANT ALL PRIVILEGES ON DATABASE sonarqube to sonar;

25 Exit PostgreSQL.

    \q
    
26. Return to your non-root sudo user account.
```
    exit
```
sudo systemctl status sonar

27. Configure SonarQube. Edit the SonarQube configuration file.
```
    sudo nano /opt/sonarqube/conf/sonar.properties

    sonar.jdbc.username=sonar
    sonar.jdbc.password=sonar
    sonar.jdbc.url=jdbc:postgresql://localhost/sonarqube
    sonar.search.javaOpts=-Xmx512m -Xms512m -XX:MaxDirectMemorySize=256m -XX:+HeapDumpOnOutOfMemoryError
```
28. Now start the Sonarqube 
```
    sh /opt/sonarqube/bin/linux-x86-64/sonar.sh start
```
29. Access SonarQube in a web browser at your server's IP address on port 9000. For example:
    ```
    http://192.168.31.226:9000/projects/create
