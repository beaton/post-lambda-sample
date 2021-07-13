# post-lambda-sample Home

This is a simple example of how to build and deploy a static website that sends a POST request to an AWS service.

What we'll do:
1. Create a static website hosted on AWS S3
1. Create a CloudFormation configuration to deploy a lambda
1. Create a CI/CD pipeline that deploys both the website and the lambda when new code is submitted.

I've created this configuration for hosting application B2B user admin consoles and developer documentation. For example check out https://developer.youi.tv/, which is powered by [Jekyll](https://jekyllrb.com/).

## Configuration

If you haven't already, you need to create a free [AWS account](https://portal.aws.amazon.com/billing/signup?refid=em_127222&redirect_url=https%3A%2F%2Faws.amazon.com%2Fregistration-confirmation#/start).

Note: this tutorial will use the AWS free tier; however, I always recommend you create a [budget](https://console.aws.amazon.com/billing/home?#/budgets) as a guardrail.  For development, I typically set my budget to $25.00/month and have an alert send me an email if I go over the 80% threshold.

## Setup

### Clone this repository

First, if you haven't downloaded the git CLI, follow these [instructions](https://git-scm.com/download/mac) (change to /win if you are on a windows computer).  Once you've downloaded git CLI, open a terminal and type git --version to confirm it is installed correctly.  You should see something like, version 2.30.1 (Apple Git-130).

In the terminal, navigate to 

> cd /Documents/Development and type 
> mkdir post-lamnda-sample 
 
then navigate into your newly created folder 

> cd post-lamda-sample.

Next, within the terminal window navigate to your desired development folder and and type,

> git clone https://github.com/beaton/post-lambda-sample.git 

to clone this git repository to your local folder.

At this point you will have a clone of this repository in your /Documents/Development/post-lamda-sample directory and you can create a static website, a lambda serverless service and a build pipeline to build, test and deploy right from github.

## AWS S3 hosted Static website

Navigate to /src/web/ and follow the readme.md instructions to create a static website hosted on S3.

## AWS Lambda serverless function

Navigate to /src/server and follow the readme.md instructions to create a serverless lambda function to return hello world. 

## AWS CodePipeline CI/CD pipeline

Naviate to /src/devops and follow the readme.md instructions to create a code pipeline that will build and deploy your code right from github.
