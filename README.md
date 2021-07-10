# post-lambda-sample

This is a simple example of how to build and deploy a static website that sends a POST request to an AWS service.

What we'll do:
1. Create a static website hosted on AWS S3
2. Create a CloudFormation configuration to deploy a lambda
3. Add a button to our website that calls the lambda
4. Create a CI/CD pipeline that deploys both the website and the lambda when new code is submitted.

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

Let's use AWS for everything, this keeps things simple and free.  You don't have to use AWS for everything, you can host your static website on Netlify for example, everything will still work.  So let's start with using AWS to host your static website. How to host a static website on AWS S3 can be found [here](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html).  Feel free to book mark that site so you can read it later and skip to 'Create an S3 Instance' below.

### Configuring a static website on Amazon S3

Navigate to [Tutorial: Configuring a static website on Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html#step2-create-bucket-config-as-website) and follow the instructions to create a static website hosted on AWS S3.

Use the index.html and error.html pages provided in this git repository. We can add your website once we have authentication and HTTPS supported.


