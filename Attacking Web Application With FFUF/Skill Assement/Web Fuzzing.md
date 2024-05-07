# Skill Assessment

Target: 94.237.53.3:44036

1) Run a sub-domain/vhost fuzzing scan on '*.academy.htb' for the IP shown above. What are all the sub-domains you can identify? (Only write the sub-domain name)

  Answer: test archive faculty

  How I got the answer
  ```
  ffuf -w /opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://academy.htb:PORT/ -H 'Host: FUZZ.academy.htb' -fs 985

  reminder everytime make sure you either sudo nano / sudo vim /etc/hosts since it doesn't auto-do it. You need to add IP academy.htb and dont forget to add the rest of
  the domains that you found 

  ```

2) Before you run your page fuzzing scan, you should first run an extension fuzzing scan. What are the different extensions accepted by the domains?

  Answer: .php .phps .php7
  
  ```
  ffuf -w /opt/useful/SecLists/Discovery/Web-Content/web-extensions.txt:FUZZ -u http://academy.htb:PORT/indexFUZZ

  Remember when you add the different sub-domains, you are also going to have to queriy the rest using the command from above
  you will get some stuff but not in others. Make sure you look through all of them in order to get an extra extention also dont forgt to using filter to get the answe you   want
  ```

3) One of the pages you will identify should say 'You don't have access!'. What is the full page URL?

  Answer: http://faculty.academy.htb:PORT/courses/linux-security.php7
  
  ```
  ffuf -w /opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://subdomain.academy.htb:PORT/FUZZ -recursion -recursion-depth 1 -e .php -v  

  Reminder: This will go through all the different type of pages that can be fuzzed, you will get courses so you are going to add it at the end and retry 
    
  ``` 

4)  In the page from the previous question, you should be able to find multiple parameters that are accepted by the page. What are they?

  Answer: user username

```
ffuf -w /opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://faculty.academy.htb:PORT/courses/linux-security.php7 -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded'

Reminder: Make sure you using filtering of some sort to be able to get the names of the username parameter 
```
  

5) Try fuzzing the parameters you identified for working values. One of them should return a flag. What is the content of the flag?

  Answer:HTB{w3b_fuzz1n6_m4573r}

  ```
  ffuf -w /opt/useful/SecLists/Usernames/xato-net-10-million-usernames.txt:FUZZ -u http://faculty.academy.htb:30401/courses/linux-security.php7 -X POST -d 'username=FUZZ' -   H 'Content-Type: application/x-www-form-urlencoded'

  Reminder: You also need to curl to get the page/answer to get the flag 

  Curl http://faculty.academy.htb:30401/courses/linux-security.php7 -X POST -d 'username=answer' -   H 'Content-Type: application/x-www-form-urlencoded'
```
