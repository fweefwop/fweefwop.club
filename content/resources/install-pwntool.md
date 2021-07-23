+++
title = "Binary Exploitation 2: Install Pwntools and Gef"
date = "2020-10-31"
weight = 500
+++

### Install pwntools ###

Pwntools is available as a pip package.
```html
$ sudo apt-get update
$ sudo apt-get install python3 python3-dev python3-pip git
$ sudo pip3 install --upgrade git+https://github.com/arthaud/python3-pwntools.git
```   
### Make sure ```$PATHONPATH``` is updated with your Python path

Add the following line into your ```~/.bashrc```  or just run it directly:
```html
export PYTHONPATH="$PYTHONPATH:$HOME/.python"
source ~/.bashrc
```

### Setup Gef 

***Gef*** is a python add-on to GDB to make binary exploitation easier.
https://gef.readthedocs.io/en/master/

### Install Gef
make sure you have ***GDB 7.7 or higher***.    
```html    
# via the install script
$ wget -q -O- https://github.com/hugsy/gef/raw/master/scripts/gef.sh | sh

# manually
$ wget -O ~/.gdbinit-gef.py -q https://github.com/hugsy/gef/raw/master/gef.py
$ echo source ~/.gdbinit-gef.py >> ~/.gdbinit
```    
