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

<Br>

Choose [Metric name] as [disk_used_percent], Path as [ / ].

If graph show up, CWAgent has succesfully caught the data.

**5.** After you choose metric at step 4, and then now you can specify conditions.

![aws_cw_alarm-6](/assets/aws/cloudwatch/cw-alarm-6.png)

    
**Period** : set as [1 minute] (Check the status in every 1 minutes)

**Threshold type** : set as [Static] (Alarms when metric hits specific value)

- Anomaly detection means alarms when specific alarm hits up

**Define the alarm condition** : set as Grater

**than…** : set as 70

**Additional configuration > Datapoints to alarm** : set as 2 out of 5 

This means hit the alarm when disk percentage has become more than 70% during twice out of 5 minutes.

**6.** Now you can configure actions. You can set the action what to do when the alarm hits.

![aws_cw_alarm-7](/assets/aws/cloudwatch/cw-alarm-7.png)

**Alarm state trigger** : set as [In Alarm] 

This defines is this alarm is OK sign or real alarm.

**Send a notification to the following SNS topic** : You can send E-mail or text message by using AWS SNS topic.

- You can also set the Auto Scaling action (Increase/Decrease scaling group), EC2 action (ex : execute certain commands), System Manager action in this step.

**7.** Set the name and description.

![aws_cw_alarm-8](/assets/aws/cloudwatch/cw-alarm-8.png)

**8.** Preview and create

![aws_cw_alarm-9](/assets/aws/cloudwatch/cw-alarm-9.png)

**9.** And now you created alarm and you can check in [Alarms]
(For first 5 minutes statue could be shown as Data Insufficient. Due to latency of gathering data)

![aws_cw_alarm-10](/assets/aws/cloudwatch/cw-alarm-10.png)
