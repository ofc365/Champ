## Install Jenkins

👉 https://www.jenkins.io/doc/book/installing/


### 1. Install Jenkins on Ubuntu (Linux)


```
sudo apt update
sudo apt install fontconfig openjdk-17-jre -y
```


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

Login to Jenkins : `server-ip:8080`

  
```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
   


### 2. Install Jenkins on Windows


```
https://www.oracle.com/in/java/technologies/downloads/#jdk21-windows
```


```
https://www.jenkins.io/download/thank-you-downloading-windows-installer-stable/
```


Login to Jenkins :  `localhost:8080`


------------------------------------
