# sst-notky

### This project is based on SST (ServerlessStack Framework).

SST makes it easy to build serverless applications by allowing developers to:
1. Define their infrastructure using AWS CDK
2. Test their applications live using Live Lambda Development
3. Set breakpoints and debug in Visual Studio Code
4. Web based dashboard to manage your apps
5. Deploy to multiple environments and regions
6. Use higher-level constructs designed specifically for serverless apps
7. Configure Lambda functions with JS and TS (using esbuild), Go, Python, C#, and F#

### To do

[BED]
* ~~Configure AWS account~~
* Create database using DynamoDB
* Set up S3 for file uploads
* Write the various backend APIs
* Set up Cognito User Pools to manage user accounts
* Set up Cognito Identity Pool to secure our resources
* Working with secrets
* Adding unit tests

[FED]
* Set up our project with NextJS
* Set up MaterialUI
* Use AWS Cognito with Amplify to login and signup users
* Plugin to the backend APIs to manage notes
* Use the AWS Amplify to upload files
* Accepting credit cards with the Stripe React SDK
* Use custom domains for the API and React
* Create a CI/CD pipeline with Seed

Monitoring and debugging serverless apps:
* Set up error reporting in React using Sentry
* Configure an Error Boundary in React
* Add error logging to serverless APIs
* Cover the debugging workflow for common serverless errors

Main issue solved going serverless? Responsibility.

1. Devs are charged for keeping the server up even when we are not serving out any requests.
2. Devs are responsible for uptime and maintenance of the server and all its resources.
3. Devs are also responsible for applying the appropriate security updates to the server.
4. As usage scales devs need to manage scaling up server as well. And as a result manage
scaling it down when we don’t have as much usage.

There are a few reasons why serverless apps are favored over traditional server hosted apps:

1. Low maintenance - not having any servers to manage
2. Low cost - effectively only paying per request
3. Easy to scale - thanks in part to DynamoDB which gives near infinite scale and Lambda that simply scales up to meet the demand

The biggest benefit by far is that one only need to worry about the code and nothing else. And of course frontend is a simple static single page app that is almost guaranteed to always respond instantly thanks to CloudFront.

Serverless computing (or serverless for short), is an execution model where the cloud provider (AWS, Azure, or Google Cloud) is responsible for executing a piece of code by dynamically allocating the resources. And only charging for the amount of resources used to run the code. The code is typically run inside stateless containers that can be triggered by a variety of events including http requests, database events, queuing services, monitoring alerts, file uploads, scheduled events (cron jobs), etc. The code that is sent to the cloud provider for execution is usually in the form of a function. Hence serverless is sometimes referred to as “Functions as a Service” or “FaaS”. Following are the FaaS offerings of the major cloud providers, such as [AWS Lambda](https://aws.amazon.com/lambda/).

AWS Lambda (or Lambda for short) is a serverless computing service provided by AWS.

Lambda functions need to be packaged and sent to AWS. This is usually a process of compressing the function and all its dependencies and uploading it to an S3 bucket. And letting AWS know that you want to use this package when a specific event takes place.

SST converts infrastructure code into a CloudFormation template.
This is a description of the infrastructure that one is trying to configure as a part of your serverless project (ex. Lambda functions, API Gateway endpoints, DynamoDB tables, S3 buckets, etc.).
CloudFormation is an AWS service that takes a template (written in JSON or YAML), and provisions your resources based on that.

AWS CDK (Cloud Development Kit), released in Developer Preview back in August 2018; allows you to
use TypeScript, JavaScript, Java, .NET, and Python to create AWS infrastructure.

```
// CloudFormation Template Example (YAML)
- Resources:
- NotesTable:
- Type: AWS::DynamoDB::Table
- Properties:
- TableName: ${self:custom.tableName}
- AttributeDefinitions:
- - AttributeName: userId
- AttributeType: S
- - AttributeName: noteId
- AttributeType: S
- KeySchema:
- - AttributeName: userId
- KeyType: HASH
- - AttributeName: noteId
- KeyType: RANGE
- BillingMode: PAY_PER_REQUEST

// AWS CDK (JS)
+ const table = new dynamodb.Table(this, "notes", {
+ partitionKey: { name: "userId", type: dynamodb.AttributeType.STRING },
+ sortKey: { name: "noteId", type: dynamodb.AttributeType.STRING },
+ billingMode: dynamodb.BillingMode.PAY_PER_REQUEST,
+ });
```
CDK internally uses CloudFormation. It converts your code into a CloudFormation template. So in the
above example, you write the code at the bottom and it generates the CloudFormation template at
the top.

A CDK app is made up of multiple stacks. Or more specifically, multiple instances of the *cdk.Stack
class*. While these do get converted into CloudFormation stacks down the road, it’s more appropriate
to think of them as representations of your CloudFormation stacks, but in code.

`cdk synth` - converts these stacks into CloudFormation templates.
`cdk deploy` - submit these to CloudFormation. CloudFormation creates these stacks and all
the resources that are defined in them.

SST comes with a list of higher-level CDK constructs designed to make it easy to build serverless apps.

`sst build`, - runs `cdk synth` internally
`npm start` or `npm run deploy` - runs `cdk deploy`
