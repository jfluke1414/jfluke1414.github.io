---
title: (Docker) how to use  and set up docker
category: Docker
order: 2
---

[최종]
### 1.
기존
실제 사용 docker run -d --restart=always --privileged -p 6502:80 --name viewer centos /sbin/init
docker run -i -t --restart=always --privileged -p 6502:80 --name viewer centos /bin/bash


### 2.
cd /root
docker cp kukudocs_linux_html_v1.0.2.4.zip viewer:/home/

### 3. 
docker exec -it viewer bash
yum install unzip -y
yum install net-tools -y
cd /home
unzip kukudocs_linux_html_v1.0.2.4.zip
tar -xvf project_linux_html_v1.0.2.4.tar

### 4.
vi /home/project_linux_html/config/default.json

{
  "PORT": "80",
 
  "DB": {
    "DRIVER"   : "sqlite"
  },
 
  "URL_HOST"   : "http://**.**.***.**:6502",
  "DIR_UPLOAD" : "uploads",
  "DIR_LOGS"   : "logs",
  "DEV_MODE"   : "false",
 
  "SERVICE_QUEUE_CONCURRENCY": 1,
 
  "PLUGIN" : ""
}

### 5. 
chmod 777 make.sh 
./make.sh
cp projectService /etc/init.d/
chmod +x /etc/init.d/projectService
/etc/init.d/projectService start