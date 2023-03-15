---
layout: post
title:  "Basic & Useful Linux Commands"
date:   2023-03-13 16:13:30 +0900
categories: Linux
tags: Linux
permalink: /Servers/Linux/commands
---
## **ls**

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
    

## **head**

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

## **tail**

- just like head command, tail shows 10 lines of the file but in opposite way
- It shows the last 10 lines of the file
- Can be used for tracking log files with -f option

```bash
# Show last 10 lines of the file
tail [filename]

# Keep tracking the file which one is keep written 
tail -f [filename]
```

## **date**

- Gets current datetime
- You can choose specific format to show date
- You can get previous, post date with -d (—date) option

```bash
# Get today's date in YYYY-MM-DD format
date "+%Y-%m-%d"

# Get the yesterday's date in YYYY-MM-DD format
date -d '1 day ago' "+%Y-%m-%d"
# or else
date -d 'yesterday' "+%Y-%m-%d"
 
# Get the date of 2 months ago in YYYY-MM-DD format
date -d '2 months ago' "+%Y-%m-%d"

# Get the date of last Sunday in YYYY-MM-DD format
date -d 'last sunday' "+%Y-%m-%d"

# Get the tomorrow's date in YYYY-MM-DD format
date -d 'tomorrow' "+%Y-%m-%d"

# Get the date after 3 years later in YYYY-MM-DD format
date -d '3 years' "+%Y-%m-%d"
```