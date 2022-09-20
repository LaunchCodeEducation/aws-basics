---
title: "ASP.NET MVC"
date: 2022-05-04T13:45:41-05:00
draft: false
weight: 105
---

## Reverse Proxy for MVC Application

This walkthrough will take an MVC application and proxy the `HTTP` requests to the running application server.

{{% notice note %}}
The build artifacts for this walkthrough are located here:
`https://github.com/LaunchCodeTechnicalTraining/dotnet-mvc-artifacts`
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

![connect-to-instance](pictures/connect-to-instance.png?classes=border)

Verify your settings are similar to the above screenshot within the `EC2 Instance Connect` tab.

Click the `Connect` button.

![connected to ec2 instance](pictures/connected-to-instance-view.png?classes=border)

Now that you have connected to your instance it is always good practive to update your server.

Run the following command:

```bash
sudo apt update -y
```

### Project Requirements

In order start our `C#/ASP.NET` application you will need the following:
1. Project Artifacts cloned
    1. `https://github.com/LaunchCodeTechnicalTraining/dotnet-mvc-artifacts`
1. `dotnet` CLI installed
    1. `dotnet-sdk-3.1`
1. Web Server Installed (Caddy)
    1. Web Server configured (Caddy)

### Clone Project Artifacts

```bash
git clone https://github.com/LaunchCodeTechnicalTraining/dotnet-mvc-artifacts
```

![Clone dotnet Project Build Artifacts](pictures/clone-dotnet-artifacts.png?classes=border)

### Install dotnet-sdk

```bash
sudo apt install dotnet-sdk-6.0
```

Confirm that you want to Install the Package:

![Install Dotnet SDK Package](pictures/apt-install-dotnet-Y.png?classes=border)

Check that the Package has been successfully installed running the following command:

```bash
which dotnet
```

![Dotnet Package Installed Validation](pictures/dotnet-installed-check.png?classes=border)

You can see that the Package has been installed and is located in the `/usr/bin/` directory.

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


