---
layout: post
title:  "Useful Cisco Commands"
date:   2022-08-17 16:21:30 +0900
categories: Networks
tags: useful_cisco_commands
permalink: /Networks/useful_cisco_commands/

---

# Useful Cisco commands

### attempting SSH to another device in Cisco devices

```jsx
ssh -l (ID) (IP)
```

### Changing previlige password (enable password)

```jsx
conf t
enable secret (your password)
```

### Changing SSH password

```jsx
conf t
username (ID) secret (Password)
```

### Checking device interface ports

```
show interface status
```

### Checking interface status per ports

```
show ip interface brief
```

### show routing tables in L3 Switches or Router devices

```
sh run | i route
```

or just simply

```
show ip route
```

### Finding physical port number by MAC address

```
show mac address-table | i <Mac Address>
```

### Finding your neighbor network devices

```
show cdp neighbor
```