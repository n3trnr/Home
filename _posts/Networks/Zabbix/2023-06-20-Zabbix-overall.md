---
layout: page
title:  "Zabbix"
date:   2023-06-20 17:21:30 +0900
categories: Networks
tags: Zabbix
permalink: /Networks/Zabbix/Zabbix-overall
---

## Zabbix

Zabbix is a management system to monitor network devices, server hardwares and also provides alarms for system administrator.

You can install Zabbix agent at UNIX, Linux and Windows OS system to monitor such as CPU usuage, Network traffics, disk usuage percents etc.

---

- Network port for Zabbix system.
    
    ```jsx
    inbound open 10051 zabbix server
    inbound open 10050 zabbix agent
    ```
    
- server
    
    ```jsx
    10050 inbound source 10.19.0.0
    ```
    
- client
    
    ```jsx
    10050 inbound/outbound source zabbix server
    ```
    
- Commands that detecting UserParameter from Zabbix server.
    
    ```php
    zabbix_get -s 10.19.1.105 -p 10050 -k "vfs.fs.size[E:,used]"
    ```