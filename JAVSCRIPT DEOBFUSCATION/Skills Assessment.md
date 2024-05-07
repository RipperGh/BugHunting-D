# Skill Assessment
Target: 94.237.57.59:50628

1)  Try to study the HTML code of the webpage, and identify used JavaScript code within it. What is the name of the JavaScript file being used?

  Answer:api.min.js

  I just open the console to get the name of the javascript

2)  Once you find the JavaScript code, try to run it to see if it does any interesting functions. Did you get something in return?

  Answer:HTB{j4v45cr1p7_3num3r4710n_15_k3y}
I open the console aftewords and got the answer to this question

3) As you may have noticed, the JavaScript code is obfuscated. Try applying the skills you learned in this module to deobfuscate the code, and retrieve the 'flag' variable.

  Answer:HTB{n3v3r_run_0bfu5c473d_c0d3!}

I went to unpacker to using the html to get the answer to what the flag will be 
  
4) Try to Analyze the deobfuscated JavaScript code, and understand its main functionality. Once you do, try to replicate what it's doing to get a secret key. What is the key?

  Answer:4150495f70336e5f37333537316e365f31355f66756e

  Used curl http:/94.237.57.59:50628/keys.php -X POST -d "null" to get the key. I tried to think that just doing the command will help. I used the question of look at the 3 variables. We see xhr, keys, flag.
  I should of realize they keys was a php so all i need was keys.php to add to the cmd

I was able to get the key using 
  
5) Once you have the secret key, try to decide it's encoding method, and decode it. Then send a 'POST' request to the same previous page with the decoded key as "key=DECODED_KEY". What is the flag you got?

  Answer:HTB{r34dy_70_h4ck_my_w4y_1n_2_HTB}

  I decoded they key
  ```
hex decode 
echo 4150495f70336e5f37333537316e365f31355f66756e | xxd -p -r

API_p3n_73571n6_15_fun
curl  -X POST -d "key=API_p3n_73571n6_15_fun" http:/94.237.57.59:50628/keys.php
HTB{r34dy_70_h4ck_my_w4y_1n_2_HTB}

```

