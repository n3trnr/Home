---
layout: post
title:  "How to set NTP server in Fortigate Firewall?"
date:   2023-01-17-16:14
categories: Networks
tags: Firewall
permalink: /Networks/Fortigate/Fortigate_NTP
---

---
<br>

In Fortigate devices, you can configure NTP server address by GUI interface

  ![Fortigate-ntp-1](/assets/fortigate-ntp-1.png)

.....aaand yeah its better to configure your custom NTP server by CLI interface

<br>

### ※ Before you begin this procedure make sure to check if you have permission to enter Fortigate CLI console

<br>

- You can check NTP server status of your Fortigate system before you begin like this

```
  Fortigate_FW $ show system ntp
    config system ntp
    set server-mode enable
    set interface "fortilink"
    end
```

in this case, your Fortigate Firewall's NTP function has not been enabled. So we need to enable its function first.
<br>
  

- Enabling NTP Sync

```
  Fortigate_FW $ config system ntp
  Fortigate_FW (ntp) $ set ntpsync enable
 
  Fortigate_FW (ntp) $ end
 
  Fortigate_FW $ show system ntp
    config system ntp
      set ntpsync enable
      set server-mode enable
      set interface "fortilink"
    end
```

<br>

- Setting the custom NTP Server IP
  
```
Fortigate_FW $ config system ntp
Fortigate_FW (ntp) $ set type custom
Fortigate_FW (ntp) $ set syncinterval 30
Fortigate_FW (ntp) $ config ntpserver 
Fortigate_FW (ntpserver) $ edit 1
new entry '1' added
Fortigate_FW (1) $ set server <YOUR CUSTOM NTP SERVER IP>
Fortigate_FW (1) $ next
Fortigate_FW (ntpserver) $ end
Fortigate_FW (ntp) $ end
```

- And you will get the result like this

```
Fortigate_FW $ show system ntp
config system ntp
    set ntpsync enable
    set type custom
    set syncinterval 30
    config ntpserver
        edit 1
            set server "<YOUR CUSTOM NTP SERVER IP>"
        next
    end
```

- this is the meaning of each commands as follows.
  
```
config system ntp

 set ntpsync enable -> Enable NTP sync function

 set type custom -> Enable sync with custom NTP server 

 set syncinterval 30 
 -> Refresh time sync with NTP server for each 30 minutes

 config ntpserver -> Enter the NTP server settings

    edit 1 -> Primary NTP server
        set server <YOUR CUSTOM NTP SERVER IP>
    next
 end
```

- Then you can see custom NTP server IP has been set on your firewall
  
  ![Fortigate-ntp-2](/assets/fortigate-ntp-2.png)