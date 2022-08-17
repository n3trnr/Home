---
layout: page
title:  "vlan"
date:   2022-08-17 16:21:30 +0900
categories: cisco
tags: vlan
permalink: /Networks/useful_cisco_commands/vlan
---

# VLAN

Whats VLAN? : VLAN is acronym of Virtual Local Area Network. It logically divides your local networks into pieces so that makes your network safer and better administrating network subnets

### Checking VLAN status

```jsx
show vlan
```

### Check VLAN status brief

```
show vlan brief
```

### Changing VLAN status

```jsx
SW1#configure terminal #aka conf t
SW1(config)#interface GigabitEthernet0/1
SW1(config)#switchmode access vlan (VLAN number)
SW1(config)#end
SW1#wr
```