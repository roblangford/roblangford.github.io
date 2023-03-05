---
layout: default
title: AWS uptime/downtime
date: 2022-04-23
---

With All Cloud hosting service providers you are billed by the operational hours/minutes/seconds that services are online and running. If you host Production and Non-Production systems it may not make sense to have these running all of the time, especially if you dont have testing or development work taking place out of hours or on weekends.
My focus is primarily on AWS so this is where I will begin however these patterns can be repeated for other providers.
We use Cloud Watch Event Rules to trigger at specific dates/times on schedules or in response to other external triggers. These will fire a Lambda Function will perform the stopping/starting of services, in order to ensure the correct systems are stopped/started we will use specific tags. I will be coding the Lambda Function using Python.

## IAM Access - 
Typically you will need a simply IAM policy to stop and start services, if however you are using KMS encryption on disks you will need to provide access for the keys also.

1. First Create an IAM Policy for Lambda, the example below assumes you are using KMS encrypted disks and logging to CloudWatch. These permissions can be adjusted as required.

### Lambda IAM Policy
```json

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowCloudWatchLogAccess",
      "Effect": "Allow",
      "Action": [
        "logs:CreateLogGroup",
        "logs:CreateLogStream",
        "logs:PutLogEvents"
      ],
      "Resource": "arn:aws:logs:*:*:*"
    },
    {
      "Sid": "KMSKeyAccess",
      "Effect": "Allow",
      "Action": [
        "kms:Decrypt",
        "kms:DescribeKey",
      ],
      "Resource": "arn:aws:kms:<region>:<accountnum>:key/xxxxx-xxxx-xxxx-xxxxxxxx"
    },
    {
      "Sid": "AllowEC2StopStart",
      "Effect": "Allow",
      "Action": [
        "ec2:Start*",
        "ec2:Stop*"
      ],
      "Resource": "*"
    },
  ]
}

```
Replace the KMS resource arn with the specific one used for your EC2 disk encryption.

2. Now create an IAM role to attach this role too. (AWS Guide)


### Lambda Function
As mentioned earlier I will be coding this solution in Python however feel free to port this code to something you are more familiar with or find an alternative.

1. In AWS Console search or select AWS Lambda and choose Create function
2. Select Author from Scratch and enter the following information.
    Function name: StopEC2Instances
    Runtime: Python 3.9
    Permissions - expand Change default execution role, under Execution role select Use an existing role and choose the IAM role created earlier.
3. Choose Create function, under Code source past in the following code


```python
import boto3
region = '<region>'

# EC2 instance lookup
def ec2_instance_lookup():
    # Get all EC2 instances
    all_ec2_instances = ec2.desc
    # Filter based on tags

    # Return 



# Main code
def lambda_handler(event, context):

    # Lookup EC2 instances.
    instances = ec2_instance_lookup()

    f'Stopping the EC2 instances: {instances}'

    # Stop EC2 instances.
    ec2.stop_instances(InstanceIds=instances)
    

```

# EC2

# RDS






# Links:
[ACSC - Hardening Linux Workstations and servers](https://www.cyber.gov.au/acsc/view-all-content/publications/hardening-linux-workstations-and-servers)

[Red Hat Enterprise Linux 8 - Security Hardening](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html/security_hardening/index)

[CentOS 7 - Hardening](https://www.tecmint.com/security-and-hardening-centos-7-guide/)