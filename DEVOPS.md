hashing algorithms are used to generate random numbers
To understand git we will be using two plumbing commits
git cat-file -t 8414636
it tells  type of what you are looking at
git cat-file -p 8414636
it prints type of values
git doesnot have parent is called first commit

now we have 3 commits
Preview
blob--file


###################
INSTALL TERRAFORM ON UBUNTU
-----------------------------------
#!/bin/bash
sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
wget -O- https://apt.releases.hashicorp.com/gpg | \
gpg --dearmor | \
sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
gpg --no-default-keyring \
--keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
--fingerprint
echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update
sudo apt-get install terraform -y
terraform -install-autocomplete

#############
INSTALL AS CLI ON LINUX
sudo apt install unzip curl -y
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

#DOCKER INSTALL 
#!/bin/sh
# Docker CE for Linux installation script
#
# See https://docs.docker.com/engine/install/ for the installation steps.
#
# This script is meant for quick & easy install via:
#   $ curl -fsSL https://get.docker.com -o get-docker.sh
#   $ sh get-docker.sh
#
# For test builds (ie. release candidates):
#   $ curl -fsSL https://test.docker.com -o test-docker.sh
#   $ sh test-docker.sh

Dockerfile Introduction
In this section we would cover Dockerfiles and instructions.
Dockerfile is a simple plain text file that contains set of user defined instructions which will be call during building the image.
Click here for Dockerfile reference
Syntax
Generic Syntax is INSTRUCTION arguments for eg FROM alpine or RUN echo 'Hello'
Dockerfile should start with a FROM instruction which specifies the base image.
Docker File Instructions
FROM:

Syntax is FROM <image>[:tag] [As <name>].
note: any thing in [] above are optional
This instruction sets the base image.
Multiple FROM statements are also allowed to support multistage builds
Refer here for more info
LABEL :

Adds metadata to the image
Refer Here for more info.
RUN :

This command takes arguments in two forms
Shell form: RUN <command>
In this command runs in a shell
exec form: RUN ["executable", "param1", "param2" ]
In this way comand execution doesn’t require a defaault shell
Each RUN instruction will execute the commands in the new layer on top of current image
Refer Here for more info.
COPY

copies file from soure to destination.
Syntax: COPY <src> <dest>
src in above syntax is only files and directories . URL’s are not supported
Refer Here for more info
ADD

copies file from soure to destination.
Syntax: ADD <src> <dest>
src in above syntax is only files and directories . URL’s are supported as source.
Refer Here for more info
ENTRYPOINT

Command which gets executed when the docker container is created from image.
CMD acts as argument to the ENTRYPOINT
Refer Here for more info
CMD

Refer Here for more info
TO understand CMD and ENTRYPOINT interatction refer here
EXPOSE

Refer Here
Building an Image
Lets build a spring-pet-clinic app image

Manually to execute spring pet clinic

Clone from Github using the following HTTPS url. git clone https://github.com/spring-projects/spring-petclinic.git

Ensure Java and maven are installed.

Execute the following command to build the image mvn package

Copy spring-petclinic*.jar file from target folder to any folder in your linux machine.

Execute the following command to run the container “` java -jar spring-petclinic*.jar“

From the above understanding lets write the Dockerfile

Create a new directory called as spring-petclinic
Create a file called as Dockerfile
Copy the spring-petclinic.jar to samefolder
Insert the following contents
FROM openjdk:8
LABEL author="KHAJA"
LABEL version="1.0"
COPY ./spring-petclinic.jar /spring-petclinic.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar"] 
CMD ["/spring-petclinic.jar"]
Execute the docker image build command docker image build -t springpetclinic:1.0 .
Try to create container with following command
docker container run -d -p 8080:8080 springpetclinic:1.0
Lets examine the layers

Execute the following command docker image inspect openjdk:8
Navigate to Layers and have a look at highlighted layers Preview
Total we have seven layers
Now execute the following command docker image inspect springpetclinic:1.0 and Navigate to layers section

DOCKER COMMANDS:
###image naming convention
[username]/[repository]:[<tag>]
shaikkhajaibrahim/myspc:1.0.1
username => shaikkhajaibrahi
repository => what image => myspc
tag => version => 1.0.1
===================================
default tag is latest
nginx
nginx:latest
==============================
official images dont have username
nginx
ubuntu
alpine
shaikkhajaibrahim/myspc
=============================================
Lets pull the image from docker hub nginx with tag 1.23
docker image pull nginx:1.23
docker image ls
===================================
Remove images from local
`docker image rm $(docker image ls -q)
===============================
Create a container with nginx
docker container run -d nginx
"-d"--->detached mode 
===================================
Remove all the running containers 
docker container rm -f $(docker container ls -q )
========================
Remove specific container
docker container rm nginx1
Remove all containers 
docker container rm -f $(docker container ls -a -q )
=======================
Docker container lifecycle
Docker lifecycle states
Created
Running
Paused
Stopped
Deleted
======================
Port-forwording
ommand: docker container run -d -p <host-port>:<container-port> <image>
Create a nginx container and expose on port 30000 
docker container run -d -p 30000:80 --name nginx1 nginx
----------------------------------------
Create a jenkins container & expose 8080 port on 30001 port of host
 docker container run -d -p 30001:8080 --name jenkins1 jenkins/jenkins
=====================================
Dockerfile based Image building
Springpetclinic Dockerfile
FROM amazoncorretto:11
RUN curl https://referenceapplicationskhaja.s3.us-west-2.amazonaws.com/spring-petclinic-2.4.2.jar -o spring-petclinic-2.4.2.jar
EXPOSE 8080
CMD ["java", "-jar", "spring-petclinic-2.4.2.jar"]
---------------------------------------
To build docker image 
docker image build -t myspc:corretto11
To run the container 
docker container run -d -P --name sridhar myspc:corretto11
----------------------------------------
Approach 2: Start from some os
FROM alpine:3
RUN apk add openjdk11
RUN wget https://referenceapplicationskhaja.s3.us-west-2.amazonaws.com/spring-petclinic-2.4.2.jar
EXPOSE 8080
CMD ["java", "-jar", "spring-petclinic-2.4.2.jar"]
To build  the image 
docker image build -t myspc1:alpine
To build container 
docker container run -d -P --sri myspc1:alpine


*********************************************************
Install python onn 

** Install python/pip**

apk add update
apk add --update --no-cache python3 && ln -sf python3 /usr/bin/python
python3 -m ensurepip
pip3 install --no-cache --upgrade pip setuptools
--------------------------------------------------------------



---------------------------------------------


FROM ubuntu:22.04
LABEL Author="Sridhar" Organization="QT" Project="Learning"
RUN apt update
RUN apt install openjdk-11-jdk -y 
RUN apt install curl -y
RUN curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key |  tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
RUN echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ |  tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
RUN apt update && apt install jenkins -y
EXPOSE 8080 
CMD ["/usr/bin/jenkins"]


 ###############################################
 ******************   
Create container Postgress
    docker container run --name postgresq -e POSTGRES_USER=panoramic -e POSTGRES_PASSWORD=trekk
ing -e POSTGRES_DB=psqldata -d -P postgres:15
docker exec -it postgresq /bin/bash
psql -U panoramic -W trekking -d psqldata
\l
psqldata=# use emloyees;
ERROR:  syntax error at or near "use"
LINE 1: use emloyees;
        ^
psqldata=# CREATE TABLE Persons (
    PersonID int,
    LastName varchar(255),
    FirstName varchar(255),
    Address varchar(255),
    City varchar(255)
);
CREATE TABLE
psqldata=# Insert into Persons Values (1,'test','test', 'test', 'test');
INSERT 0 1
psqldata=# Select * from Persons;
 personid | lastname | firstname | address | city
----------+----------+-----------+---------+------
        1 | test     | test      | test    | test
(1 row)

--------------------------------------------------------------
Try creating dockerfile which runs on phpinfo page,user ARG & ENV whereever appropriate a) on apache server   b)on nginx server

FROM ubuntu/apache2
LABEL Author="Sridhar" Organization="QT" Project="Learning"
RUN apt update
RUN apt install php libapache2-mod-php -y
RUN apt install php-cli -y 
RUN apt install php-cgi -y 
RUN apt install php-mysql -y 
RUN apt install php-pgsql -y
RUN echo "<?php phpinfo(); ?>" >> /var/www/html/# info.php
EXP
OSE 80

Try creating dockerfile which runs on phpinfo page,user ARG & ENV whereever appropriate  b)on nginx server

FROM ubuntu/nginx
LABEL Author="Sridhar" Organization="QT" Project="Learning"
RUN apt-get update && apt-get upgrade 
RUN nginx -v
RUN nginx -t
RUN systemctl stop nginx.service
RUN systemctl start nginx.service
RUN systemctl enable nginx.service
RUN systemctl restart nginx.service
##  Step 2: PHP Install and Version Check
RUN apt-get -y install php7.0 php7.0-fpm -y
RUN apt-get upgrade
RUN systemctl status php7.0-fpm
RUN cd ~
RUN cd /etc/nginx
RUN cd etc/php/
RUN vim 7.0/fpm/php.ini
RUN cp php.ini php.ini_copy
RUN systemctl restart nginx.service
RUN vim /var/www/html/phpinfo.php
RUN echo "<?php phpinfo(); ?>" >> vim /var/www/html/phpinfo.php
EXPOSE 80

*************************************************************
1.docker network create mybridge
2.docker run -d --network mybridge --name mysri -v myvolume:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=sridhar -e MYSQL_DATABASE=employees -e MYSQL_USER=qtdevops -e MYSQL_PASSWORD=rootroot mysql:8
  vi Dockerfile
3.docker image build -t nopimage:4.60.2 .
4.docker container run -d -P --network mybridge --name nop -v myvolume:/var/lib/mysql -e     
   MYSQL_ROOT_PASSWORD=sridhar -e MYSQL_DATABASE=employees  nopimage:4.60.2

+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
Method-II
==========
docker network create --driver bridge nop-net
docker volume create nop-db
docker container run --name mysql --network nop-net -d \
    -e MYSQL_ROOT_PASSWORD=rootroot \
    -e MYSQL_USER=nop \
    -e MYSQL_PASSWORD=rootroot \
    -v nop-db:/var/lib/mysql \
    mysql:8
vi Dockerfile
docker container run --name nop --network nop-net \
    -P -d nop:4.60.2
    In the install page, pass connection string
server=mysql;uid=root;pwd=rootroot;database=nop
------------------------------------------------------------------------------
Docker Workshop -3 
 &&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&&
1.	Create a multistage docker file to build  
a.	nop commerce  
b.	spring petclinic 
FROM alpine/git AS vcs
RUN cd / && git clone https://github.com/spring-projects/spring-petclinic.git && \
    pwd && ls /spring-petclinic

FROM maven:3-amazoncorretto-17 AS builder
COPY --from=vcs /spring-petclinic /spring-petclinic
RUN ls /spring-petclinic 
RUN cd /spring-petclinic && mvn package

FROM amazoncorretto:17-alpine-jdk
LABEL author="khaja"
EXPOSE 8080
ARG HOME_DIR=/spc
WORKDIR ${HOME_DIR}
COPY --from=builder /spring-petclinic/target/spring-*.jar ${HOME_DIR}/spring-petclinic.jar
EXPOSE 8080
CMD ["java", "-jar", "spring-petclinic.jar"]
--------------------------------------------------
c.	student courses register 
FROM python:3.7-alpine
LABEL author=SRIDHAR
LABEL blog=directdevops.blog
ARG HOME_DIR='/studentcourses'
ADD . $HOME_DIR
ENV MYSQL_USERNAME='directdevops'
ENV MYSQL_PASSWORD='directdevops'
ENV MYSQL_SERVER='localhost'
ENV MYSQL_SERVER_PORT='3306'
ENV MYSQL_DATABASE='test'
EXPOSE 8080
WORKDIR $HOME_DIR
RUN pip install -r requirements.txt
ENTRYPOINT ["python", "app.py"]

-----------------------------------------------------
git clone https://github.com/DevProjectsForDevOps/StudentCoursesRestAPI.git
cd StudentCoursesRestAPI
docker image build -t scr:latest
docker network create -d bridge scr_bridge
docker volume create scr_db
docker container run -d --name mysql -e MYSQL_ROOT_PASSWORD=password -e MYSQL_DATABASE=test -e MYSQL_USER=directdevops -e MYSQL_PASSWORD=directdevops --network scr_bridge -v scr_db:/var/lib/mysql mysql:5.6
docker container run -d --name mypythonapp -e MYSQL_SERVER=mysql --network scr_bridge -P scr:latest
+++++++++++++++++++++++++++++++++++++++++
2.	Push the images to  
a.	AWS ECR 
b.	Azure ACR 
--------------------------------------------------
3.	Write a docker compose file for 
a.	Nop Commerce 
---
version: "3.9"
services:
  nop:
    build:
      context: .
      dockerfile: Dockerfile
    networks:
      - nop-net
    ports:
      - "35000:5000"
    depends_on:
      - nop-db

  nop-db:
    image: mysql:8
    networks:
      - nop-net
    volumes:
      - nop-db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=rootroot
      - MYSQL_USER=nop
      - MYSQL_PASSWORD=rootroot
      - MYSQL_DATABASE=nop
volumes:
  nop-db:
networks:
  nop-net:
  --------------------------------------
b.	Spring petclinic 


c.	Game of life 
d.	Student Courses Register 
---------------------------------------------
FROM 
RUN wget https://github.com/wakaleo/game-of-life.git

apt update
    2  git -version
    3  apt install git
    4  git clone https://github.com/wakaleo/game-of-life.git
    5  ls
    6  cd game-of-life/
    7  ls
    8  apt install openjdk-8-jdk maven -y
    9  mvn --version
   10  java -version
   11  mvn -version
   12  history

 



