# Cloudformation Template for EKS Onboarding
A Cloudformation template for onboarding EKS logs with Expel Workbench.

## Usage

Navigate to the [CloudFormation Console](https://console.aws.amazon.com/cloudformation/home?#/stacks/create/template), and upload the `expel_eks_onboarding.template`.

## Parameters

This Cloudformation template accepts the following parameters:

| Parameter | Description |
| --- | --- |
| ExpelCustomerOrganizationGUID | The organization GUID assigned to you by Expel |
| ExpelAWSAccountARN | The Expel AWS account to grant assume role access |
| ExpelAssumeRoleSessionName | The assume role session name Expel will use |
| EKSLogGroupName | The log group name containing EKS logs to send to Expel |
| StreamRetentionHours | The number of hours logs will be kept in the Kinesis stream |

## Resources

Launching a stack with this template will create the following resources:

| Resource Type | Name | Description |
| --- | --- | --- |
| AWS::Kinesis::Stream | ExpelEKSLogStream | A Kinesis stream Expel will consume EKS logs from |
| AWS::Logs::SubscriptionFilter | N/A | A subscription filter that sends logs from CloudWatch to the Kinesis stream |
| AWS::IAM::Role | ExpelEKSServiceAssumeRole | An IAM role Expel will use to consume EKS logs |
| AWS::IAM::Role | EKSLogsCloudWatchAssumeRole | An IAM role CloudWatch will use to deliver logs to Kinesis |
| AWS::IAM::ManagedPolicy | ExpelEKSAssumeRolePolicy | A policy that grants the Expel IAM role permissions to read from Kinesis and discover EKS clusters |
| AWS::IAM::ManagedPolicy | EKSProducerPolicy | A policy that grants CloudWatch permissions to deliver logs to Kinesis |