---
title: "First EC2 Instance"
date: 2022-05-04T14:45:47-05:00
draft: false
weight: 100
---

## Launching Your First Instance

Now that you are ready to launch your first instance there will be some options for us to select. The options we will be focusing on are as follows:

1. Name of instance
1. Amazon Machine Image or AMI
1. Instance type
1. Key Pair
1. Security Group

![first-instance-view](pictures/first-ec2-launch.png?classes=border)

### Name and AMI

The first step is to provide your new EC2 instance with a name and select an AMI.

![Name and AMI of EC2](pictures/name-and-AMI.png?classes=border)

For your first EC2 instance, you should provide the name, `my-first-instance`.

From the quick start menu, select `Ubuntu` with the newest `22.04 LTS` as the version.

### Instance Type

Next you will select the type of instance for your image.

![Type of Instance](pictures/instance-type.png?classes=border)

For this walkthrough, you will be using the t2.micro which is eligible for the free tier.

### SSH Key Pair

In order to access our machine through the terminal you will need to provide an ssh key pair. Since this is your first time launching a new instance you will be creating a new key pair value.

![Key Pair Selection](pictures/key-pair.png?classes=border)

Click on the *Create new key pair* button.

### Creating a new SSH Key Pair

In the subsequent menu, provide the name `first-key-pair`. You will be leaving the Key pair type as `RSA` and the file format as a `.pem` file.

![New Key Pair Name](pictures/first-key-pair.png?classes=border)

{{% notice blue "Note" "rocket" %}}
After you click *Create key pair*, it will download a new file to your machine called `first-key-pair.pem`. You will need access to this file in order to ssh into your new machine in the future. So make sure you know where it is located!
{{% /notice %}}

Click the *Create key pair* button.

### Network Settings

![Network Settings Section](pictures/network-settings.png?classes=border)

Your network settings should allow SSH traffic from anywhere.

### Storage

![Storage Settings Section](pictures/storage-section.png?classes=border)

When you check the storage, you should have 8 GB.