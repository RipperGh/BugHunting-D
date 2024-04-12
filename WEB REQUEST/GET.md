## GET 
ET request to obtain the remote resources hosted at that URL. Once the browser receives the initial page it is requesting; it may send other requests using various HTTP methods. This can be observed through the Network tab in the browser devtools, as seen in the previous section.

## HTTP BASIC AUTH 

Unlike the usual login forms, which utilize HTTP parameters to validate the user credentials (e.g. POST request), this type of authentication utilizes a basic HTTP authentication, which is handled directly by the webserver to protect a specific page/directory, without directly interacting with the web application.

CMD example off curl 
```
GhostRipper@htb[/htb]$ curl -i http://<SERVER_IP>:<PORT>/
HTTP/1.1 401 Authorization Required
Date: Mon, 21 Feb 2022 13:11:46 GMT
Server: Apache/2.4.41 (Ubuntu)
Cache-Control: no-cache, must-revalidate, max-age=0
WWW-Authenticate: Basic realm="Access denied"
Content-Length: 13
Content-Type: text/html; charset=UTF-8

Access denied
```
we get Access denied in the response body, and we also get Basic realm="Access denied" in the WWW-Authenticate header, which confirms that this page indeed uses basic HTTP auth, as discussed in the Headers section. To provide the credentials through cURL, we can use the -u flag, as follows:

Example of -u usage in curl cmd 
```
GhostRipper@htb[/htb]$ curl -u admin:admin http://<SERVER_IP>:<PORT>/

<!DOCTYPE html>
<html lang="en">

<head>
...SNIP...
````

Basic HTTP auth using credentials 
```
GhostRipper@htb[/htb]$ curl http://admin:admin@<SERVER_IP>:<PORT>/

<!DOCTYPE html>
<html lang="en">

<head>
...SNIP...
```
## HTTP Authorization Header
```
GhostRipper@htb[/htb]$ curl -v http://admin:admin@<SERVER_IP>:<PORT>/

*   Trying <SERVER_IP>:<PORT>...
* Connected to <SERVER_IP> (<SERVER_IP>) port PORT (#0)
* Server auth using Basic with user 'admin'
> GET / HTTP/1.1
> Host: <SERVER_IP>
> Authorization: Basic YWRtaW46YWRtaW4=
> User-Agent: curl/7.77.0
> Accept: */*
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 200 OK
< Date: Mon, 21 Feb 2022 13:19:57 GMT
< Server: Apache/2.4.41 (Ubuntu)
< Cache-Control: no-store, no-cache, must-revalidate
< Expires: Thu, 19 Nov 1981 08:52:00 GMT
< Pragma: no-cache
< Vary: Accept-Encoding
< Content-Length: 1453
< Content-Type: text/html; charset=UTF-8
< 

<!DOCTYPE html>
<html lang="en">

<head>
...SNIP...
```
basic HTTP auth, we see that our HTTP request sets the Authorization header to Basic YWRtaW46YWRtaW4=, which is the base64 encoded value of admin:admin. If we were using a modern method of authentication (e.g. JWT), the Authorization would be of type Bearer and would contain a longer encrypted token.

Another example of manaul authorization without supplying credentials using -H to stup header
```
GhostRipper@htb[/htb]$ curl -H 'Authorization: Basic YWRtaW46YWRtaW4=' http://<SERVER_IP>:<PORT>/

<!DOCTYPE html
<html lang="en">

<head>
...SNIP...
```
## GET Parameters
Once we are authenticated, we get access to a City Search function, in which we can enter a search term and get a list of matching cities:
![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/abb2a633-1ce5-457d-a4bb-34a747a0a518)

To verify this, we can open the browser devtools and go to the Network tab, or use the shortcut [CTRL+SHIFT+E] to get to the same tab. Before we enter our search term and view the requests, we may need to click on the trash icon on the top left, to ensure we clear any previous requests and only monitor newer requests:
![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/d134ecc2-88c7-42a4-a393-4fbd1f3d29be)

After that, we can enter any search term and hit enter, and we will immediately notice a new request being sent to the backend
![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/c11b1287-38f5-46d9-a571-ad067e0e5202)

we click on the request, it gets sent to search.php with the GET parameter search=le used in the URL. This helps us understand that the search function requests another page for the results.
we can send the same request directly to search.php to get the full search results, though it will probably return them in a specific format (e.g. JSON) without having the HTML layout shown in the above screenshot.
To send a GET request with cURL, we can use the exact same URL seen in the above screenshots since GET requests place their parameters in the URL. However, browser devtools provide a more convenient method of obtaining the cURL command. We can right-click on the request and select Copy>Copy as cURL. Then, we can paste the copied command in our terminal and execute it, and we should get the exact same response:


```
GhostRipper@htb[/htb]$ curl 'http://<SERVER_IP>:<PORT>/search.php?search=le' -H 'Authorization: Basic YWRtaW46YWRtaW4='

Leeds (UK)
Leicester (UK)
```

We can also repeat the exact request right within the browser devtools, by selecting Copy>Copy as Fetch. This will copy the same HTTP request using the JavaScript Fetch library. Then, we can go to the JavaScript console tab by clicking [CTRL+SHIFT+K], paste our Fetch command, and hit enter to send the request:
![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/65760668-779e-40f0-87e8-41605ffabd54)


# Example Exercise 
Question: 
  The exercise above seems to be broken, as it returns incorrect results. Use the browser devtools to see what is request it is sending when we search, and use cURL to search for 'flag' and obtain the flag.

Target:http:94.237.54.170:48871

**Note to self** 
  Remember that when you were doing 
```  
  if
  
  curl 94.237.54.170:48871, you will get access denied
  
  but
  
  curl -u admin:admin 94.237.54.170:48871, gave a response of 200(connected)
  
  still, no answer to flag 
  
  after looking I realize that 
  
  curl -u admin:admin "http://94.237.54.170:48871/search.php?*search=flag/HTB*"
  
  I started to look for everything with php database since it allows me to search for other information
  ```
Answer:
  HTB{curl_g3773r}

