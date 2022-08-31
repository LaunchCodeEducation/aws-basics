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
You can find Installation steps for both `caddy` and `nginx` here:
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

#### Environment Variables

This application was created using environment variables in order to connect to the `MySQL` database. 

This was done for multiple reasons:
1. `Security`
1. `Ease of use`
1. `Ability to change database settings`

#### Running Application

After completing the above steps you should be able to open your browser to the `public-ipv4` address of your `EC2` instance to view the running application.

![Running Java Techjobs Persistent Application](pictures/running-techjobs-application.png?classes=border)


