---
layout: post
title:  "Basic & Useful Linux Commands"
date:   2023-03-13 16:13:30 +0900
categories: Linux
tags: Linux
permalink: /Servers/Linux/commands
---
## ls

list file & directory

```jsx
ls -a : Shows every files and directories including hidden ones
ls -l : Shows verbose informations (Date, Permissions etc)
```

## **tar**

- Compresses multiple files or directories
- In tar, you can use 3 different compression method : tar, tar.gz, bzip2

- **Compress into tar.gz file**
    
    ```bash
    tar -cfvz [Filename].tar.gz [location]/
    ```
    
- **Decompress the tar.gz file into local directory**
    
    ```bash
    tar -xfvz [tar.gz_filename].tar.gz
    ```
    
- **Decompress the tar.gz file into specific directory**
    
    ```bash
    tar -xfvz [tar.gz_filename] -C [directory_location]
    ```
    

## head

- head command shows the first 10 line of the file
- Can be used with cat command

```bash
 # Shows first 10 lines of the file
head [filename]

# Specifies line number you want to see
head -n*[line number]* [filename] 

# Use head command with cat command
cat [filename] | head -n******[line numbers]******
```

## tail

- just like head command, tail shows 10 lines of the file but in opposite way
- It shows the last 10 lines of the file
- Can be used for tracking log files with -f option

```bash
# Show last 10 lines of the file
tail [filename]

# Keep tracking the file which one is keep written 
tail -f [filename]
```