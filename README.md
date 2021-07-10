# post-lambda-sample

This is a simple example of how to build and deploy a static website that sends a POST request to an AWS service.

## Configuration

If you haven't already, you need to create a free [AWS account](https://portal.aws.amazon.com/billing/signup?refid=em_127222&redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start).

Note: this tutorial will use the AWS free tier; however, I always recommend you create a [budget](https://console.aws.amazon.com/billing/home?#/budgets) as a guardrail.  For development, I typically set my budget to $25.00/month and have an alert send me an email if I go over the 80% threshold.

## Setup

### Clone this repository

First, if you haven't downloaded the git CLI, follow these [instructions](https://git-scm.com/download/mac) (change to /win if you are on a windows computer).  Once you've downloaded git CLI, open a terminal and type git --version to confirm it is installed correctly.  You should see something like, version 2.30.1 (Apple Git-130).

In the terminal, navigate to > cd /Documents/Development and type > nkdir post-lamnda-sample then navigate into your newly created folder > cd post-lamda-sample.

Next, within the terminal window navigate to your desired development folder and and type, > git clone https://github.com/beaton/post-lambda-sample.git to clone this repo to your local folder.

At this point you will have a clone of this repository in your /Documents/Development/post-lamda-sample directory.

## Static website

Let's use AWS for everything, this keeps things simple and free.  So let's start with using AWS to host your static website. How to host a static website on AWS S3 can be found [here](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html).  Feel free to book mark that site so you can read it later and skip to 'Create an S3 Instance' below.

### Create an S3 instance 

1. Navigate to [S3](https://s3.console.aws.amazon.com/s3/home?region=us-east-1#) and click the 'create bucket' button in the upper right.
2. Click "Create Bucket" orange button.
3. Give your bucket a name.
4. Choose a region (I usually choose us-east-1 because that's my timezone)
5. Choose "Block all public access." We'll modify this in the next section.
6. The remaining setting defaults are fine.
7. Click the orange "create bucket" at the bottom.

You should now see your bucket in the [AWS S3 Console](https://s3.console.aws.amazon.com/s3/)

### Grant read access to your S3 Bucket so users can access your website

https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteAccessPermissionsReqd.html

1. Open the Amazon S3 console at [AWS S3 Console](https://s3.console.aws.amazon.com/s3/).
2. Choose the name of the bucket that you have configured as a static website.
3. Choose Permissions tab.
4. Under Block public access (bucket settings), choose Edit.
5. Clear Block all public access, and choose Save changes.

### Add a bucket policy

This step allows the public to access your website files through HTTP.  Later we'll add CloudFront and enable HTTPS for added security.

1. Under Buckets, choose the name of your bucket.
2. Choose Permissions tab.
3. Under Bucket Policy, choose Edit.
4. To grant public read access for your website, copy the following bucket policy, and paste it in the Bucket policy editor.

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

5. Replace "Bucket-Name" with your S3 bucket name.
6. Choose Save changes.

### Upload your website

1. Open the Amazon S3 console at [AWS S3 Console](https://s3.console.aws.amazon.com/s3/).
2. Select your new S3 bucket, click the upload button and add /Documents/Development/post-lamda-sample/home.html.
3. Click upload (this small file will upload quickly)
4. Now that home.html has been uploaded, click on it to open a details view. Copy the 'Object URL' and paste it into a new browser tab.  You should see "Hello World" displayed in the browser... if not, stop, go back and walk through the steps again.

Great, you've uploaded Hello World! Take a break.  Next we'll look at adding CloudFront to support HTTPS and add user authentication so only registered users can access your website. THEN you can add your website to this bucket (don't do that yet).


