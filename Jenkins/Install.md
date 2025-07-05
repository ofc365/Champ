## Install Jenkins


Step-by-step guide to install Jenkins on Ubuntu, Mac, and Windows

### 1. Install Jenkins on Ubuntu (Linux)

(Create ubuntu ec2-instance using t2.micro(all traffic))


Install Java


`sudo apt update`

`sudo apt install fontconfig openjdk-17-jre -y`


Now, you can proceed with installing Jenkins

👉 https://www.jenkins.io/doc/book/installing/linux/#debianubuntu

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

Login to Jenkins using the below URL :- EX- `http://(ec2-instance-public-ip-address):8080`

  

`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`
   

Click on Install suggested plugins


Start using the Jenkins 




### 2. Install Jenkins on Windows

Download java & Install java

`https://www.oracle.com/in/java/technologies/downloads/#jdk21-windows`


Download Jenkins & Install

`https://www.jenkins.io/download/thank-you-downloading-windows-installer-stable/`


`login and access` =====>  `localhost:8080`


-----
