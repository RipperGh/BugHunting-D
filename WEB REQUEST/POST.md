# POST

Unlike HTTP GET, which places user parameters within the URL, HTTP POST places user parameters within the HTTP Request body. This has three main benefits:

Lack of Logging: As POST requests may transfer large files (e.g. file upload), it would not be efficient for the server to log all uploaded files as part of the requested URL, as would be the case with a file uploaded through a GET request.
Less Encoding Requirements: URLs are designed to be shared, which means they need to conform to characters that can be converted to letters. The POST request places data in the body which can accept binary data. The only characters that need to be encoded are those that are used to separate parameters.
More data can be sent: The maximum URL Length varies between browsers (Chrome/Firefox/IE), web servers (IIS, Apache, nginx), Content Delivery Networks (Fastly, Cloudfront, Cloudflare), and even URL Shorteners (bit.ly, amzn.to). Generally speaking, a URL's lengths should be kept to below 2,000 characters, and so they cannot handle a lot of data.



# Login Forms
![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/4a73466b-ee63-4114-aa88-80ff5e949601)
If we try to login with admin:admin, we get in and see a similar search function to the one we saw earlier in the GET section:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/64a2173a-6911-40b1-ac21-7b4911dc3bb2)

If we clear the Network tab in our browser devtools and try to log in again, we will see many requests being sent. We can filter the requests by our server IP, so it would only show requests going to the web application's web server (i.e. filter out external requests), and we will notice the following POST request being sent:
![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/7654212a-b3a1-4e97-8eef-4371f4dff419)

 click on the Request tab (which shows the request body), and then click on the Raw button to show the raw request data. We see the following data is being sent as the POST request data:
 ```
username=admin&password=admin
```
We will use the -X POST flag to send a POST request. Then, to add our POST data, we can use the -d flag and add the above data after it, as follows:

Example of POST FLAG CMD
```
GhostRipper@htb[/htb]$ curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/

...SNIP...
        <em>Type a city name and hit <strong>Enter</strong></em>
...SNIP...
```
# Authenticated Cookies
 we were successfully authenticated, we should have received a cookie so our browsers can persist our authentication, and we don't need to login every time we visit the page. We can use the -v or -i flags to view the response, which should contain the Set-Cookie header with our authenticated cookie:

 Example output of CMD
 ```
GhostRipper@htb[/htb]$ curl -X POST -d 'username=admin&password=admin' http://<SERVER_IP>:<PORT>/ -i

HTTP/1.1 200 OK
Date: 
Server: Apache/2.4.41 (Ubuntu)
Set-Cookie: PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1; path=/

...SNIP...
        <em>Type a city name and hit <strong>Enter</strong></em>
...SNIP...
```
 we should now be able to interact with the web application without needing to provide our credentials every time. To test this, we can set the above cookie with the -b flag in cURL, as follows

 example of CMD 
 ```
GhostRipper@htb[/htb]$ curl -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/

...SNIP...
        <em>Type a city name and hit <strong>Enter</strong></em>
...SNIP...
```
As we can see, we were indeed authenticated and got to the search function. It is also possible to specify the cookie as a header, as follows:
```
curl -H 'Cookie: PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' http://<SERVER_IP>:<PORT>/
```
Then, we can go to the Storage tab in the devtools with [SHIFT+F9]. In the Storage tab, we can click on Cookies in the left pane and select our website to view our current cookies. We may or may not have existing cookies, but if we were logged out, then our PHP cookie should not be authenticated, which is why if we get the login form and not the search function:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/8a25e894-645b-445d-8e31-611ee1c6e389)

let's try to use our earlier authenticated cookie, and see if we do get in without needing to provide our credentials. To do so, we can simply replace the cookie value with our own. Otherwise, we can right-click on the cookie and select Delete All, and the click on the + icon to add a new cookie. After that, we need to enter the cookie name, which is the part before the = (PHPSESSID), and then the cookie value, which is the part after the = (c1nsa6op7vtk7kdis7bcnbadf1). Then, once our cookie is set, we can refresh the page, and we will see that we do indeed get authenticated without needing to login, simply by using an authenticated cookie:
![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/02ed1b0d-43d5-45c7-9f12-27bc2880976f)

# JSON Data

let's see what requests get sent when we interact with the City Search function. To do so, we will go to the Network tab in the browser devtools, and then click on the trash icon to clear all requests. Then, we can make any search query to see what requests get sent:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/67ee8ff7-99df-40f1-bfb5-3ae6a263cf41)

As we can see, the search form sends a POST request to search.php, with the following data:
```
{"search":"london"}
```
so our request must have specified the Content-Type header to be application/json. We can confirm this by right-clicking on the request, and selecting Copy>Copy Request Headers:
```
POST /search.php HTTP/1.1
Host: server_ip
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.15; rv:97.0) Gecko/20100101 Firefox/97.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Referer: http://server_ip/index.php
Content-Type: application/json
Origin: http://server_ip
Content-Length: 19
DNT: 1
Connection: keep-alive
Cookie: PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1
```
we do have Content-Type: application/json. Let's try to replicate this request as we did earlier, but include both the cookie and content-type headers, and send our request to search.php:

```
GhostRipper@htb[/htb]$ curl -X POST -d '{"search":"london"}' -b 'PHPSESSID=c1nsa6op7vtk7kdis7bcnbadf1' -H 'Content-Type: application/json' http://<SERVER_IP>:<PORT>/search.php
["London (UK)"]
```

Finally, let's try to repeat the same above request by using Fetch, as we did in the previous section. We can right-click on the request and select Copy>Copy as Fetch, and then go to the Console tab and execute our code there:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/8732350b-ac5d-4a81-88b8-6f29ef88ac57)

# Excerise

Question

 1) Obtain a session cookie through a valid login, and then use the cookie with cURL to search for the flag through a JSON POST request to '/search.php'

Target:
  94.237.54.170:32085

## What I did to get the answer
```
  1) curl -X POST -d 'username=admin&password=admin' http://94.237.54.170:32085/
    -  used this command to get the body of page uusing admin credentials

  2) url -X POST -d 'username=admin&password=admin' http://94.237.54.170:32085/ -v
    - then added -v ( Note: -i will also give sessionkey) to increase how in depth the information I was going to receive
    - I got the cookie session key which was  PHPSESSID=omegbov3qujnuqi0mo8lfi5h54;

  example of what happpen when you get cookie key
    - curl -b 'PHPSESSID=pr13rrl399rn7brlckbjrea3rs' http://94.237.54.170:32085/
    - curl -H 'Cookie: PHPSESSID=pr13rrl399rn7brlckbjrea3rs' http://94.237.54.170:32085/
    Both of these command allow me to skip authicating myself using admin:admin

  3) curl -X POST -d '{"search":"london"}' -b 'PHPSESSID=pr13rrl399rn7brlckbjrea3rs' -H 'Content-Type: application/json' http://94.237.54.170:32085/search.php
     - This allowed me to query the site to look for '{"search":"london"}, this is when I realized that I could change out london to look for flag
```
 ![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/53c63070-9024-412d-b6bd-b2aba0bed3dc)
 
These images show what I was trying to do before realizing what it was letting me do 
Answer
```
  4) curl -X POST -d '{"search":"flag"}' -b 'PHPSESSID=pr13rrl399rn7brlckbjrea3rs' -H 'Content-Type: application/json' http://94.237.54.170:32085/search.php
    ["flag: HTB{p0$t_r3p34t3r}"]
```
