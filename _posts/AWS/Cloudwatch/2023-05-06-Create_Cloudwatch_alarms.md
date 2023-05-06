---
layout: post
title:  "Create new Cloudwatch alarm"
date:   2023-05-06 12:11:38 +0900
categories: AWS
tags: AWS
permalink: /AWS/CloudWatch/Create_new_cloudwatch_alarm
---

This is an example of how to make cloudwatch alarm about this condition.
```
Rings alarm when disk used percentage ( root directory) is over 70% for twice time during 5 minute of Amazon EC2 instance.
```

**1.** Go to [Alarm] - [All Alarm] - [Create Alarm] in Cloudwatch console

![aws_cw_alarm](/assets/aws/cloudwatch/cw-alarm-1.png)

**2.** Press [Select Metric] to choose EC2 instance you want to make alarm.
![aws_cw_alarm-2](/assets/aws/cloudwatch/cw-alarm-2.png)
![aws_cw_alarm-3](/assets/aws/cloudwatch/cw-alarm-3.png)

Search EC2 instances by it's ID (which starts with i-) 