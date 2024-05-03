# Exercise 

Question: Using what you learned in this section, run a parameter fuzzing scan on this page. what is the parameter accepted by this webpage?

Target: 94.237.58.148:59217

Answer: user

### This is a summarry what I had to do for the question at the bottom 

I was able to get the answer after a few steps 

1) I had to add the domains being asked so I added using sudo nano /etc/hosts
   ```
   94.237.58.148 academy.htb admin.academy.htb test.academy.htb faculty.academy.htb
   ````
   - I used ctrl-o and press enter to save the file
   - Then ctrl-x to save it, will give one more option pressedd y to accept change

2) After I was able to use the command to look for thing but I forgot to add ip address at the end 
   ```
   ffuf -w /opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://admin.academy.htb:59217/admin/admin.php?FUZZ=key -fs xxx
   ```
     - I forgot to add port at the end of address
     - I got an answer after getting a port, after I was able to figure out what -fs to filter out
       - it showed -fs 0, shows 798 as responise size, after I changed it
     - shows user as an option which is the answer 
