# ec2-scheduler

The [EC2 Scheduler](https://aws.amazon.com/answers/ec2-scheduler) is a simple AWS-provided solution that enables customers to easily configure custom start and stop schedules for their Amazon EC2 instances. The solution is easy to deploy and can help reduce operational costs for both development and production environments. 

Source code for the AWS solution "EC2 Scheduler". 


## Cloudformation templates

- cform/ec2-scheduler.template

## Lambda source code

- code/ec2-scheduler.py

## Building

In order to build this, you will need some python libraries and create a zip file to upload to Lambda / Cloudformation. 

Basic instructions are:
  cd code
  pip install boto3 -t .
  pip install urllib -t .
  pip install datetime -t .
  pip install pytz -t .
  zip  -r ../ec2-scheduler.zip 

### Lambda without cloudformation
If you want to upload directly to Lambda, replace the code that reads the DynamoDB table from cloudformation with:
IE: replace

  outputs = {}
  stack_name = context.invoked_function_arn.split(':')[6].rsplit('-', 2)[0]
  response = cf.describe_stacks(StackName=stack_name)
  for e in response['Stacks'][0]['Outputs']:
      outputs[e['OutputKey']] = e['OutputValue']
  ddbTableName = outputs['DDBTableName']

with:

  ddbTableName = 'EC2-Scheduler'

***

Copyright 2016 Amazon.com, Inc. or its affiliates. All Rights Reserved.

Licensed under the Amazon Software License (the "License"). You may not use this file except in compliance with the License. A copy of the License is located at

    http://aws.amazon.com/asl/

or in the "license" file accompanying this file. This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, express or implied. See the License for the specific language governing permissions and limitations under the License.
