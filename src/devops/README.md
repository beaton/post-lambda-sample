# post-lambda-sample CloudFormation

This is a simple example of how to build and deploy a static website that sends a POST request to an AWS service.

If you do not already know about AWS [CloudFormation](https://aws.amazon.com/cloudformation/), it's a configuration file (.json or .yaml formatted) that describes your deployment environment and all your required resources.  It is a consistent, predictable and repeatable way to deploy and redeploy your resources across multiple environments programmatically.

This document describes how to use the cloudformation.json file in this folder to deploy all the necessary AWS Services to support this project:

1. AWS S3 and AWS CloudFront for hosting a static website.
1. AWS API Gateway and a simple lambda function that accepts a POST request from the client and returns the users IP address in plain text.

## Setup

### Clone this repository

You should have already cloned the parent directory and all sub-directories.

### Configure 

When deploying the cloudformation configuration, the user will be prompted to enter values for the "Parameters" defined cloudformation.json. I suggest you use the default values until you are familiar with what each parameter is doing in the deployment. 

Within the cloudformation.json file, the "Resources" section defines what AWS resources will be deployed, 

1. [apiGateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html) - a secure server-side API that controls access to the lambda.
1. [lambdaFunction](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) - the python function that executes the HTTP POST request.
1. [lambdaIAMRole](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) - an AWS IAM user role that has access to the lambda function from the API Gateway.
1. [lambdaLogGroup]() - AWS CloudWatch log service that records log output of the lambda service.

NOTE: CloudWatch is a necessary service but it can be a very expensive part of any AWS deployment, continually watch your CloudWatch costs carefully as they add up! I set the log retention to 5-days (see cloudformation.json) which may not be enough in a production environment.

Note: Although I have not supported it here, the API Gateway can both authenticate a user and validate the POST request body.

The "Outputs" section of the cloudformation.json is the result of executing the cloudformation configuration. In our case we output the public URL required to call the API Gateway and the ARN, which helps identify the lambda that was created.

### Run

TBD


