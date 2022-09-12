---
title: "AWS Account Creation"
date: 2022-05-04T13:43:26-05:00
draft: false
weight: 100
---

## AWS Account Creation Steps
The following information  is meant to serve as a guide to create a new AWS account using all of the free options. 

{{% notice note %}}
Please note that you will need to provide a valid credit card while creating your AWS Account. You will not be immediately charged with any fees. This course will utilize all available free-tiers on the platform so that you accrue the absolute minimum amount possible.
{{% /notice %}}

There will also be an introduction to the billing section of the AWS platform that provides you with all of the information on any costs that you would have under the account.

Please click the following link to **[Create your AWS Account](https://aws.amazon.com/free)**

{{% notice warning %}}
If you already have an AWS Account you do not need to create a new one!
{{% /notice %}}

![Free Account View Page](pictures/aws-amazon-free.png?classes=border)

Click on the `Create a Free Account` button.

### AWS Email and Account name

![AWS Account Creation page](pictures/aws-account-creation-homepage.png?classes=border)

You will need to provide a `Root user email address` and an `AWS account name`.

### Account Verification

After providing the `Root user email address` and `AWS account name` you will need to verify the email.

![Email validation](pictures/email-validation.png?classes=border)

Provide the verification code sent to your email.

### Root user password

After providing the verification code you will need to create a `Root user password` for the account. 

![Root user password view](pictures/root-user-password.png?classes=border)

{{% notice note %}}
This password will be used for the `root` user of the `AWS account`. Any users added to the `AWS` account through `IAM` roles will have their own `username` and `password`. 

If you would like to learn more about `IAM` roles you can read the documentation here:
[AWS IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)
{{% /notice %}}

### Contact Information

You will now need to provide your contact information.

You have the option to select a `Business` or `Personal` account. You will be using this as a `Personal` account.

{{% notice "red" warning%}}
Make sure to select `Personal` for the account type!
{{% /notice %}}

![AWS Account Contact Information](pictures/contact-information.png?classes=border)

After filling in the required information you will need to select agree to the terms of the `AWS Customer Agreement`

### Billing Information

{{% notice "red" Warning %}}
Please note that it states the following when completing the billing page:

"We will not charge you for usage below AWS Free Tier limits. We may temporarily hold up to $1 USD (or an equivalent amount in local currency) as a pending transaction for 3-5 days to verify your identity."
{{% /notice %}}

![AWS Account Billing Information](pictures/billing-information.png?classes=border)

You do need to provide a Credit or Debit card to complete the billing stage.

### Confirm Identity

To confirm the identity of the account you will need to verify using `Text  Message (SMS)` or a `Voice call`.

![AWS Account Confirm Identity](pictures/confirm-identity.png?classes=border)

If you have chosen the `SMS` option you will need to click the `Send SMS` button to move forward to the next step.

#### SMS Verification

![SMS Verification View](pictures/sms-verification.png?classes=border)

Provide the `SMS` verification code

### Support Plan

Once you have provided the last verification you will need to select the `Support plan`

You will be using the `Basic support - Free` plan.

![AWS Account Support Plan](pictures/support-plan.png?classes=border)

Click on the `Complete sign up` button.

### Setup Complete

Once your setup is complete you will receive a notification.

![AWS Account Setup Complete](pictures/setup-complete.png?classes=border)

Feel free to click on the `Go to the AWS Management Console` button to login.

### Root User Login

To log in to the AWS account you will need to provide the root user email address and password you created earlier in this walkthrough.

![AWS Account Login Prompt](pictures/login-prompt.png?classes=border)

After logging in to your your new `AWS` account you should see a view similar to the following screenshot:

![AWS Console Homepage](pictures/console-homepage.png?classes=border)
