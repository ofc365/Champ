## Install Docker


👉 https://docs.docker.com/get-docker/


### Install Docker on Ubuntu (Linux)


```
sudo apt update
sudo apt install docker.io -y

sudo systemctl status docker
sudo systemctl start docker

docker --version
```

Grant Access : `sudo usermod -aG docker ubuntu`

(You need to logout and login back for the changes to be reflected.)


You can create an Linux EC2 Instance on AWS and run the below commands to install docker `sudo yum install docker -y`


----------------------------------
