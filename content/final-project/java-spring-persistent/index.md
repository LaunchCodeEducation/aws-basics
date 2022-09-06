---
title: "Java Spring Persistent"
date: 2022-05-04T14:45:47-05:00
draft: false
weight: 100
---

## Deploying a Persistent Spring Boot Application

Now that you have worked closely with the EC2 and S3 service it is time to take things one step further. You are going to deploy a web application that is connected to a MySQL database. 

Below you will find the steps outlined.

### Getting Organized
What needs to happen for the Java/Spring Persistent web application to be deployed?

You will need:
1. New `EC2` Instance
1. Built Artifacts of application cloned to `EC2` instance
1. Correct version of `Java` installed on `EC2`
1. Web Server installed on `EC2`
1. `Docker` installed to create a `MySQL` container for the database

#### EC2 Instance Created
1. `Name of Instance`: java-spring-persistent
1. `AMI`: Ubuntu 22.04
1. `Instance Type`: t2 micro
1. `Key Pair`: Not Required
1. `Security Group`: New Security Group:
    1. `HTTP` enabled

After creating your new `EC2` you can now use `EC2 Instance Connect` to connect to your virtual server. 

#### Project Artifacts
The artifacts are already built, they just need to be installed onto the virtual machine with `git`. 

1. use `git` to clone the build artifacts

{{% notice note %}}
Build artifacts for this deployment:
`https://github.com/LaunchCodeTechnicalTraining/java-techjobs-persistent-artifacts`
{{% /notice %}}

#### Java

This application uses `Java 11`. To install the correct version of `Java` you will be using your package manager.

Run the following command within the `EC2` instance through `EC2 Instance Connect`

```bash
sudo apt install openjdk-11-jre -y
```

#### Web Server
`caddy`, `nginx`, or some other web server must be installed to catch `HTTP` requests and respond as a `reverse_proxy` to our running application.

{{% notice "green" Bonus %}}
You can find Installation steps and further information for both `caddy` and `nginx` here:
- [Caddy Installation](https://launchcodetechnicaltraining.org/linux/web-server/caddy/setup/)
- [Nginx Installation](https://launchcodetechnicaltraining.org/linux/web-server/nginx/setup/)
{{% /notice %}}


#### Docker Installation

In order to keep everything inside of our virtual-server you will be utilizing `Docker` to run a `MySQL` container. 

This allows us to create a `MySQL` container inside of our virtual-server and configure it's settings so that our `Java` application is able to connect to it.

{{% notice note %}}
docker is an extremely useful tool and can be utilized in many different ways. To cover its entire purpose and numerous use cases is outside of the scope of this class. 

If you would like to continue reading and learn more about `docker` you can find the documentation here:
[docker docs](https://docs.docker.com/)
{{% /notice %}}

```bash
sudo apt update -y

sudo apt install apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y

apt-cache policy docker-ce

sudo apt install docker-ce
```

## Starting the Application

Now that you have:
1. Created a new `EC2`
    1. Cloned the build artifacts
    1. Installed `Java`
    1. Installed a Web Server
    1. Installed `docker`

You are ready to do the following:
1. Create a `MySQL` container using `docker`
1. Start the `Java-Spring` application
1. Configure the Web Server
1. Access the running application in your browser

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

Breakdown of command:
1. `sudo docker run --name name-of-container`: Creating a new container with any provided name
1. `-p 3306:3306`: specifying what port the database can be accessed
1. `-e MYSQL_ROOT_PASSWORD="admin" -e MYSQL_USER="techjobs"`: Environment variables with values
1. `-d mysql`: targeting `MySQL` docker image

{{% notice "green" Bonus %}}
If you would like to read the documentation for the `MySQL` `docker` image you can find the information here:

[Docker MySQL Image Docs](https://hub.docker.com/_/mysql)
{{% /notice %}}

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

You will need to edit the default `caddy` file. This walkthrough utilizes `vim` to edit the file.

{{% notice green "Bonus" %}}
If you need a refresher on `vim` or are unfamiliar with the tool you can find useful information here:

[Vim Walkthrough / Introduction](https://launchcodetechnicaltraining.org/linux/userspace-applications/walkthrough/vim/)
{{% /notice %}}

Run the following command:

```bash
sudo vim /etc/caddy/Caddyfile
```

Remove all content within the file.

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

#### Running Application

After completing the above steps you should now be able to open your browser to the `public-ipv4` address of your `EC2` instance to view the running application.

![Running Java Techjobs Persistent Application](pictures/running-techjobs-application.png?classes=border)



