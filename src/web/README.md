# post-lambda-sample

This is a simple example of how to build and deploy a static website that sends a POST request to an AWS service.

I've created this configuration for hosting application admin consoles and developer documentation. For example check out https://developer.youi.tv/, which is powered by [Jekyll](https://jekyllrb.com/).

## Setup

### Clone this repository

You should have already cloned the parent directory and all sub-directories.

## Static website

Let's create a static website.  

How to host a static website on AWS S3 can be found [here](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html).  Feel free to book mark that site so you can read it later and skip to 'Create an S3 Instance' below.

### Configuring a static website on Amazon S3

Navigate to [Tutorial: Configuring a static website on Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html#step2-create-bucket-config-as-website) and follow the instructions to create a static website hosted on AWS S3.

Use the index.html and error.html pages provided in this git repository. We can add your website once we have authentication and HTTPS supported.

### Configuring CloudFront for my static website

CloudFront offers a couple advantage, first it caches your website closer to your customers for rendering time is faster for the end user. Second, you can enable HTTPS (SSL) for better security.

To configure CloudFront for your static website, check out [Using a website endpoint as the origin, with anonymous (public) access allowed](https://aws.amazon.com/premiumsupport/knowledge-center/cloudfront-serve-static-website/).

When creating your [CloudFront distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-creating-console.html), 

1. Origin Domain will be your S3 endpiont you created above, something like: BUCKET-NAME.s3-website-us-east-1.amazonaws.com.
1. For oOrigin Domain protocol, select HTTP here - this is for communication between CloudFront and your S3 bucket, which is only configured to support HTTP.
1. View settings, here choose 'Redirect HTTP to HTTPS' and set Allowed HTTP methods to 'GET, HEAD' only.
1. For default root object, enter 'index.html' (without the quotes). Note this is option is you are using index.html as your root page for your site.
1. Once you hit 'create' it will take some time to deploy before your CloudFront becomes active, time to go grab a coffee.

Once CloudFront has been deployed, copy the 'distribution domain name' and paste it into a browser address bar - the index.html page will now render via https.

### Restrict access to my static website

So far we have a static website that can be accessed either directly on S3 via HTTP or through CloudFront on HTTPS. Now we want to limit that access to only CloudFront HTTPS and prevent users from hitting S3 directly.

https://aws.amazon.com/premiumsupport/knowledge-center/cloudfront-access-to-amazon-s3/

Right now CloudFront is accessing your S3 bucket as a static website, let's change that first.  

1. Open the [CloudFront console](https://console.aws.amazon.com/cloudfront/)
1. From the list of distributions, choose the distribution that serves content from the S3 bucket that you want to restrict access to.
1. Choose the Origins tab.
1. Select the Origin name and choose 'edit.'
1. In the Origin Domain drop-down, choose your S3 bucket.
1. For S3 Bucket Access, choose 'Yes use OAI (bucket can restrict access to only CloudFront).'
1. Create a new OAI and choose Bucket Policy: 'Yes, update the bucket policy.'
1. Save your changes.

As above, try it out. Use the same 'distribution domain name' as above (for example: https://dfoo81275bar.cloudfront.net/) and the index.html page should render.

Now navigate to the [S3 Console](https://console.aws.amazon.com/s3/) and turn off 'host static website' so that the S3 bucket will only be accessible through CloudFront.

1. From the list of S3 buckets, choose the bucket that you created above.
1. Choose the Properties tab.
1. Scroll to the bottom, 'Static website hosting' and choose 'edit.'
1. Disable 'Static website hosting.'

Try it out again. As above use the same 'distribution domain name' as above (for example: https://dfoo81275bar.cloudfront.net/) and the index.html page should render.

Now you have a static website hosted on AWS S3 and accessible to the public only through CloudFront on HTTPS! Take a break.

Check out [CNAME](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/CNAMEs.html) configuration when you have your own domain, www.foo.com for example.

Next if you are securing your static website behind AWS Cognito, check out this link for how to Use Lambda@Edge to [Enhance Web Application Security](https://aws.amazon.com/blogs/networking-and-content-delivery/authorizationedge-how-to-use-lambdaedge-and-json-web-tokens-to-enhance-web-application-security/).
