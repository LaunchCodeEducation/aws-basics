---
title: "S3"
date: 2022-05-04T13:43:26-05:00
draft: false
weight: 115
---

## Introduction

The AWS S3 resource is primarily used to store objects. The service offers scalability, data availability, security, and high performance.

## Notes from POC

### Create an AWS Account

### Install AWS CLI
- Configure with secret key and access
- Use default for region and *

### Make new s3 bucket
- aws s3 mb bucket-name

### Add build artificats / static web resources
- aws s3 cp target-file-local-file-or-directory s3://target-s3-bucket --acl "public-read"

### Configure static website
- aws s3 website s3://bucket-name --index-document index.html

### Find bucket https://location via console


## Content Links

{{% children %}}
