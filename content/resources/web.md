+++
title = "Do You Know About These Web Exploitation Tools?"
date = "2019-03-05"
weight = 200
+++

### Network Quick Scan ###
```html
nmap -sV -sC -A $IP
```       

### Webservers ###
#### Find vulnerability ####
Nikto:   
```html
nikto -h http://$IP
```            
Directory Brute Force: 
```html 
dirb http://$IP rockyou.txt -w -X .php,.html,.txt
```    

#### DNS ####
Zone Transfer:    
```html 
dig axfr $domain-name @$IP
ie. dig axfr @10.120.0.3 -p 6362 namezone.com
```    

Enum: 
```html
dnsrecon -d $domain-name
```