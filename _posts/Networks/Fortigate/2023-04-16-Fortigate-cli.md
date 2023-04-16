---
layout: post
title:  "Fortigate CLI"
date:   2023-04-16 17:04
categories: Networks
tags: Firewall
permalink: /Networks/Fortigate/Fortigate_CLI
---

Fortigate Firewall configuration is ususally based on GUI enviornment. However you can also access with SSH protocol and configure with CLI option

This is how you get into CLI terminal after you log in Fortigate Firewall in GUI web page.

![fortigate-cli-1](/assets/fortigate/forti-cli-1.png)

## Some useful Fortigate CLI commands

### diagnose sniffer packet any 'host (IP address)'

→ Shows packet connections via specific IP address

![fortigate-cli-2](/assets/fortigate/forti-cli-2.png)

For example, If you want to see packets that flows into 10.1.4.43, it shows like this.

**syn** : Calling 

**ack** : 해당 IP 측에서 받음

**fin** : 통신 완료되어 종료

다음과 같이 구분하시면 됩니다.

```
# 해당 IP주소와 특정 포트를 함께 조회 하는 식으로도 가능합니다.
diagnose sniffer packet any 'host IP_ADDRESS and port 443'

# 또는 and 조건이 아닌 or 조건으로도 사용 가능
diagnose sniffer packet any 'host IP_ADDRESS or port 443'

```

## execute 명령어

→ 일반적인 PING 이나 TELNET 명령어의 경우 앞에 execute 명령어를 사용해야합니다.

### execute ping (IP 주소)

→ 해당 IP 주소로 PING을 날립니다.

### execute telnet (IP 주소) (포트)

→ 해당 IP 주소로 텔넷 통신을 시도합니다. 포트도 지정 가능합니다.

```
# vdom 사용 환경에서 vdom 전환

refine # config vdom
refine (vdom) # edit root
current vf=root:0

# 특별하게 vdom을 사용하는 환경의 Fortigate라면 vdom을 전환해야 명령어를 사용 할 수 있다.
# 하지만 vdom 전환하지 않고 execute나 diagnose 명령어를 사용하고자 한다면 아래와 같이 sudo 명령어를 사용하면 된다.
# ex) sudo root COMMAND

refine # sudo root execute  ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8): 56 data bytes
64 bytes from 8.8.8.8: icmp_seq=0 ttl=55 time=1.9 ms
64 bytes from 8.8.8.8: icmp_seq=1 ttl=55 time=1.8 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=55 time=1.8 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=55 time=1.7 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=55 time=1.8 ms

```

## Show 명령어

### show firewall

→  방화벽 관련 정보를 보여줌

(? 를 이용해서 뒤에 어떤 명령어가 사용될 수 있는지 조회 가능)

### show firewall policy

→ 정책 조회

```
SK_IDC_Phone_1 $ show firewall policy
config firewall policy
    edit 4
        set uuid <uuid no.1>
        set srcintf "LAN"
        set dstintf "HQ_Phone_VPN"
        set srcaddr "<IP>" "<IP2>" "<IP3>"
        set dstaddr "<IP4>" "<IP5>" "<IP6>"
        set action accept
        set schedule "always"
        set service "ALL"
        set logtraffic all
    next
    edit 3
        set uuid <uuid no.2>
        set srcintf "HQ_Phone_VPN"
        set dstintf "LAN"
        set srcaddr "<IP>" "<IP2>" "<IP3>"
        set dstaddr "<IP4>" "<IP5>" "<IP6>"
        set action accept
        set schedule "always"
        set service "ALL"
        set logtraffic all
    next
end

```

### show router static

→ 정적 라우팅 조회

```
bash
SK_IDC_Phone_1 $ show router static
config router static
    edit 1
        set gateway <gateway IP>
        set device "wan1"
    next
    edit 2
        set dst <IP> 255.255.255.0
        set gateway <Gateway IP>
        set device "LAN"
    next
end

```

## get 명령어

- 주로 현재 설정된 정보를 읽고자 할 때 사용되는 명령어입니다.

### get system status

- > OS 버전 확인

```
SK_IDC_Phone_1 $ get system status
Version: FortiGate-100E v6.2.7,build1190,201216 (GA)
Virus-DB: 1.00000(2018-04-09 18:07)
Extended DB: 1.00000(2018-04-09 18:07)
IPS-DB: 6.00741(2015-12-01 02:30)
IPS-ETDB: 0.00000(2001-01-01 00:00)
APP-DB: 6.00741(2015-12-01 02:30)

```

### get system ha status

- > HA 구성 확인

```
SK_IDC_Phone_1 $ get system ha status
HA Health Status: OK
Model: FortiGate-100E
Mode: HA A-P
Group: 0
Debug: 0
Cluster Uptime: 543 days 19:29:47
Cluster state change time: 2021-04-16 14:42:47
Master selected using:
    <2021/04/16 14:42:47> FG100E********** is selected as the master because it has the largest value of uptime.
    <2021/04/16 14:37:21> FG100E********** is selected as the master because it's the only member in the cluster.
ses_pickup: disable
override: disable

```

### get system arp

- > ARP 조회

```

Refine_HQ_PTS_Internet_1 $ get system arp
Address           Age(min)   Hardware Addr      Interface
55.55.10.29       1          c4:65:**:**:**:** LAN
55.55.10.58       0          c4:65:**:**:**:** LAN
55.55.10.116      1          c4:65:**:**:**:** LAN
55.55.10.174      0          3c:52:**:**:**:** LAN
55.55.10.203      3          c8:d9:**:**:**:** LAN

```

## Config 명령어

### config firewall address

- Address 에 새로운 주소 추가

```bash
config firewall address
edit "[Address Name]"
set subnet [IPv4 Address] 255.255.255.255
next
end
```

### config router static

- 정적 라우팅 생성

```bash
config router static
edit 0
set dst [IP] 255.255.255.0
set gateway [Gateway IP]
set device "VPN tunnel name"
set comment "Comments"
next
end
```

### config firewall policy

- IPv4 정책 생성

```bash
config firewall policy
edit 0
set name "[Policy Name]"
set srcintf "[Source Interface]"
set dstintf "[Destination Interface]"
set srcaddr "[Source IP]"
set dstaddr "[Destination IP]"
set action accept
set status disable
set schedule "always"
set service "ALL"
set logtraffic all
next
end
```