+++
title = "Binary Exploitation 0: Useful Commands"
date = "2020-10-10"
weight = 350
+++
                                                                                  
1. Get function names: ```nm binary | grep ' t ' ```                                                              
2. Get ***GOT*** entries: ```readelf --relocs binary```                                               
3. Get ***PLT*** entries: ```objdump -M intel -dj .plt binary```                                         
4. Get strings: ```strings binary```                  
5. Virtual address space layout: ```vmmap``` in debugger
6. Finding gadgets: ```ROPgadget```                            
