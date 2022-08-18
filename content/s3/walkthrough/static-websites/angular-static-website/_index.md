---
title: "Angular Static Website"
date: 2022-05-04T13:43:26-05:00
draft: false
weight: 105
---

## Angular S3 Static Website Walkthrough

### Getting Organized

Begin by creating a new S3 Bucket with the following settings:
- `Bucket Name`: orbit-report-static-s3-[insert random number]
- `AWS Region`: default region
- `Object Ownership`: ACLs disabled
- `Public Access Settings`: All Public Access Allowed
- `Bucket Versioning`: Disable
- `Tags`: None
- `Default Encryption`: Disable
- `Advanced Settings`: None

Once you have the above settings correct, click the `Create bucket` button.

![Angular Static Website Bucket Created](pictures/orbit-report-static-s3-1.png?classes=border)

Click on the name of your newly created bucket to view its dashboard.

### Cloning Build Artifacts

In order to host a static website you will need to upload the build artifacts for the application.

{{% notice note %}}
The build artifacts you will be using for this static website are located within this github repository: `https://github.com/LaunchCodeTechnicalTraining/orbit-report-artifacts`
{{% /notice %}}

You will need to clone the above build artifacts to your machine so that you can upload them to your newly created bucket.


### Uploading Build Artifacts

Once you have cloned the build artifacts click on the `Upload` button within the console.

![Upload Button On New Bucket](pictures/orbit-report-static-s3-dashboard.png?classes=border)

You will be uploading the build artifacts that you cloned earlier in this walkthrough.

![Upload Angular Build Artifacts View](pictures/upload-build-artifacts.png?classes=border)

{{% notice "green" Bonus %}}
There are multiple ways that you can upload the build artifacts to this S3 bucket. I simply selected all files within the `orbit-report-artifacts` folder to drag and drop them inside.
{{% /notice %}}

Once you have added the files to be uploaded, scroll to the bottom of the page and click the `Upload` button.

![Uploaded Files View](pictures/uploaded-files-view.png?classes=border)

### Validation

Upon uploading the build artifacts to your `S3` bucket you should see a notification that lets you know the upload was successful.

Click on the `Close` button located near the top right corner of your screen. This will take you back to your bucket dashboard.

You should see that the build artifacts are located within the `Objects` tab of your bucket.

![Content Successfully uploaded](pictures/orbit-report-bucket-with-content.png?classes=border)

All of the files you uploaded are a result of building an `Angular` project and taking what was inside of the `build` folder and storing them as build artifacts.

### Enable Static Website Hosting

Now that you have had a look at what is inside of the folder you will need to enable the option for Static Website Hosting within this bucket.

Navigate back to the main dashboard of your bucket and click the on `Properties` tab.

There are a lot of different properties within this tab. You are looking for the `Static Website Hosting` property.

Scroll down within this view until you reach the `Static Website Hosting` section.

![Static Website Hosting Option](pictures/static-website-hosting.png?classes=border)

Click on the `Edit` button.

![Edit Static Website Hosting View](pictures/edit-static-website-hosting.png?classes=border)

Click on the `Enable` option.

This will open up a new menu with the following options:

- `Hosting Type`: For this walkthrough you will be selecting `Host a static website` as the option.
- `Index Document`: The Index Document you will be using is `index.html` that you uploaded earlier in this walkthrough.
- `Error Document`: This option you will leave as defaulted.
- `Redirection Rules`: This option you will leave as defaulted.

![Edit Static Website Hosting Expanded View](pictures/edit-static-website-expanded.png?classes=border)

After you have selected and filled in the correct values scroll to the bottom of the page and click the `Save Changes` button.

### Validation

After saving the above changes you should be able to scroll to the bottom of your `Properties` tab and see the changes reflected under `Static Website Hosting`.

![Static Website Hosting Options Saved](pictures/static-website-hosting-validation.png?classes=border)

You can also now see the endpoint for your static website. In the above screenshot the bucket endpoint is:
- `http://my-first-bucket-john.s3-website-us-east-1.amazonaws.com`

If you click on the link your browser should open up a new window. You will most likely receive the following error on that new page:

![403 forbidden whitepage](pictures/403-forbidden-whitepage.png?classes=border)

This is there is no bucket policy attached to the `orbit-report-bucket`. You will need to attach a new bucket policy to this bucket in order to make the objects available to the public.

### Attaching Bucket Policy

Open up the `Permissions` tab within your S3 Bucket.

Navigate the permissions view until you come accross the `Bucket Policy` section as shown below:

![Permissions Tab of S3 Bucket](pictures/permissions-tab.png?classes=border)

Click on the `Edit` button.

This will open up a new view so that you are able to attach a policy to the bucket.

You will be using the bucket policy provided in this article: [AWS S3 Security Permissions Document](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteAccessPermissionsReqd.html)

You can find the raw json below:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": [
                "s3:GetObject"
            ],
            "Resource": [
                "arn:aws:s3:::Bucket-Name/*"
            ]
        }
    ]
}
```

Add the above `Policy` to the empty field as shown in the screenshot below, replacing `Bucket-Name` with the name of your bucket:

![Public Bucket Polcy S3 Bucket](pictures/attach-bucket-policy.png?classes=border)

{{% notice warning %}}
You will need to add the name of your bucket under the "Resource" section in order for the policy to work. Without a valid bucket name you will most likely receive an error if you try to save changes.
{{% /notice %}}

Click on the `Save changes` button.

### Validation

Now that you have attached a `Policy` to your bucket you should now be able to access your static website using the link found under the `Static Website` section under your `Properties` tab!

![Working Angular Static Website](pictures/angular-static-website-view.png?classes=border)

{{% notice note %}}
This link is publicly available to anyone. Feel free to share the link!
{{% /notice %}}
