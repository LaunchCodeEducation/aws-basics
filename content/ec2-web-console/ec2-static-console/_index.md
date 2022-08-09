---
title: "EC2 Static Website Console"
date: 2022-05-04T13:45:41-05:00
draft: false
weight: 110
---

## AWS EC2 Static Website Console

Now you are ready to deploy a static website to a brand new EC2 instance. Let's begin by creating a brand new EC2. Below you will find the appropriate settings for this walkthrough.

### EC2 Settings

- `Name`: "first-static-website"
- `Machine Image`: "Ubuntu 22.04 LTS"
- `Instance Type`: "t2.micro"
- `Key Pair`: "first-key-pair"
- `Security Group`: "Create Security Group"
	- Allow SSH Traffic from Anywhere
	- Allow HTTPs traffic from the internet
	- Allow HTTP Traffic from the internet
- `Storage`: Default


Once you have all of the above options selected you are ready to launch your EC2 instance.

### Validation

Click the `Launch Instance` button.

![first-static-website on ec2 dashboard](pictures/first-static-website.png?classes=border)

Click on the `Instance ID` to view the summary page for the new EC2 instance.

![first-static-website summary](pictures/first-static-website-summary.png?classes=border)


### Connect to the Instance

![connect-to-instance-image](pictures/first-static-website-summary.png?classes=border)

Click on the `Connect` button.

### EC2 Instance Connect

![ec2-instance-connect-view](pictures/ec2-instance-connect.png?classes=border)

Within the `EC2 Instance Connect` click on the `Connect` button.

{{% notice note %}}
The `Instance ID` and the `Public IP Address` will have different values for you.
{{% /notice %}}

![ec2 instance connect terminal emulator](pictures/ec2-instance-connect-terminal-emulator.png?classes=border)

### Getting Organized

The objective for this walkthrough is to deploy a static react application to an `EC2 instance`. Below you will find a list of items needed in order to accomplish this task:
1. `Build artificats of the react project`

{{% notice note %}}
The build artifacts for the react project are located within this github repository: `https://github.com/LaunchCodeTechnicalTraining/react-tic-tac-toe-build-artifacts.git`
{{% /notice %}}

2. `Web Server to deploy application`: This walkthrough will utilize `Caddy` as the web server.


### Clone the Build Artifacts

Run the following command:

![react-tic-tac-toe build artifacts](pictures/react-build-artifacts.png?classes=border)

```bash
git clone https://github.com/LaunchCodeTechnicalTraining/react-tic-tac-toe-build-artifacts.git
```

### Caddy Installation

```bash
sudo apt update -y

sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https

curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg

curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list

sudo apt update -y

sudo apt install caddy -y
```

#### Caddy Install Validation

To verify that you have installed caddy run the following command:

![verify caddy installation](pictures/which-caddy.png?classes=border)

```bash
which caddy
```

### Standing up Static React Website

Now that you have a web server installed on your server in addition to the build artifacts you are ready to stand the application up.

The default Caddyfile is located in the following location: `/etc/caddy/Caddfile`.

#### Editing the Caddy Config File

You will need to edit the file as a sudo user and add the following content:

{{% notice note %}}
This walkthrough will be using Vim to edit files. If you are unfamiliar with Vim you can learn more in our Linux Curriculum located here: `https://launchcodetechnicaltraining.org/linux/userspace-applications/walkthrough/vim/`.
{{% /notice %}}

![caddy config file ](pictures/caddy-config-file.png?classes=border)

```bash
sudo vim /etc/caddy/Caddyfile
```



