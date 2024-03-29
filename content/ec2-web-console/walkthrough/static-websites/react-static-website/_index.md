---
title: "React Static Website"
date: 2022-05-04T13:45:41-05:00
draft: false
weight: 100
---

## AWS EC2 React Static Website

Now you are ready to deploy a static website to a brand new EC2 instance. Let's begin by creating a brand new EC2. Below you will find the appropriate settings for this walkthrough.

### EC2 Settings

1. Name: "first-static-website"
1. Machine Image: "Ubuntu 22.04 LTS"
1. Instance Type: "t2.micro"
1. Key Pair: "first-key-pair"
1. Security Group: "Create Security Group"
	1. Allow SSH Traffic from Anywhere
	1. Allow HTTPs traffic from the internet
	1. Allow HTTP Traffic from the internet
1. Storage: Default

Once you have all of the above options selected you are ready to launch your EC2 instance.

### Validation

Click the *Launch Instance* button.

![first-static-website on ec2 dashboard](pictures/first-static-website.png?classes=border)

Click on the *Instance ID* to view the summary page for the new EC2 instance.

![first-static-website summary](pictures/first-static-website-summary.png?classes=border)

### Connect to the Instance

![connect-to-instance-image](pictures/first-static-website-summary.png?classes=border)

Click on the *Connect* button.

### EC2 Instance Connect

![ec2-instance-connect-view](pictures/ec2-instance-connect.png?classes=border)

Within the *EC2 Instance Connect* menu, click on the *Connect* button.

{{% notice blue "Note" "rocket" %}}
The `Instance ID` and the `Public IP Address` will have different values for you.
{{% /notice %}}

Now the terminal will launch and you can begin your work!

![ec2 instance connect terminal emulator](pictures/ec2-instance-connect-terminal-emulator.png?classes=border)

### Getting Organized

The objective for this walkthrough is to deploy a static React application to an EC2 instance. Below you will find a list of items needed in order to accomplish this task:

1. Build artifacts of the React project. The build artifacts for the react project are located within this [Github repository](https://github.com/LaunchCodeTechnicalTraining/react-tic-tac-toe-build-artifacts.git).
1. Web Server to deploy application. This walkthrough will utilize Caddy as the web server.


### Clone the Build Artifacts

Run the following command:

```bash
git clone https://github.com/LaunchCodeTechnicalTraining/react-tic-tac-toe-build-artifacts.git
```

### Caddy Installation

To install Caddy, run the following bash commands in the order they are presented in this text.

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

```bash
which caddy
```

The output of this command should something similar to `/usr/bin/caddy`.

### Standing up Static React Website

Now that you have a web server installed on your server in addition to the build artifacts you are ready to stand the application up.

The default Caddyfile is located in the following location: `/etc/caddy/Caddfile`.

#### Editing the Caddy Config File

You will need to edit the file as a sudo user and add the following content:

{{% notice blue "Note" "rocket" %}}
This walkthrough will be using Vim to edit files. If you are unfamiliar with Vim you can learn more in our Linux Curriculum located here: `https://launchcodetechnicaltraining.org/linux/userspace-applications/walkthrough/vim/`.
{{% /notice %}}

{{% notice blue "Note" "rocket" %}}
The default Caddyfile will already have text inside. You should see the file with the following information:
![default caddyfile text](pictures/default-caddyfile-view.png?classes=border)
Feel free to remove all of the information inside of this file. It is simply there as an example.
{{% /notice %}}

You will need to edit the file as a sudo user and add the following content:

```bash
sudo vim /etc/caddy/Caddyfile
```

![caddy config file ](pictures/caddy-config-file.png?classes=border)

{{% notice blue "Note" "rocket" %}}
In the above image you will need to replace the ip address `184.72.82.98` with your EC2 Instances IPV4 Public IP Address. The above address is specific to the machine used for this walkthrough.
{{% /notice %}}

In addition to the above you are also specifying that you will be using `HTTP` because you do not have a DNS attached to the IP address. Since Caddy runs `HTTPS` by default this is a required addition to the file.

You are also pointing to the directory holding the build artifacts for the react project and using the file_server annotation to serve the files.

{{% notice warning %}}
You will also need to reload your caddy file after the above changes have been made. There are a couple of ways to accomplish this:

While inside the `/etc/caddy/` directory:
```bash
sudo caddy reload
```

From anywhere:
```bash
sudo caddy reload --config /etc/caddy/Caddfile
```
{{% /notice %}}

### Validation

After completing the above steps you should be able to access the application running on your public IPV4 address while specifying http.

Navigate a new private browser window to `http://your-public-ipv4-address`

![running react application in browser](pictures/react-app-browser.png?classes=border)

#### Troubleshooting

If you are having issues accessing the application in your browser it very well could be a permissions issue. You will find a couple of fixes below that may help you.

1. Run the following commands:
```bash
sudo systemctl stop caddy
```

```bash
sudo caddy start
```

Within your `/etc/caddy/` directory:
```bash
sudo caddy reload
```
{{% notice blue "Note" "rocket" %}}
I have found that caddy is started and managed automatically by systemctl and if your project directory is in a location with incorrect permissions this can cause issues. Once you run all the commands as the same user it usually fixes the issues of caddy being able to access the project direcrory.
{{% /notice %}}



