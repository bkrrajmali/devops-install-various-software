# Install Jenkins on Ubuntu 22.04 LTS

Step-1-First, open a terminal window and update the system package repository by running:

  ```bash 
    sudo apt update  
   ```
Step-2- To install OpenJDK 11, run:
  ```bash 
  sudo apt install openjdk-11-jdk -y
  ```
Step-3- First, add the repository key to the system:
```bash
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y
```

Step-4- sudo systemctl start jenkins 
```bash
sudo systemctl status jenkins
```
Step-5- Open the port if its blocked
```bash
sudo ufw allow 8080
sudo ufw enable
```
Step-6- Check the status 
```bash
sudo ufw status
```
Step-7- Accessing Jenkins which is running on default port 8080
  we can use http://localhost:8080 or we can use public ip http://<publicIP>:8080
  ![Screenshot_20221218_104937](https://user-images.githubusercontent.com/24952643/208282799-6e83a3d8-84fe-457d-a52b-cdd6d2911e0d.png)
 
Step-7 - we can retrive password as below
  
  ```bash
  sudo cat /var/lib/jenkins/secrets/initialAdminPassword
 ```
 
 Step-8 - We will get below screen after we login, we can choose either options:
  ![Screenshot_20221218_105308](https://user-images.githubusercontent.com/24952643/208282899-dd469319-3c5f-4e20-870a-3f437f421005.png)
  
  ![Screenshot_20221218_110113 (1)](https://user-images.githubusercontent.com/24952643/208283142-89fda131-8fed-4f1e-a5b1-d2410a0c3e37.jpg)
  
Step-9- Create Admin user and password or you can continue with existing admin user
  
  ![Screenshot_20221218_110438](https://user-images.githubusercontent.com/24952643/208283186-4b41713c-ae75-4cb8-abcb-8d8cd305b75a.jpg)

Step-10 - Once we are done with everything we get as below:
  
  ![Screenshot_20221218_110752](https://user-images.githubusercontent.com/24952643/208283266-8c9cf8a3-3b16-4f8b-b367-0c69e586cd04.jpg)

Step-11 - Create New Project by clicking on NewItem and we get below screen and then enter New Project Name, Select FreeStyle Project and click ok below
  
  ![Screenshot_20221218_111046](https://user-images.githubusercontent.com/24952643/208283394-74ce1287-f114-440c-8be0-3c3bf864a4e0.jpg)
  
Step-12- Enter description
  
  ![Screenshot_20221218_111428](https://user-images.githubusercontent.com/24952643/208283441-4a301d2f-63b4-4f92-8885-145fb3c8a857.png)
  
Step-13 -

![Screenshot_20221218_111631](https://user-images.githubusercontent.com/24952643/208283603-7a062d24-5770-417e-9292-76f91e6e847c.png)
  
![Screenshot_20221218_111727](https://user-images.githubusercontent.com/24952643/208283601-20a9c0c3-fd21-4b75-a8bb-be69ed271b6e.png)

Step-14 - Save

Step-15 - Now Click on Build
  
![Screenshot 2022-12-18 112040](https://user-images.githubusercontent.com/24952643/208283722-67d46bf8-ccab-48a4-80c1-27ce41251f1d.jpg)
  
![Screenshot 2022-12-18 112402](https://user-images.githubusercontent.com/24952643/208283783-b05fc937-8b3d-404f-875e-20c1785ce3a7.jpg)
  
![Screenshot 2022-12-18 112429](https://user-images.githubusercontent.com/24952643/208283787-9986f025-9453-499b-94a1-02cb306ae0d5.jpg)
