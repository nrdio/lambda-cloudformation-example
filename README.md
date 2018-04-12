# Example CloudFormation Template for creating a CloudFormation stack comprising of SNS topic, Subscription and Lambda

This [template](cloudformation-template.yaml) creates a CloudFormation stack comprising of -

   * SNS topic
   * Simple Node.js Lambda
   * Lambd SNS topic subscription
   * IAM Roles and Policies


This template is intended to jump start Lambda development by putting otherwise extensive and fragmented information together. 
Additional information is available at [Shift from Containers to Serverless Computing using AWS Lambda](http://woodo.space/shift-from-containers-to-serverless-computing-using-aws-lambda/)

## How to run?

Prerequisite : [AWS account](https://aws.amazon.com/) and [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/installing.html)
   
Create a package by running following AWS CLI command

```
aws cloudformation package --template-file cloudformation-template.yaml --s3-bucket <your-bucket-name> 
    --output-template-file packaged-template.yaml
```

Create Stack using following command

```
aws cloudformation deploy --template-file packaged-template.yaml --stack-name <your-stack-name> --capabilities CAPABILITY_IAM
```
## Test

List stack resources using following command 

```
aws cloudformation list-stack-resources --stack-name <your-stack-name>
```

Please copy SNS topic(AWS::SNS::Topic) ARN (PhysicalResourceId) from list of resources. 

Now you can publish a message to SNS topic using following command. Lambda should log the event in CloudWatch logs.

```
aws sns publish --topic-arn your-sns-topic-arn --message "Hello World"
```


