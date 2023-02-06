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

**1. Choose OS :** Linux / Windows / Other 

**2. Do you run this agent in EC2 or On-premise server? :** EC2 / On-premise

**3. Set the run user :** root / cwagent / others

**4. StatsD daemon :** yes / no (StatsD daemon is a protocol to provides additional custom metrics to retreive more data)

**5. CollectD daemon :** no (StatsD와 마찬가지)

**6. Cpu, Memory monitor :** yes (CPU랑 메모리도 모니터링할건지 여부 (이 둘은 EC2 만들면 기본으로 AWS에서 수집해주기는 한다))

**7. Get the data per Cpu core :** yes / no

**8. add ec2 dimensions :** yes

**9. 지표기록 주기 :** 60's(4번) (주기가 짧을 수록 더 높은 해상도의 지표가 기록 되지만 그만큼 더 많은 비용이 발생)
**10. default metrics :** Standard

**11. JSON :** yes (1번)로 진행
**12. 지금까지가 지표에** 관한 설정이였다면 이제 로그에 대한 설정을 진행한다. 다음에 나오겠지만 한 번에 설정하도록 하겠다.

**13. 기존에 설정된 CloudWatch Logs 설정 파일이 있는가? :** no

**14. 로그 파일 모니터링 :** no

**15. SSM parameter store 설정 :** no

**16. Program exits now.** 라는 문구와 함께 종료.


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

- > CloudWatch Agent 로그 실시간으로 확인하는 명령어
- CloudWatch Agent는 서비스로 자동으로 등록되어 종료되기 이전에 성공적으로 실행됐다면 시스템이 시작될 때 자동으로 실행 됩니다.

1-2. 기록된 지표 확인

1. CloudWatch 서비스 이동 -> 지표 -> CWAgent라는 이름의 네임스페이스가 사용자 지정 네임스페이스에 추가돼 있음을 확인.

![46b2e48a1366a89fd6a87454cb592ea6038fb2ac0e96bd08eadf43a49c6d4ae8.jpg](AWS%20CWagent%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20e31d937056c64e8b85d2574120c758af/46b2e48a1366a89fd6a87454cb592ea6038fb2ac0e96bd08eadf43a49c6d4ae8.jpg)

1. CWAgent 클릭 -> [Imageld, InstanceId, InstanceType] 클릭

![6ca961444aca6861e8c92a3250ac4022fad1ff708bb3e2ab0d0177acaeaeb73a.jpg](AWS%20CWagent%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8E%E1%85%B5%20e31d937056c64e8b85d2574120c758af/6ca961444aca6861e8c92a3250ac4022fad1ff708bb3e2ab0d0177acaeaeb73a.jpg)

1. 참고 2-1. CloudWatch Agent의 미리 정의된 지표 목록 Basic 메모리 사용량(used_percent)

Swap 사용량(used_percent)

Standard Basic의 내용

CPU 사용량(usage_idle, usage_iowait, usage_user, usage_system)

Disk 사용량(used_persent, inodes_free, io_time)

Advanced Standard의 내용

Diskio(write_bytes, read_bytes, writes, reads)

Netstat(tcp_established, tcp_time_wait)

2-2. CloudWatch Agent의 명령어와 주요 파일 위치 -. 특정 설정 파일을 사용해 CloudWatch Agent 서비스를 시작

```jsx
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -c file:[설정파일] -s 예시로 사용한 설정파일은 /opt/aws/amazon-cloudwatch-agent/bin/config.json 임을 알 수 있다.
```

```jsx
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a start -> CloudWatch Agent 서비스 시작
```

```jsx
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a stop -> CloudWatch Agent 서비스 중지
```

```jsx
sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -m ec2 -a status -> CloudWatch Agent 서비스 상태 조회
```

- CloudWatch Agent 설정 파일의 위치

Wizard로 생성한 파일 위치 

```jsx
/opt/aws/amazon-cloudwatch-agent/bin/config.json
```

실제로 CloudWatch Agent가 사용하는 설정 파일 위치

```jsx
/opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json
```