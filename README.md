# sst-notky

[BED]
* Configure AWS account
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

Serverless computing (or serverless for short), is an execution model where the cloud provider (AWS,
Azure, or Google Cloud) is responsible for executing a piece of code by dynamically allocating the
resources. And only charging for the amount of resources used to run the code.
The code is typically run inside stateless containers that can be triggered by a variety of events including http requests,
database events, queuing services, monitoring alerts, file uploads, scheduled events (cron jobs), etc.
The code that is sent to the cloud provider for execution is usually in the form of a function. Hence
serverless is sometimes referred to as “Functions as a Service” or “FaaS”. Following are the FaaS
offerings of the major cloud providers, such as [AWS Lambda](https://aws.amazon.com/lambda/).

AWS Lambda (or Lambda for short) is a serverless computing service provided by AWS.

Lambda functions need to be packaged and sent to AWS. This is usually a process of compressing the
function and all its dependencies and uploading it to an S3 bucket. And letting AWS know that you
want to use this package when a specific event takes place.
