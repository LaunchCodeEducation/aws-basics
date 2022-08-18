---
title: "React Static Website"
date: 2022-05-04T13:43:26-05:00
draft: false
weight: 100
---

## React S3 Static Website Walkthrough

### Uploading Content

{{% notice note %}}
This walkthrough will be using the bucket you created during the `First S3 Bucket` and `Accessing Your S3 Bucket` walkthroughs.
{{% /notice %}}

In order to host a static website you will need to upload the folder containing the build artifacts for the application.

{{% notice note %}}
The build artifacts you will be using for this static website are located within this github repository: `https://github.com/LaunchCodeTechnicalTraining/react-tic-tac-toe-build-artifacts`
{{% /notice %}}

You will need to clone the above build artifacts to your machine so that you can upload them to your newly created bucket.

Once you have cloned the build artifacts click on the `Upload` button within the console.

![My First Bucket View](pictures/first-bucket-view.png?classes=border)

### Upload Content View

You will be uploading the build artifacts that you cloned earlier in this walkthrough.

![Upload Content View](pictures/upload-view.png?classes=border)

{{% notice "green" Bonus %}}
There are multiple ways that you can upload the build artifacts to this S3 bucket. I simply selected all files within the `react-tic-tac-toe-build-artifacts` folder to drag and drop them inside.
{{% /notice %}}

![Uploaded Files View](pictures/uploaded-files-view.png?classes=border)

Once you have added the files to be uploaded, scroll to the bottom of the page and click the `Upload` button.

### Validation

Upon uploading the build artifacts to your `S3` bucket you should see a notification that lets you know the upload was successful.

![Uploaded React Build Artifacts Complete](pictures/upload-react-artifacts.png?classes=border)

Click on the `Close` button located near the top right corner of your screen. This will take you back to your bucket dashboard.

You should see that the build artifacts are located within the `Objects` tab of your bucket.

![Content Successfully uploaded](pictures/first-bucket-view-with-content.png?classes=border)

All of the above files are a result of building a `React` project and taking what was inside of the `build` folder and storing them as build artifacts.

### Enable Static Website Hosting

Now that you have had a look at what is inside of the folder you will need to enable the option for Static Website Hosting within this bucket.

Navigate back to the main dashboard of your bucket and click the on `Properties` tab.

There are a lot of different properties within this tab. You are looking for the `Static Website Hosting` property.

![Properties Tab View](pictures/properties-tab-view.png?classes=border)

Scroll down within this view until you reach the `Static Website Hosting` property option.

![Static Website Hosting Option](pictures/static-website-hosting.png?classes=border)

Click on the `Edit` button.

![Edit Static Website Hosting View](pictures/edit-static-website-hosting.png?classes=border)

Click on the `Enable` option.

This will open up a new menu with the following options:

- `Hosting Type`: For this walkthrough you will be selecting `Host a static website` as the option.
- `Index Document`: The Index Document you will be using is `index.html` as seen earlier in this walkthrough.
- `Error Document`: This option you will leave as defaulted.
- `Redirection Rules`: This option you will leave as defaulted.

![Edit Static Website Hosting Expanded View](pictures/edit-static-website-expanded.png?classes=border)

After you have selected and filled in the correct values scroll to the bottom of the page and click the `Save Changes` button.

### Validation

After saving the above changes you should be able to scroll to the bottom of your `Properties` tab and see the changes reflected under the `Static Website Hosting` option.

![Static Website Hosting Options Saved](pictures/static-website-hosting-validation.png?classes=border)

You can also now see the endpoint for your static website. In the above screenshot the bucket endpoint is:
- `http://my-first-bucket-john.s3-website-us-east-1.amazonaws.com`

If you click on the link your browser should open up a new window with a working react static website.

![Working React Static S3 Website](pictures/react-website-in-browser.png?classes=border)

{{% notice note %}}
This link is publicly available to anyone. Feel free to share the link!
{{% /notice %}}