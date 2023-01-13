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

### ※  Before we begin, please check your python version in your local PC. you can check your python version by this command 
  
  ```
PS C:\Users> pip --version
pip 22.0.4 from C:\Program Files\WindowsApps\PythonSoftwareFoundation.Python.3.9_3.9.3568.0_x64__qbz5n2kfra8p0\lib\site-packages\pip (python 3.9)
  ```
<br>
  
### -  First, you need to make proper directory to download external library. <br>
    the location should be like this format
    
```
 /your_package_name/python/
```


### -  After you make directory, move to that directory by shell program
<br>

```
cd /your_package_name/python/
```

<br>

### -   And now you are ready to download the external library in your local computer 
 
```
 pip install [Package name] -t [your_package_name/python/] --no-user
```
<br>

### -   Once you install the package, your package directory should be look like this

  ![lambda_1](/assets/lambda_1.png)

### - Move out to your_package_name/ path
```
  cd ../..
```

<br>

### - And then, you should zip the directory as its package name. <br>
  (In this example, I used PowerShell script. But if you have another Zip-File maker (ex. Winzip), you can use it )
```
 ##This line works only in PowerShell! 

  Compress-Archive -Path ./[your_package_name] ./[your_package_name].zip
```

<br>

### - Now you finished to created package file to upload! Move on to AWS Lambda Console
  ![lambda_2](/assets/lambda_2.png)

<br>

### - Go to [Additional Layers] - [Layers] and then press [Create Layer] Button on Console
  ![lambda_3](/assets/lambda_3.png)

<br>

### - Fill out the Name and Description then select [Upload a .zip file] among radio button. After that press [Upload] button.
  ![lambda_4](/assets/lambda_4.png)
<p align='center'> You can also add compartible runtimes and license as options </p>
<br>

### ※ Pacakge file must be below 10MB. If its not, you should upload by S3
<br>

### - And now you succesfully uploaded python package into Lambda layer

  ![lambda_5](/assets/lambda_5.png)
    
<br>

### - You can add your custom layer when you editing Lambda function like this 

<br>
   
   ![lambda_6](/assets/lambda_6.png)

<br>

   ![lambda_7](/assets/lambda_7.png)

<br>

   ![lambda_8](/assets/lambda_8.png)

### - If you can't find your layer when you about to add, return to Lambda Layer page and find your layer, add Compartible architectures and Comaprtible runtimes. 

   ![lambda_9](/assets/lambda_9.png)