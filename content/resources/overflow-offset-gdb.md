+++
title = "Binary Exploitation 3: Finding Buffer Overflow Offset with GDB"
date = "2020-10-31"
weight = 600
+++

### Using GDB and gef 
```html
gef> pattern create 128                         
aaaaaaaaaaaaaaaaaaaaaaaaaaaaaa....aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa                                    
gef> run
```             
copy paste the created pattern as input to program ```aaaaaaaa......aaaaaaaaaaaaaaaaa```                      
The program will seg fault at $rsp because the pattern overflow the pointer
```html
gef> pattern search $rsp
[+] Fond at offset 40
gef>            
```


