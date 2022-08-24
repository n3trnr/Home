---
layout: post
title:  "SSH"
date:   2022-08-24 14:30:30 +0900
categories: Networks
tags: SSH
permalink: /Networks/SSH/
---

## What's SSH? 

SSH, Secure Socket Shell was developed to make up for vulnarability of Telnet services. \
With encryption key, SSH provides secured remote connection between network devices.  \




## How to set SSH on Cisco device?

```
Switch#configure terminal ## Enters Configuration mode

Switch(config)# username admin password 123 ## Configuring user and password 

Switch(config)#enable secret 123 ## Set the previleage mode password

Switch(config)#hostname <your hostname> ## must set your device's hostname!

Switch(config)#ip domain-name <your domain name> ## Set your own domain name 

Switch(config)#crypto key generate rsa ## make encryption key for secure connection (in this example, I used RSA)

The name for the keys will be: Switch.<your domain name>
Choose the size of the key modulus in the range of 360 to 4096 for your
General Purpose Keys. Choosing a key modulus greater than 512 may take
a few minutes.

How many bits in the modules [512]: 1024 ## Configuring bitrate for RSA key

% Generating 1024 bit RSA keys, keys will be non-exportable...
[OK] (elapsed time was 4 seconds)

Switch(config)#line vty 0 15 
## this line is to configuring previleage level to each users. 0 and 15 means administrator 

Switch(config-line)#transport input ssh 
## allows input only SSH 


Switch(config-line)#login local
## means you're gonna log in with this local account only
```

## Additional configuration

```