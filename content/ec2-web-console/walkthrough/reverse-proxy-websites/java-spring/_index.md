---
title: "Java Spring MVC"
date: 2022-05-04T13:45:41-05:00
draft: false
weight: 100
---

## Reverse Proxy for MVC Application

This walkthrough will take a `Java/Spring` application and proxy the `HTTP` requests to the running application server.

{{% notice note %}}
The build artifacts for this walkthrough are located here:
`https://github.com/LaunchCodeTechnicalTraining/spring-techjobs-mvc-artifact`
{{% /notice %}}

### Machine Settings

Create a new `EC2` instance with the following:
1. Name: `your-ec2-name`
1. AMI: `Ubuntu 22.04 LTS`
1. Instance Type: `t2-micro (free tier)`
1. Key Pair: `Proceed without a key pair`
1. Network Settings:
    1. VPC: `Default`
    1. Subnet: `Default`
    1. Auto-assign public IP: `Enabled`
    1. Create Security Group
        1. `Allow SSH traffic`
        1. `Allow HTTPs traffic`
        1. `Allow HTTP traffic`
1. Storage: `Default settings`
1. Advanced Details: `Default settings`

### Connecting to EC2 Instance

After the EC2 has been created navigate to the dashboard of the `EC2 instance`.

Click on the connect button which will take you to the `Connect to Instance` page.

![Connect to EC2 Instance Page](pictures/connect-to-instance-page.png?classes=border)

Verify your settings are similar to the above screenshot within the `EC2 Instance Connect` tab.

Click the `Connect` button.

![EC2 Instance Connect View](pictures/ec2-instance-connect.png?classes=border)

Now that you have connected to your instance it is always good practive to update your server.

Run the following command:

```bash
sudo apt update -y
```

### Project Requirements

In order start our `Java/Spring` application you will need the following:
1. Project Artifacts cloned
    - `https://github.com/LaunchCodeTechnicalTraining/spring-techjobs-mvc-artifact`
1. `open-jdk` installed
    - `openjdk-11-jre`
1. Web Server Installed (Caddy)
    - Web Server configured (Caddy)

### Clone Project Artifacts

```bash
git clone https://github.com/LaunchCodeTechnicalTraining/spring-techjobs-mvc-artifact
```

![Clone Spring Project Artifacts](pictures/git-clone-spring-artifacts.png?classes=border)

### Install Java SDK

```bash
sudo apt install openjdk-11-jre
```

Validate that it was installed correctly with the following commands:

```bash
which java
```

```bash
java --version
```

![Validate openjdk Installation](pictures/validate-openjdk-install.png?classes=border)

{{% notice note %}}
You can see that the `openjdk-11` Runtime Environment was installed correctly. This will allow us to start our `Java` project using the build artifacts provided.
{{% /notice %}}

### Install Caddy

```bash
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
```

```bash
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
```

```bash
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
```

```bash
sudo apt update
```

```bash
sudo apt install caddy
```

{{% notice note %}}
Verify that caddy was installed using the following commands:
{{% /notice %}}

```bash
which caddy
```

```bash
caddy version
```

![Caddy Installation Validation](pictures/caddy-install-validation.png?classes=border)

### Configure Web Server

Now that you have cloned the project `build artifacts` in addition to installing the correct `Java runtime environment` and `Web Server` you need to configure your `Caddyfile`.

{{% notice note %}}
The `Spring` project will be running on port `8080`. That means you will need to configure a reverse proxy within your `Caddyfile` to handle the `HTTP` requests to port `8080` on the running server.
{{% /notice %}}

Run the following command to open your default `Caddyfile`:

```bash
sudo vim /etc/caddy/Caddyfile
```

![Default Caddyfile View](pictures/default-caddyfile.png?classes=border)

Remove all content within the file and overwrite it with the following:

{{% notice "green" Bonus %}}
If you need a refresher on how to use `vim` you can visit the `Linux` curriculum here: [Vim Introduction](https://launchcodetechnicaltraining.org/linux/userspace-applications/walkthrough/vim/)
{{% /notice %}}

```bash
http://your-public-ipv4-address {
    reverse_proxy 127.0.0.1:8080
}
```

After making changes to your `Caddyfile` you will need to reload it with the following command:

```bash
sudo caddy reload --config /etc/caddy/Caddyfile
```

### Start Java/Spring Application

Now that the web server is configured you are ready to start your application.

Navigate to your `spring-techjobs-mvc-artifacts` directory and run the following command:

```bash
java -jar spring-mvc.jar
```

![Running Spring Application](pictures/running-spring-application.png?classes=border)

### Validation

Now that the application is up and running you should be able to access it within your browser.

Open a new browser window and access the application at `http://your-public-ipv4-address`

![Spring Application In Browser](pictures/spring-application-browser.png?classes=border)