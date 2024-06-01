# AWS-serverless-inventory
AWS CloudFormation template which creates an inventory tracking system which reads inventory files, adds to a DynamoDB table, and sends SMS alerts.

In this scenario, the inventory tracking system is for international Apple stores. These stores will upload inventory files (the .csv files) to an Amazon S3 bucket. When this occurs, a Lambda function triggers which reads the CSVs and inserts the items into an Amazon DynamoDB table. Then, another Lambda funciton triggers to send notifications through Amazon SNS when inventory levels are critically low.
This serverless system reduces cost compared to if ran on servers, automatically scaling with usage and minimising costs while idle. Additionally the use of CloudFormation provides the benefits of infrastructure as code.

Very important!!!

When deploying the template, you NEED to use step1of2 for the base CloudFormation stack creation! Once the create is complete, then you can update the stack using step2of2, which will give the S3 bucket the trigger it needs.
This is because of a recursive issue with the way the trigger relys on the permission, as is discussed at the top of this page: https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-s3-bucket-notificationconfiguration.html

Also make sure to fully set up the SNS notification configuration.
