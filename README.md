# CloudwatchMetricAlarmPushedOnSns

## Description

An instance is created with Cloud-watch agent installed and configured. Custom logs are pushed to 
Cloud-watch. Custom metrics are created. Alarms are configured. Alarms are then pushed to SNS which
routes it to my email and SQS. 

## Files

It has 4 files to be uploaded as cloudformation stacks (California). 

1. vpc.yaml
2. instance.yaml
3. alarm.yaml
4. cloudformation.json 

## Working

Firstly, vpc.yaml is uploaded. It setups the environment required for the infrastructure to function.

Then, instance.yaml is uploaded to setup an ec2 instance and configure/install cloudwatch instance. It sets
it up to send custom metrics and logs to Cloudwatch.

Finally, alarm.yaml configures the required alarm. Sends it to SNS which then sends it to email and SQS. 
