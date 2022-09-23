---
layout: page
title:  "Lambda-Layers"
date:   2022-09-13 14:55:30 +0900
categories: AWS
tags: AWS
permalink: /AWS/lambda/lambda-layer
---

## How to add Lambda-Layers
-----
### (This guide is based on Python 3.9 version and Windows PC)
<br>
*  Before we begin, please check your python version in your local PC. you can check your python version by this command 
  
  ```
PS C:\Users> pip --version
pip 22.0.4 from C:\Program Files\WindowsApps\PythonSoftwareFoundation.Python.3.9_3.9.3568.0_x64__qbz5n2kfra8p0\lib\site-packages\pip (python 3.9)
  ```
<br>
  
  1.  First, you need to make proper directory to download external library. <br>
    the location should be like this format
    
```
 /your_package_name/python/
```
<br>

2. After you make proper directory, move to that directory by shell program
<br>

```
cd /your_package_name/python/
```

<br>

3.  And now you are ready to download the external library in your local computer 
 
```
 pip install [Package name] -t [location] --no-user
```
<br>

4.  