Step-1 First, open a terminal window and update the system package repository by running:
```
sudo apt update
```
Step-2- To install OpenJDK 17, run:
```
sudo apt install openjdk-17-jdk -y
```
Step-3: Create Group as nexus
```
sudo groupadd nexus
```
Step-4: Add nexus User

```
sudo useradd -m -s /bin/bash nexus -g nexus
```
Step-6 Create Password for nexus user
```
sudo passwd nexus
```
Step-7 edit Sudoers file
```
visudo
nexus ALL=(ALL) NOPASSWD: ALL
```
Step-8 Download nexus in /opt
```
https://download.sonatype.com/nexus/3/nexus-3.44.0-01-unix.tar.gz
```

Step-9 Untar (extract the file)
```
tar -xvzf nexus-3.44.0-01-unix.tar.gz
```
Step-10 Edit the nexus.rc file as below
```
sudo vi /opt/nexus/bin/nexus.rc
run_as_user="nexus"

```
Step-11
Check the below file
vi  /opt/nexus/bin/nexus.vmoptions 

    	  -Xms2703m
        -Xmx2703m
        -XX:MaxDirectMemorySize=2703m
        -XX:+UnlockDiagnosticVMOptions
        -XX:+LogVMOutput
        -XX:LogFile=../sonatype-work/nexus3/log/jvm.log
        -XX:-OmitStackTraceInFastThrow
        -Djava.net.preferIPv4Stack=true
        -Dkaraf.home=.
        -Dkaraf.base=.
        -Dkaraf.etc=etc/karaf
        -Djava.util.logging.config.file=etc/karaf/java.util.logging.properties
        -Dkaraf.data=./sonatype-work/nexus3
        -Dkaraf.log=./sonatype-work/nexus3/log
        -Djava.io.tmpdir=./sonatype-work/nexus3/tmp
        -Dkaraf.startLocalConsole=false
        -Djdk.tls.ephemeralDHKeySize=2048

Step-12 Change default port if needed: 
```
vi /opt/nexus/etc/nexus-default.properties
```
Step-13 Add Nexus as service editing below file
```
sudo vi /etc/systemd/system/nexus.service
```
```
[Unit]
Description=nexus service
After=network.target

[Service]
Type=forking
LimitNOFILE=65536
ExecStart=/opt/nexus/bin/nexus start
ExecStop=/opt/nexus/bin/nexus stop
User=nexus
Restart=on-abort

[Install]
WantedBy=multi-user.target
```
Step-14 Check the Status of Nexus
```
sudo systemctl status nexus
```
```
sudo chkconfig nexus on
```
```
sudo systemctl start nexus
```
```
sudo systemctl enable nexus
```
```
sudo systemctl stop nexus
```
```
sudo systemctl restart nexus
```

curl -X GET http://192.168.31.79:8081/service/rest/v1/repositories/maven-releases --user admin:Nexus@1234

# Example
sudo cat > /etc/docker/daemon.json <<EOF
{
 "insecure-registries": ["192.168.31.79:8082"]
}
EOF
systemctl restart docker

docker tag alpine:latest 192.168.31.79:8082/alpine:latest

docker push 192.168.31.79:8082/alpine:latest


http://192.168.31.79:8081
