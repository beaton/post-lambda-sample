# post-lambda-sample CloudFormation

This is a simple example of how use the [AWS CloudFormation Service](https://console.aws.amazon.com/cloudformation/) to build and deploy a serverless function.

If you do not already know about AWS [CloudFormation](https://aws.amazon.com/cloudformation/), it's an AWS Service that deploys your server environment through a configuration file (.json or .yml formatted). This configuration file describes your AWS runtime environment with all your defined resources.  It is a consistent, predictable and repeatable way to deploy and redeploy your resources across multiple environments programmatically and without human error.

Within the cloudformation.yml file, the "Resources" section defines what AWS resources will be deployed, 

1. [apiGateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html) - a secure server-side API that controls access to the lambda.
1. [lambdaFunction](https://docs.aws.amazon.com/lambda/latest/dg/welcome.html) - the python function that executes the HTTP POST request.
1. [lambdaIAMRole](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html) - an AWS IAM user role that has access to the lambda function from the API Gateway.
1. [lambdaLogGroup]() - AWS CloudWatch log service that records log output of the lambda service.

The "Outputs" section of the cloudformation.yml is the result of executing the cloudformation configuration. In our case we output the public URL required to call the API Gateway and the ARN, which helps identify the lambda that was created.

## Setup

### Clone this repository

You should have already cloned the parent directory and all sub-directories.

### Run

To deploy your serverless environment,

1. Navigate to [AWS CloudFormation Service](https://console.aws.amazon.com/cloudformation/)
2. Be sure to select the 'N. Virginia' region in the upper right corner drop-down so you will be deploying to us-east-1.
3. Choose 'Create Stack' and 'With new resources (standard)'
4. In the Create Stack Step, choose 'Template is ready' and 'Upload a template file' (this is cloudformation.yml)
5. Select 'Choose file' and search for and select the cloudformation.yml file in this folder.
6. Select 'Next'
7. In Step 2, enter a Stack Name (can be anything), 'post-lambda-sample'
8. Select 'Next'
9. In step 3, accept all the defaults and select 'Next'
10. In step 4, under capabilities, read the info and acknowledge the need to create additional [IAM roles](https://console.aws.amazon.com/iamv2/home?#/roles)
11. Select 'Create Stack'

Go grab a coffee, this will take a few minutes...

Switch to the 'Outputs' tab in your newly created CloudFormation Stack view and copy the 'apiGatewayInvokeURL.'

The the following into a terminal window (if you are on a mac, you will have cURL already installed):

> $ curl --request POST [copied-from-output]/call

hint: it should look something like 

> $ curl --request POST https://rf48uo4dumbledore.execute-api.us-east-1.amazonaws.com/call

You should see the following response from your newly deployed service:

> Hello there 127.0.0.1 (with your outbound, not localhost).

Grab another coffee and a chocolate chip oatmeal cookie, you have a service running in the cloud!

What's next? Let's get your python script up there and then perhaps give some thought to adding additional security to your service with user authentication.

NOTE: If you want to tear down your environment, it's super easy, just navigate to your [stacks](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks?filteringStatus=active&filteringText=&viewNested=true&hideStacks=false), select the one you just created 'post-lambda-sample' and select 'Delete.' AWS CloudFormation will tear down all resources you've deployed (it's a good idea to tear it down if you're not using it to avoid any unnecessary charges).

REMEMBER: you can easily redeploy all the resources by following the steps above.  In fact, typically in a CI/CD environment where code is constantly being deployed with each approved pull request, we will also deploy any updated cloudformation files in the same CI/CD pipeline - fully automated!


