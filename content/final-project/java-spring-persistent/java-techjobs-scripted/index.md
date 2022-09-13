---
title: "Scripting with User Data"
date: 2022-05-04T14:45:47-05:00
draft: false
weight: 105
---

## Deploying a Persistent Spring Boot Application With User Data

After deploying the persistent Java application you can take things one step further and create your `EC2` instance providing `User Data`

`User Data` is a way for us to give instructions to the `EC2` instance to complete on creation. This allows you to automate the process of installing the requirements to deploy your web application.

### Getting Organized
This walkthrough will take the `Java/Spring` application deployment requirements and store them inside of one script.

The Script will need:
1. Built Artifacts of application cloned to `EC2`
1. Correct version of `Java` installed on `EC2`
1. Web Server installed on `EC2`
1. Web Server file configured
1. `public-ipv4` address of web server
    1. This will be needed for the web server configuration
1. `Docker` installed to create a `MySQL` container for the database
1. Bash Heredoc within script to write to Web Server configuration file

### Scripting with Bash

This walkthrough will be completing the above task utilizing a `Bash` script.

{{% notice "green" Bonus %}}
The steps to manually deploy the application have been included below. The goal of this walkthrough is to have the script perform all of these steps so that the entire process is automated. For more information on scripting please reference the ["Bash: Scripting" section from the Linux Curriculum](https://launchcodetechnicaltraining.org/linux/bash-scripting/)
{{% /notice %}}

#### Project Artifacts
The artifacts are already built, they just need to be installed onto the virtual machine with `git`. 

1. use `git` to clone the build artifacts

{{% notice note %}}
Build artifacts for this deployment:
`https://github.com/LaunchCodeTechnicalTraining/java-techjobs-persistent-artifacts`
{{% /notice %}}

#### Java

This application uses `Java 11`. To install the correct version of `Java` you will be using your package manager.

The following command will accomplish that.

```bash
sudo apt install openjdk-11-jre -y
```

#### Web Server
`caddy`, `nginx`, or some other web server must be installed to catch `HTTP` requests and respond as a `reverse_proxy` to the running application.

{{% notice "green" Bonus %}}
You can find Installation steps and further information for both `caddy` and `nginx` here:
- [Caddy Installation](https://launchcodetechnicaltraining.org/linux/web-server/caddy/setup/)
- [Nginx Installation](https://launchcodetechnicaltraining.org/linux/web-server/nginx/setup/)
{{% /notice %}}


#### Docker Installation

In order to keep everything inside of our virtual-server you will be utilizing `Docker` to run a `MySQL` container. 

This allows us to create a `MySQL` container inside of our virtual-server and configure it's settings so that our `Java` application is able to connect to it.

`Docker` can be installed using the below commands:

```bash
sudo apt update -y

sudo apt install apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y

apt-cache policy docker-ce

sudo apt install docker-ce
```

#### Creating the MySQL Docker Container

`Environment Variables`: docker allows the user to provide enviroment variables when creating the `MySQL` container.

The available environment variables you will be using are as follows:
- `MYSQL_ROOT_PASSWORD`: Required variable when creating a `MySQL` docker container
- `MYSQL_USER`: Specifies username for database
- `MYSQL_PASSWORD`: Specifies password for the username
- `MYSQL_DATABASE`: Specifies name of database

Run the below command to create the `MySQL` container:

```bash
sudo docker run --name name-of-container -p 3306:3306 -e MYSQL_ROOT_PASSWORD="admin" -e MYSQL_USER="techjobs" -e MYSQL_PASSWORD="tech" -e MYSQL_DATABASE="techjobs" -d mysql
```

#### Starting Java-Spring Application

This application was created using environment variables in order to connect to the `MySQL` database. 

Similar to creating the `docker` image you will need to assign the variables values when starting the java application.

The available environment variables you will be using are as follows:
- `RDS_ENDPOINT`: Endpoint for `MySQL` database. This value will be the auto-assigned `ipv4-address` of your `EC2` instance
- `DB_PORT`: Port `MySQL` is running on (3306)
- `DB_NAME`: Name of database
- `DB_USERNAME`: Username 
- `DB_PASSWORD`: Password
- `SERVER_PORT`: Designated Port that you want the application to run on.

Run the following command to boot your `Java-Spring` project and connect to the `MySQL` database:

```bash
java -DRDS_ENDPOINT="ipv4-address" -DDB_PORT="3306" -DDB_NAME="techjobs" -DDB_USERNAME="techjobs" -DDB_PASSWORD="tech" -DSERVER_PORT="8080" -jar path/to/build/artifacts/java-techjobs-persistent-artifacts.jar 
```
{{% notice warning %}}
You will need to replace the `-DRDS_ENDPOINT="ipv4-address"` with the public `ipv4-address` of your `EC2`!

You will also need to specify the path to the `.jar` file within your `EC2` instance.
{{% /notice %}}

#### Configure Web Server

This walkthrough will utilize `caddy` for the web server.

You will need to write the required content to the `caddy` config file with a `Bash Heredoc`.

Add the following content:

```bash
your-public-ipv4-address {
    reverse_proxy 127.0.0.1:8080
}
```
Write and Quit the file.

##### Reload Caddy

In order for the changes you made to the default `caddy` file to take effect you will need to reload `caddy`.

Run the following command:

```bash
sudo caddy reload --config /etc/caddy/Caddyfile
```

{{% expand "Click here for Caddy Troubleshooting" %}}
If you are having issues with caddy you may need to run the following commands.

```bash
sudo systemctl stop caddy
```

```bash
sudo caddy start
```

```bash
sudo caddy reload --config /etc/caddy/Caddyfile
```
{{% /expand %}}

{{% expand "Script Solution" %}}
```bash
public_ipv4_address=$(curl http://169.254.169.254/latest/meta-data/public-ipv4) 
export public_ipv4_address

sudo apt update -y

## Clone Build Artifacts

git clone https://github.com/LaunchCodeTechnicalTraining/java-techjobs-persistent-artifacts

## Install Java

sudo apt install openjdk-11-jre -y

## Install Caddy

sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https

curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg

curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list

sudo apt update

sudo apt install caddy

## Docker Install

sudo apt update -y 
 
sudo apt install apt-transport-https ca-certificates curl software-properties-common 
 
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg 
 
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null 
 
sudo apt update 
 
apt-cache policy docker-ce 
 
sudo apt install docker-ce 
 
## Create Docker MySQL Container 
 
sudo docker run --name java-scripted-mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD="admin" -e MYSQL_USER="techjobs" -e MYSQL_PASSWORD="tech" -e MYSQL_DATABASE="techjobs" -d mysql 
 
## Configure Web Server with Heredoc 
 
( 
cat <<EOF 
http://$public_ipv4_address { 
        reverse_proxy 127.0.0.1:8080 
}
EOF
) > Caddyfile

## Reload Caddy

sudo caddy reload

## Start Java Project

sudo java -DRDS_ENDPOINT="127.0.0.1" -DDB_PORT="3306" -DDB_NAME="techjobs" -DDB_USERNAME="techjobs" -DDB_PASSWORD="tech" -DSERVER_PORT="8080" -jar /home/ubuntu/java-techjobs-persistent-artifacts/java-techjobs-persistent-artifacts.jar
```
{{% /expand %}}



