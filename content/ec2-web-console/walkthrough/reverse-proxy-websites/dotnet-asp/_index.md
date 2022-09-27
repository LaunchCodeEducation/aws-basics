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
    - `https://github.com/LaunchCodeTechnicalTraining/dotnet-mvc-artifacts`
1. `dotnet` CLI installed
    - `dotnet-sdk-3.1`
1. Web Server Installed (Caddy)
    - Web Server configured (Caddy)

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

{{% notice note %}}
Check that the Package has been successfully installed running the following command: `which dotnet`
{{% /notice %}}

```bash
which dotnet
```
![Dotnet Package Installed Validation](pictures/dotnet-installed-check.png?classes=border)

You can see that the Package has been installed and is located in the `/usr/bin/` directory.

You can also check that you have the correct version installed with the following command:

```bash
dotnet --version
```

![Check Version of dotnet](pictures/dotnet--version.png?classes=border)

You can see that the version is `6.0.x`.

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

Now that you have cloned the project `build artifacts` and installed both the correct `SDK` and `Web Server`, you need to configure your Caddyfile.

{{% notice note %}}
The `ASP.NET` project will be running on port `5000`. That means you will need to configure a reverse proxy within your `Caddyfile` to handle the `HTTP` requests to port `5000` on the running server.
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
    reverse_proxy 127.0.0.1:5000
}
```

After making changes to your `Caddyfile` you will need to reload it with the following command:

```bash
sudo caddy reload --config /etc/caddy/Caddyfile
```

### Start ASP.NET Application

Now that the web server is configured you are ready to start your application.

Navigate to your `dotnet-mvc-artifacts` directory and run the following command:

```bash
dotnet run
```

![ASP.NET Run Command](pictures/dotnet-run.png?classes=border)

### Validation

Now that the application is up and running you should be able to access it within your browser.

Open a new browser window and access the application at `http://your-public-ipv4-address`

![Running ASP.NET Application](pictures/running-dotnet-application.png?classes=border)