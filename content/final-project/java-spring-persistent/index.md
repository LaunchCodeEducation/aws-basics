---
title: "Java Spring Persistent"
date: 2022-05-04T14:45:47-05:00
draft: false
weight: 100
---

## Deploying a Persistent Spring Boot Application

Now that you have worked closely with the EC2 and S3 service it is time to take things one step further. You are going to deploy a web application that is connected to a MySQL database. Below you will find the steps outlined.

### Getting Organized
What needs to happen for the Java/Spring Persistent web application to be deployed?

#### EC2 Instance Created

#### Machine State
1. `git` must be installed
1. web server must be installed

#### Project Artifacts
The artifacts are already built, they just need to be installed onto the machine with `git`. 

1. use `git` to clone the build artifacts

{{% notice note %}}
Build artifacts for this deployment:
`https://github.com/LaunchCodeTechnicalTraining/java-techjobs-persistent-artifacts`
{{% /notice %}}

#### Web Server Configured
`caddy`, `nginx`, or some other web server must be configured to catch `HTTP` requests and respond as a `reverse_proxy` to our running application.

#### Environment Variables

#### Docker

#### Running Application



