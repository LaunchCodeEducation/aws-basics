---
title: "Access your EC2"
date: 2022-05-04T14:45:47-05:00
draft: false
weight: 105
---

## Accesssing Your EC2

### Successful Launch

Now that you have successfully launched an EC2 Instance you can view the instances dashboard.

![successful-launch](pictures/successful-launch.png?classes=border)

Click on the `view all instances` button.

### EC2 Instances View

This view will show you all instances within the aws account. Once the EC2 has passed all status checks you should see that the instance state is `Running`

![instances-view](pictures/instances-view.png?classes=border)

Click on the `Instance ID` underneath the `Instance ID` section. in the above image the `Instance ID` is `i-024d607e6b85c24df`.

### Instance Summary View

Once you have navigated into the `Instance Summary` view you will see a variety of details. Some important things to note:
- `Public IPv4 address`
- `Instance ID`
- `VPC ID`
- `Subnet ID`

![instance-dashboard](pictures/instance-dashboard.png?classes=border)

This page has the information you would need in order to connect to the instance via `SSH` or by clicking on the `Connect` button.

Click on the `Connect` button to connect to the server.

### Connecting to your Instance

One of the newer AWS features is the ability to connect to your server through the browser using `EC2 Instance Connect`.

You will be connecting to the server using the following:
- `Instance ID`
- `Public IP address`
- `User name`

![connect-to-instance](pictures/connect-to-instance.png?classes=border)

Within the `EC2 Instance Connect` tab click on the `Connect` button.

### Terminal Emulator

After clicking the connect button your browser will open a new tab and start a new terminal emulator. You should see something similar to the below image:

![browser-connect](pictures/browser-connect.png?classes=border)
