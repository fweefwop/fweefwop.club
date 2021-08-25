+++
title = "Web Exploitation Tips"
date = "2021-08-05"
weight = 300
+++

### Web Exploitation Tips

1) Put a basic payload in all possible inputs: ```qwe'"<X</```. And just watch text reflection on a website. If you will see somewhere ```qwe'"```(without angle brackets), there is a chance of XSS. Additionally, search for "qwe" text in the source code of the page. Use Developers Tools in the browser for this task.   

2) You can use ```&#01;``` before javascript protocol to bypass XSS(cross-site scripting) protection in ```<a>``` tag. Example: ```<a href="&#01;javascript:alert(1)">```    

3) You can try to bypass the uploaded file extension block using these tricks ```file.html.``` (using dot at the end) or ```file.htm%6C``` (using encoded l)     

4) SSTI ( (Server Side Template Injection) Payload List:  ```{{7*7}}``` or ```${7*7}``` or 
```<%= 7*7 %>``` or  ```${{7*7}}``` or ```#{7*7}```. If evaluated as 49 - target can be vulnerable to XSS or even RCE.    




Credit to Anton@theceman