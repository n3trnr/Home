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
Rings alarm when disk used percentage
 (path : root directory) is over 70%
  for twice time during 5 minute of 
  Amazon EC2 instance.
```

**1.** Go to [Alarm] - [All Alarm] - [Create Alarm] in Cloudwatch console

![aws_cw_alarm](/assets/aws/cloudwatch/cw-alarm-1.png)

**2.** Press [Select Metric] to choose EC2 instance you want to make alarm.
![aws_cw_alarm-2](/assets/aws/cloudwatch/cw-alarm-2.png)
![aws_cw_alarm-3](/assets/aws/cloudwatch/cw-alarm-3.png)

Search EC2 instances by it's ID (which starts with i-) 

**3.** As you can see, you can now choose namespace. If you didnt installed CWAgent, You can only see AWS namespace, however we installed CWAgent so that we can define CWAgent metrics among Custom Namespaces.

![aws_cw_alarm-4](/assets/aws/cloudwatch/cw-alarm-4.png)


**4.** To make example alarm, you can find disk percentage metric at Custom namespace [CWAgent > ImageId, InstanceId, InstanceType, device, fstype, path]


![aws_cw_alarm-5](/assets/aws/cloudwatch/cw-alarm-5.png)

<Br><br>

Choose [Metric name] as [disk_used_percent], Path as [ / ].

If graph show up, CWAgent has succesfully caught the data.

