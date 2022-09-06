---
title: "EC2 Load Balancer"
date: 2022-05-04T14:45:47-05:00
draft: false
hidden: true
weight: 150
---


## Load Balancer 
Handling traffic and sending it to the appropriate location based on volume.
- EC2 taking amount of load and spinning up targets in the target group. How many do we have, whos requests are we sending to? This makes it so that none of our ec2s crash.
- 1 load balancer, ingress points, autoscales the target group, sometimes you will have multiple autoscaling groups.
- 3 squares. The VPC, the autoscaling group, and the target group
- How to define a target, target group, auto scaling group, load balancer inside of a target group, how to configure the load balancer? How to set the load? How much is too much?

New VPC Created:

Load Balancing:
- Load Balancers
- Target Groups
Auto Scaling
- Launch Configs
- Auto Scaling Groups

Internal: Private
Internet-Facing: Public

## VPC 
First to be (created), entire network where everything is living. Made up of subnets both public and private

## Target Group
Everything that gets launched is going to live inside of the target group. Only the EC2s that get created, part of the autoscaling group, managed by the load balancer

## Launch Template 
Template with specifics about the EC2 Instance. What type of instance or machine are we letting AWS know we want to create?

## Load Balancer 
Using an EC2 as our load balancer, server whos responsibility is to check the health of everything in the target group, Scaling up and down, proxying internet requests to those machines.

## AutoScaling Group
(Last Thing to Be created). Collection of the load balancer (brain), target group (nodes), Launch Template (what will each node become), VPC (holds all of this).

