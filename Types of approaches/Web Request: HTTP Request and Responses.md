# HTTP Requests and Responses

An HTTP request is made by the client (e.g. cURL/browser), and is processed by the server (e.g. web server). The requests contain all of the details we require from the server, including the resource (e.g. URL, path, parameters), any request data, headers or options we specify, and many other options we will discuss throughout this module.

# HTTP Request 
![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/e089383f-542e-4ce1-9e89-894836ee36a9)

URL: http://inlanefreight.com/users/login.html

Field|Example|Description
* Method	|GET| The HTTP method or verb, which specifies the type of action to perform.
* Path |/users/login.html|The path to the resource being accessed. This field can also be suffixed with a query string (e.g. ?username=user).
* Version|HTTP/1.1|The third and final field is used to denote the HTTP version.

# HTTP Response
![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/b038aa39-061a-4365-be84-b2b9f825a53f)

1) The first being the HTTP version (e.g. HTTP/1.1), and the second denotes the HTTP response code (e.g. 200 OK).
2) After the first line, the response lists its headers, similar to an HTTP request. Both request and response headers are discussed in the next section.
3) Finally, the response may end with a response body, which is separated by a new line after the headers. The response body is usually defined as HTML code. However, it can also respond with other code types such as JSON,


# cURL 
```
GhostRipper@htb[/htb]$ curl inlanefreight.com -v

*   Trying SERVER_IP:80...
* TCP_NODELAY set
* Connected to inlanefreight.com (SERVER_IP) port 80 (#0)
> GET / HTTP/1.1
> Host: inlanefreight.com
> User-Agent: curl/7.65.3
> Accept: */*
> Connection: close
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 401 Unauthorized
< Date: Tue, 21 Jul 2020 05:20:15 GMT
< Server: Apache/X.Y.ZZ (Ubuntu)
< WWW-Authenticate: Basic realm="Restricted Content"
< Content-Length: 464
< Content-Type: text/html; charset=iso-8859-1
< 
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
```

# Browser DevTools

Most modern web browsers come with built-in developer tools (DevTools), which are mainly intended for developers to test their web applications. However, as web penetration testers, these tools can be a vital asset in any web assessment we perform, as a browser (and its DevTools) are among the assets we are most likely to have in every web assessment exercise. In this module, we will also discuss how to utilize some of the basic browser devtools to assess and monitor different types of web requests.


![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/4ba5cf54-b632-4a1a-a566-441e88921e60)


