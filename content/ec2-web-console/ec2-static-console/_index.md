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

### Getting Organized

The objective for this walkthrough is to deploy a static react application to an ec2 instance. Below you will find a list of items needed in order to accomplish this task:
- `Build artificats of the react project`
- `Web Server to deploy application`

### Connect to the Instance

![connect-to-instance-image](pictures/first-static-website-summary.png?classes=border)

Click on the `Connect` button.

### EC2 Instance Connect

![ec2-instance-connect-view](pictures/ec2-instance-connect.png?classes=border)

Within the `EC2 Instance Connect` click on the `Connect` button.

{{% notice note %}}
The `Instance ID` and the `Public IP Address` will have different values for you.
{{% /notice %}}
