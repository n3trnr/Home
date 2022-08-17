# Useful Cisco commands

[VLAN](Useful%20Cisco%20commands%20381e53546556453ca4e2af699002fc1f/VLAN%2022fcc80cf580498f9ca3d14326e29939.md)

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