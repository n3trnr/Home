---
layout: post
title:  "Configuring SNMP for Cisco network devices and create new host at Zabbix server"
date:   2022-08-17 16:21:30 +0900
categories: Zabbix
tags: Zabbix
permalink: /Networks/Zabbix/Zabbix-overall/Zabbix-cisco

---

### From Cisco devices

Access to Cisco device console and run the command beneath this article in Configure terminal mode

```bash
snmp-server community public RO
snmp-server community private RW
snmp-server community Community RW
snmp-server enable traps snmp authentication linkdown linkup coldstart warmstart
snmp-server host {Zabbix Server's IP} version 2c public snmp
snmp ifmib ifindex persist
```

