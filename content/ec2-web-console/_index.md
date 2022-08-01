---
title: "Elastic Compute Cloud"
date: 2022-05-04T14:45:47-05:00
draft: false
weight: 105
---

## Notes for EC2 Console

One EC2 - needs access to internet

ipv4 CIDR block is for internal network:
- 10.0.0.0/16 - transient default
Availability zones:
- where does the project live?
Public subnet:
- need at least 1
Number of private subnets:
- could say 0 and only use public, this means there is no internal network connecting resources
- resources that dont need to be public should not be public
- architecture - 1 ec2
ssh 0 instead of anywhere whitelisted for only my ip address


## Content Links

{{% children %}}
