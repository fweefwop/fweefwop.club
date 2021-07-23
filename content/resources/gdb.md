+++
title = "Binary Exploitation 1: Using GDB"
date = "2020-10-31"
weight = 400
+++

##  Enable core dumps
```html
ulimit -c unlimited
ulimit -c
```

## Install GDB
```html
sudo apt-get install gdb
```

## Run GDB to analyze     

Complet commands: https://visualgdb.com/gdbreference/commands/      

### Run gdb, load a program to analyze
```html 
gdb vuln
```

**-q** -> hide the initial chunk when executing gdb
**-x file** -> pass in a file with gdb
**-p pid** -> attach to process

### Dissasemble the function
```html 
disas main
```      
```html 
disas 0x12345
```     

### Finding the address of the function
```html 
p system
```         

### Convert hex to dec
```html
(gdb) p/d ox10f
$1 = 271
```     

### Set breakpoint
```html
b *main       
b *func + 23       
b *0x1234             
b *0x1234 + 23
```                    

### Clear breakpoint
```html 
clear linenumber 
```         

### Execute next instruction

```html
nexti 
```    

### Show debugging symbols
```html 
list
list main
```                        

### examine register address
``` info register rip``` (or ```i r rip```)  

example:
```html
gef➤  i r rip        
rip            0x55555555513d      0x55555555513d <main+8>     
```      

### Get any address using print
example:
```html
gef➤  print $rbp - 4
$2 = (void *) 0x7fffffffe06c
```           

### Run the overflow, seg fault
```html
run $(python -c 'print "\x41" * 508')
```                     

### Examine value @ address
```x``` means examine. It takes two arguments: location in memory and how to display that memory.
```o``` display in octal         
```x``` display in hex        
```u``` display in unsigned decimal        
```t``` display in binary         

```html 
x/200x ($esp - 550)                 
x/w pointer  -> value of the pointer                          
x/s pointer -> string pointed by the pointer                   
x/i $eip  -> instructions of the EIP
```                  

example:        
```html                     
gef➤  x/x $rbp - 4
0x7fffffffe06c: 0x00000000
```          

### Example

```html
$gdb allokay
gef➤  b *main
Breakpoint 1 at 0x40084f
gef➤  info files
Symbols from "/home/kali/damctf/allokay/allokay".
Local exec file:
        `/home/kali/damctf/allokay/allokay', file type elf64-x86-64.
        Entry point: 0x400680
        0x0000000000400238 - 0x0000000000400254 is .interp
        0x0000000000400254 - 0x0000000000400274 is .note.ABI-tag
        0x0000000000400274 - 0x0000000000400298 is .note.gnu.build-id
        0x0000000000400298 - 0x00000000004002bc is .gnu.hash
        0x00000000004002c0 - 0x00000000004003e0 is .dynsym
        0x00000000004003e0 - 0x0000000000400475 is .dynstr
        0x0000000000400476 - 0x000000000040048e is .gnu.version
        0x0000000000400490 - 0x00000000004004d0 is .gnu.version_r
        0x00000000004004d0 - 0x0000000000400518 is .rela.dyn
        0x0000000000400518 - 0x00000000004005d8 is .rela.plt
        0x00000000004005d8 - 0x00000000004005ef is .init
        0x00000000004005f0 - 0x0000000000400680 is .plt
        0x0000000000400680 - 0x0000000000400942 is .text
        0x0000000000400944 - 0x000000000040094d is .fini
        0x0000000000400950 - 0x00000000004009be is .rodata
        0x00000000004009c0 - 0x0000000000400a0c is .eh_frame_hdr
        0x0000000000400a10 - 0x0000000000400b50 is .eh_frame
        0x0000000000600e10 - 0x0000000000600e18 is .init_array
        0x0000000000600e18 - 0x0000000000600e20 is .fini_array
        0x0000000000600e20 - 0x0000000000600ff0 is .dynamic
        0x0000000000600ff0 - 0x0000000000601000 is .got
        0x0000000000601000 - 0x0000000000601058 is .got.plt
        0x0000000000601058 - 0x0000000000601068 is .data
        0x0000000000601080 - 0x00000000006010d8 is .bss
gef➤  shell
kali@kali:~/damctf/allokay$ ROPgadget --binary allokay| grep pop
0x000000000040075c : add byte ptr [rax], al ; add byte ptr [rax], al ; push rbp ; mov rbp, rsp ; pop rbp ; jmp 0x4006f9
0x000000000040075d : add byte ptr [rax], al ; add byte ptr [rbp + 0x48], dl ; mov ebp, esp ; pop rbp ; jmp 0x4006f8
0x00000000004006e6 : add byte ptr [rax], al ; pop rbp ; ret
0x000000000040075e : add byte ptr [rax], al ; push rbp ; mov rbp, rsp ; pop rbp ; jmp 0x4006f7
0x00000000004006e5 : add byte ptr [rax], r8b ; pop rbp ; ret
0x000000000040075f : add byte ptr [rbp + 0x48], dl ; mov ebp, esp ; pop rbp ; jmp 0x4006f6
0x0000000000400747 : add byte ptr [rcx], al ; pop rbp ; ret
0x00000000004006d9 : je 0x4006f0 ; pop rbp ; mov edi, 0x601068 ; jmp rax
0x000000000040071b : je 0x400730 ; pop rbp ; mov edi, 0x601068 ; jmp rax
0x0000000000400742 : mov byte ptr [rip + 0x20093f], 1 ; pop rbp ; ret
0x0000000000400762 : mov ebp, esp ; pop rbp ; jmp 0x4006f3
0x0000000000400761 : mov rbp, rsp ; pop rbp ; jmp 0x4006f4
0x00000000004006e3 : nop dword ptr [rax + rax] ; pop rbp ; ret
0x0000000000400725 : nop dword ptr [rax] ; pop rbp ; ret
0x0000000000400745 : or dword ptr [rax], esp ; add byte ptr [rcx], al ; pop rbp ; ret
0x000000000040092c : pop r12 ; pop r13 ; pop r14 ; pop r15 ; ret
0x000000000040092e : pop r13 ; pop r14 ; pop r15 ; ret
0x0000000000400930 : pop r14 ; pop r15 ; ret
0x0000000000400932 : pop r15 ; ret
0x0000000000400764 : pop rbp ; jmp 0x4006f1
0x00000000004006db : pop rbp ; mov edi, 0x601068 ; jmp rax
0x000000000040092b : pop rbp ; pop r12 ; pop r13 ; pop r14 ; pop r15 ; ret
0x000000000040092f : pop rbp ; pop r14 ; pop r15 ; ret
0x00000000004006e8 : pop rbp ; ret
0x0000000000400933 : pop rdi ; ret
0x0000000000400931 : pop rsi ; pop r15 ; ret
0x000000000040092d : pop rsp ; pop r13 ; pop r14 ; pop r15 ; ret
0x0000000000400760 : push rbp ; mov rbp, rsp ; pop rbp ; jmp 0x4006f5
kali@kali:~/damctf/allokay$ exit
```     

