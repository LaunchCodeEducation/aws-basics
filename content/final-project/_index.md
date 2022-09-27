---
title: "Final Project"
date: 2022-05-04T14:45:47-05:00
draft: false
weight: 150
---

## Recap

This `AWS` intro course has covered two of the most commonly used `AWS Resources`:
- Amazon S3
    - Static Websites
        - React
        - Angular
- Amazon EC2
    - Static Websites
        - React
        - Angular
    - Reverse Proxy
        - Java/Spring Application
        - C#/ASP.NET Application

At this point you have learned how to deploy the above applications using the `S3` and `EC2` resource. Taking things a step further you will do the following:
1. Deploy a Persistent `Java/Spring` Application to a new `EC2` instance.
    - Utilize a `docker` container that will be running `MySQL` for your database
    - Connect the running application to the `docker` container with `environment variables`
    - Reverse Proxy the `HTTP` requests to the running server
1. Script all of the above with a `Bash` script.

{{% children %}}
