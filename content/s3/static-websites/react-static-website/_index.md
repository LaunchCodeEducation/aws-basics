---
title: "React Static Website"
date: 2022-05-04T13:43:26-05:00
draft: false
weight: 100
---

## React S3 Static Website Walkthrough

### Uploading Content

In order to host a static website you will need to upload the folder containing the build artifacts for the application.

{{% notice note %}}
The build artifacts you will be using for this static website are located within this github repository: `https://github.com/LaunchCodeTechnicalTraining/react-tic-tac-toe-build-artifacts`
{{% /notice %}}

You will need to clone the above build artifacts to your machine so that you can upload them to your newly created bucket.

Once you have cloned the build artifacts click on the `Upload` button within the console.

![My First Bucket View](pictures/first-bucket-view.png?classes=border)

### Upload Content View

In this walkthrough you will be uploading the cloned folder containing the build artifacts.

Click on the `Add Folder` button.

![Upload Content View](pictures/upload-view.png?classes=border)

{{% notice note %}}
Once you click on the `Add Folder` button you will need to navigate your file explorer to the location containing your cloned directory. After you have selected the proper directory you will see that the `Files and folders` section has been populated with that directories cotent.
{{% /notice %}}

![Uploaded Files View](pictures/uploaded-files-view.png?classes=border)

Once you have added the folder to be uploaded, scroll to the bottom of the page and click the `Upload` button.

### Validation

Upon uploading the folder to your `S3` bucket you should see a notification that lets you know the upload was successful.

![Uploaded React Build Artifacts Complete](pictures/upload-react-artifacts.png?classes=border)

Click on the `Close` button located near the top right corner of your screen. This will take you back to your bucket dashboard.

You should see that the `react-tic-tac-toe-build-artifacts` is located within the `Objects` tab of your bucket.

![Content Successfully uploaded](pictures/first-bucket-view-with-content.png?classes=border)

Click on the `react-tic-tac-toe-build-artifacts` folder to take a look at what is inside.
