## JENKINS INSTALLATION ON AMAZON-EC2-UBUNTU
===============================================


## 1. Launch AWS EC2 Instance

- Go to AWS Console
- Instances(running) :- ubuntu-22 or other
- t2.micro
- security group :- ssh, http, https, all traffic (anywhere)
- key pair :- jenkins-key.pem
- Launch instances


### Run the below commands to install Java and Jenkins

Install Java

```
sudo apt update
sudo apt install fontconfig openjdk-17-jre -y
```

Verify Java is Installed

```
java -version
```

Now, you can proceed with installing Jenkins
## YOU CAN FOLLOW : https://www.jenkins.io/doc/book/installing/linux/#debianubuntu

```
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y
jenkins --version

```

 *If your jenkins is not running then only, you can use this or else skip it👇👇
```
sudo systemctl start jenkins
sudo systemctl enable jenkins
```


### Login to Jenkins using the below URL :-


#### 1. By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.

- EC2 > Instances > Click on <Instance-ID>
- In the bottom tabs -> Click on Security
- Security groups
- Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed `All traffic`).

#### 2. http://(ec2-instance-public-ip-address):8080 

  
#### 3. After you login to Jenkins, generate password

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
      

#### 4. Click on Install suggested plugins


#### 5. Create First Admin User or Skip the step


#### 6. Start using the Jenkins 




## JENKINS INSTALLATION ON WINDOWS
===========================================

#### 1. Download java

`https://www.oracle.com/in/java/technologies/downloads/#jdk21-windows`

Install java

`java --version`

#### 2. Download Jenkins

`https://www.jenkins.io/download/thank-you-downloading-windows-installer-stable/`

Install


`login and access` =====>  `localhost:8080`
