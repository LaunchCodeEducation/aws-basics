---
title: "EC2 Static Website CLI Outline"
date: 2022-05-04T13:45:41-05:00
draft: false
weight: 115
---

## AWS EC2 Notes

### Information needed to create a new EC2

- `image AMI` = ami-09d56f8956ab235b3
- `instante type` = (t2.micro)
- `count` = 1
- `SSH Key Pair` = MyKeyPair
- `VPC ID` = vpc-db768aa6
- `Subnet ID` = subnet-46ab0719
- `Security ID` = sg-024730b92b8c9258e 

Complete command to create new EC2 Instance:

```bash
aws ec2 run-instances --image-id ami-xxxxxxxx --count 1 --instance-type t2.micro --key-name MyKeyPair --security-group-ids sg-903004f8 --subnet-id subnet-6e7f829e
```

{{% notice note %}}
All of the IDs are from this specific example: [EC2-VPC section](https://docs.aws.amazon.com/cli/latest/userguide/cli-services-ec2-instances.html)
{{% /notice %}}

## Finding the `--image-id` AMI

`--image-id ami-xxxxxxxx`: Navigated to web console [located here](https://us-east-1.console.aws.amazon.com/ec2/v2/home?region=us-east-1#LaunchInstances:) and looked up `Ubuntu 22.04`: `ami-09d56f8956ab235b3` (64-bit (x86) option)

{{% notice note %}}
`--count`: How many instances to create

`--instance-type`: Processor of the server
{{% /notice %}}

## Finding the `--key-name`

If you already have a public key you can provide the key instead of creating a new one.

### Creating a New Key Pair if Necessary

To create a new key-pair using the AWS CLI:

```bash
aws ec2 create-key-pair --key-name MyKeyPair --query 'KeyMaterial' --output text > MyKeyPair.pem
```

{{% notice note %}}
You can replace "MyKeyPair" with the desired key name. This will be stored on the ec2 web console page as the public key for the instance. Also rename "MyKeyPair.pem" to the desired pem file name on your local machine. This is your private key. The permissions need to be 400 for the local key file.

`https://us-east-1.console.aws.amazon.com/ec2/v2/home?region=us-east-1#KeyPairs:`
{{% /notice %}}

## Find VPC Id

For this POC we used the default PVC provided by AWS. Located here: `https://us-east-1.console.aws.amazon.com/vpc/home?region=us-east-1#vpcs:VpcId=vpc-db768aa6`

{{% notice note %}}
We still need to explore creating a VPC using the CLI:

[AWS-VPC-CLI Docs](https://docs.aws.amazon.com/cli/latest/reference/ec2/create-vpc.html)
{{% /notice %}}

## Find Subnet Id

To find the subnets available for each VPC: `https://us-east-1.console.aws.amazon.com/vpc/home?region=us-east-1#subnets:`

<!-- `Provide subnet id`
subnet id = subnet-46ab0719
--subnet-id subnet-6e7f829e -->

## Find the Security Group Id

If you already have a previously created security group you can provide the id which is located here: `https://us-east-1.console.aws.amazon.com/ec2/v2/home?region=us-east-1#SecurityGroups:`

### Create new Security Group if Necessary

To create a new security group using the CLI you can run the following command:

```bash
aws ec2 create-security-group --group-name my-sg --description "My security group" --vpc-id vpc-1a2b3c4d
```

Command we executed:
```bash
aws ec2 create-security-group --group-name New-Group-Name  --description "New Security Group" --vpc-id vpc-db768aa6
```

## Add New Policy to Existing Security Group

aws ec2 authorize-security-group-ingress --group-id sg-903004f8 --protocol tcp --port 3389 --cidr x.x.x.x

Command we executed:
```bash
aws ec2 authorize-security-group-ingress --group-id sg-903004f8 --protocol ssh --port 22 --cidr $(curl ipinfo.io/ip)
```

## Connect to machine:
- `ssh -i .pem-file ubuntu@server-address`

## Content Links

{{% children %}}
