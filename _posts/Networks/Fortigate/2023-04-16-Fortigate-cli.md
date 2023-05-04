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

**syn** : Calling packets.

**ack** : Packets has been received and acknowleged.

**fin** : Successfully finished network connections.


```
# You can also search specify IP and port at the same time.
diagnose sniffer packet any 'host [IP_ADDRESS] and port 443'

# You can use with AND & OR commands
diagnose sniffer packet any 'host [IP_ADDRESS] or port 443'

```

## execute

→ execute command is usually execute PING, SSH, TELNET, Traceroute commands

### execute ping (IP address)

→ Send ICMP PING to specific IP address

### execute telnet (IP address) (port)

→ Execute Telnet connection to specific IP address. You can also defines port too.

### execute ssh (IP address) (port)

→ Execute SSH connection to specific IP address. Just as telnet command, you can define port too

### execute traceroute (IP address)

→ Execute traceroute to specific IP address to track down how to reach.


```
# Using execute command in VDOM environment

refine # config vdom
refine (vdom) # edit root
current vf=root:0

# If you use VDOM mode in Fortigate FW, you must change into legit vdom account which has permit to use execute command.

# However, you can use Sudo command to override changing into other account

# ex) sudo root COMMAND

refine # sudo root execute  ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8): 56 data bytes
64 bytes from 8.8.8.8: icmp_seq=0 ttl=55 time=1.9 ms
64 bytes from 8.8.8.8: icmp_seq=1 ttl=55 time=1.8 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=55 time=1.8 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=55 time=1.7 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=55 time=1.8 ms

```

## Show

### show firewall

→  Shows information about this firewall device

(Use ? to check following commands)

### show firewall policy

→ Shows policy status in this firewall device

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

→ Shows routing table policy.

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

## get

### get system status

- > Check the OS version.

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

- > Check HA status in this firewall

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

- > check ARP addresses in this firewall

```

Refine_HQ_PTS_Internet_1 $ get system arp
Address           Age(min)   Hardware Addr      Interface
55.55.10.29       1          c4:65:**:**:**:** LAN
55.55.10.58       0          c4:65:**:**:**:** LAN
55.55.10.116      1          c4:65:**:**:**:** LAN
55.55.10.174      0          3c:52:**:**:**:** LAN
55.55.10.203      3          c8:d9:**:**:**:** LAN

```

## Config 

- This commands can actually affects to firewall environment. So you must use it carefully.

### config firewall address

- Adds new IP address in [Address]

```bash
config firewall address
edit "[Address Name]"
set subnet [IPv4 Address] 255.255.255.255
next
end
```

### config router static

- Create new or configures existing routing table policy

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

- Create new or configures existing firewall policy

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