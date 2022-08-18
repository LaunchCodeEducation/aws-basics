---
title: "First S3 Bucket"
date: 2022-05-04T13:43:26-05:00
draft: false
weight: 100
---

## Creating Your First S3 Bucket

In order to create an S3 Bucket you will need to provide the following:
- `Bucket Name`: This name must be unique. If there is an existing bucket with the desired name you will not be able to create the bucket.
- `Object Ownership`:
- `Public Access`: Public access is blocked by default. This behavior can be changed.
- `Bucket Versioning`:
- `Encryption`:

### Bucket Name
For your first bucket you will only need to provide a unique name and leave all other options as they have been defaulted.

![first-bucket-view](pictures/first-bucket-view.png?classes=border)

The name I used  while creating the bucket is `my-first-bucket-john`.

### Public Access

![allow-public-access-s3](pictures/allow-public-access-s3.png?classes=border)

For the following walkthroughs you will need public access to be enabled for the s3 buckets. The goal is to host a static webiste and you will notice in order to do so public access cannot be blocked.

### Tags

You do not need to add a tag for this walkthrough, and the `Default Encryption` should be disabled.

![tags-encryption-advanced](pictures/tags-encryption-advanced.png?classes=border)

After you have completed the above steps hit the `Create Bucket` button.
