---
title: "Accessing Your S3 Bucket"
date: 2022-05-04T13:43:26-05:00
draft: false
weight: 105
---

## Accessing Your New S3 Bucket

Now that you have created an S3 Bucket, you will want to access the resource.


### S3 Bucket Dashboard

Navigate to the Amazon S3 Dashboard to view your existing buckets.

![Amazon S3 Dashboard Overview](pictures/existing-buckets-view.png?classes=border)

Click on the name of your newly created bucket. The bucket I created is named `my-first-bucket-john`.

{{% notice note %}}
This AWS Account also has an already existing bucket named `launchcode-blog-images`. You will only see the bucket you created in the previous walkthrough unless you have explored and utilized the `S3` resource in the past!
{{% /notice %}}

### Individual Bucket Dashboard

Once you are viewing your newly created bucket, you will notice there are multiple tabs available.

- `Objects`: View for all existing objects within the bucket
- `Properties`: Various settings available for the bucket
- `Permissions`: Permissions for viewing the objects within the bucket (Public Access), any bucket policies, object ownership, and an ACL (Access Control List)
- `Metrics`: Data and Usage for the S3 Bucket
- `Management`: Lifecycle rules for objects within the bucket
- `Access Points`: Manage the access points for the bucket

![First Bucket Dashboard](pictures/first-bucket-view.png?classes=border)

Now that you have a general understanding of how and where to access your bucket you are now ready to add a folder containing the build artifacts for a static website.