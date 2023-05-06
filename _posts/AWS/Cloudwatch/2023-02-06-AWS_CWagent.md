---
layout: post
title:  "Install & Configure AWS CWagent app in EC2 Instance"
date:   2023-02-06 14:11:38 +0900
categories: AWS
tags: AWS
permalink: /AWS/CloudWatch/Install_&_Configure_CWAgent
---
This textbook is about how to install & configure AWS CloudWatch agent in EC2 instance

## Prerequisite 

-> You need IAM role for collects resources from EC2 instance.

<br>

### -  Making IAM Role for Cloudwatch agent

- Go to AWS IAM console and select [Roles] - [Create Role]
- Select [AWS Service] - [EC2]

![aws_cwagent1](/assets/aws/cwagent/aws_cwagent1.png)

- You will see the Add permissions section. Search [CloudWatchAgentServerPolicy] and choose it

![aws_cwagent2](/assets/aws/cwagent/aws_cwagent2.png)

- In this last step, name your role and make sure to check permission you've choose before
  
![aws_cwagent3](/assets/aws/cwagent/aws_cwagent3.png)
![aws_cwagent4](/assets/aws/cwagent/aws_cwagent4.png)

**※ If you dont add this role, this error will shows up when you start CWagent app**

![aws_cwagent_err](/assets/aws/cwagent/aws_cwagent_error.jpg)

<br>

## Install & configure

<BR>

- Connect into EC2 instance, and run this command to install CWAgent app

```
sudo yum install amazon-cloudwatch-agent

or else

https://s3.amazonaws.com/amazoncloudwatch-agent/amazon_linux/amd64/latest/amazon-cloudwatch-agent.rpm
```
- if you download rpm file, unzip the file 
```
  sudo rpm -ivh amazon-cloudwatch-agent.rpm 
```

- After you unzip the file, execute config wizard for configuring agent

```
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard 
```

- Once you execute wizard, you need to answer the question to configure

**1. On which OS are you planning to use the agent? :** you can choose between Linux and Windows

**2. Are you using EC2 or On-Premises hosts? :** Are you gonna install this agent in AWS EC2 or On-Presmises physical server?

**3. Which user are you planning to run the agent? :** In this step, you can choose which user will gather the data for metric

**4. StatsD daemon :** yes / no (StatsD daemon is a protocol to provides additional custom metrics to retreive more data)
**4. Do you want to turn on StatsD daemon? :** yes / no (StatsD daemon is a protocol to provides additional custom metrics to retreive more data)

**5. Do you want to monitor metrics from CollectD :** no (CollectD is and user defined metrics. Yet we dont need this for now)

**6. Do you want to monitor any host metrics? e.g. CPU, memory, etc** yes (Actually CPU utilization metrics are collected without using CWAgent)

**7. Do you want to monitor cpu metrics per core? Additional CloudWatch charges may apply. :** (Default : Yes)

**8. Do you want to add ec2 dimensions (ImageId, InstanceId, InstanceType, AutoScalingGroupName) :** yes

**9. Would you like to collect your metrics at high resolution? This enables sub-minute resolution for all metrics, but you can customize for specific metrics in the output json file :** (Default : 60s)

**10. Which default metrics config do you want? :** Standard

**Are you satisfied with the above config? Note: it can be manually customized after the wizard** -> Shows your configuration by JSON form.

**11. Do you want to monitor any customized log files? :** no

**14. Do you want to monitor log files? :** no

**15. Do you want to store the config in the SSM parameter store? :** no

**16. Program exits now.**


- Execute Agent

```
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:/opt/aws/amazon-cloudwatch-agent/bin/config.json -s
```

- Checks status of agent

```
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a status
```

- If you see this value, your agent is successfully running
  
```
{
"status": "running",

"version": "1.246396.0"
}
```

- Check agent's running log

```
tail -f /opt/aws/amazon-cloudwatch-agent/logs/amazon-cloudwatch-agent.log
```
- Command to see Cloudwatch agent log with real time. You can check if it runs without problems.