---
layout: post
title:  "SNMP service for Zabbix"
date:   2023-06-21 16:21:30 +0900
categories: Zabbix
tags: Zabbix
permalink: /Networks/Zabbix/Zabbix-overall/Zabbix-SNMP

---

If you want to monitor device using with SNMP service, you need to open both inbound and outbound network port UDP 161 and 162.


Besides you need to open ICMP port for both in and outbound port to proceed PING check.


- Checking connection between device and Zabbix server.

```jsx
snmpwalk -v 2c -c zabbix <IP>
```

- Making list for device's snmp 

```php
snmpwalk -v 2c -c zabbix <IP> > snmpwalkList.log
```

- Checking SNMP trap status

```php
snmpwalk -v 2c -c zabbix <IP> ifLinkUpDownTrapEnable
IF-MIB::ifLinkUpDownTrapEnable.1 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.2 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.3 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.4 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.5 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.6 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.7 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.8 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.9 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.10 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.11 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.12 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.13 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.14 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.15 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.16 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.17 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.18 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.19 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.20 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.21 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.22 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.23 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.24 = INTEGER: enabled(1)
IF-MIB::ifLinkUpDownTrapEnable.25 = INTEGER: enabled(1)
```

```php
snmpget -v2c -c zabbix -On <IP> IF-MIB::ifOperStatus.1
.1.3.6.1.2.1.2.2.1.8.1 = INTEGER: down(2)
```

```php
snmpget -v2c -c zabbix -On <IP> IF-MIB::ifLinkUpDownTrapEnable.1
.1.3.6.1.2.1.31.1.1.1.14.1 = INTEGER: enabled(1)
```

[Configuring SNMP for Cisco network devices and create new host at Zabbix server](/Networks/Zabbix/Zabbix-overall/Zabbix-cisco)