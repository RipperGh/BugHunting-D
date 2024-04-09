# Hypertext Transfer Protocol Secure (HTTPS)

If we examine an HTTP request, we can see the effect of not enforcing secure communications between a web browser and a web application. For example, the following is the content of an HTTP login request

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/29c107cf-1fad-461a-9dc0-2475bed445a4)

In contrast, when someone intercepts and analyzes traffic from an HTTPS request, they would see something like the following:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/3bb02bb6-9c82-43e5-ae8e-d356ef5e7474)


# HTTPS Flow

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/3ce268cb-fbfa-4ead-a5bb-54f959bddf44)

 **Note:** A request is sent to port 80 first, which is the unencrypted HTTP protocol. The server detects this and redirects the client to secure HTTPS port 443 instead. This is done via the 301 Moved Permanently response code, which we will discuss in an upcoming section.
 

# cURL for HTTPS

URL should automatically handle all HTTPS communication standards and perform a secure handshake and then encrypt and decrypt data automatically. However, if we ever contact a website with an invalid SSL certificate or an outdated one, then cURL by default would not proceed with the communication to protect against the earlier mentioned MITM attacks:

Example of cURL of HTTPS
```
GhostRipper@htb[/htb]$ curl https://inlanefreight.com

curl: (60) SSL certificate problem: Invalid certificate chain
More details here: https://curl.haxx.se/docs/sslcerts.html
```

Using cURL for HTTPS site using -k
  * -k : skip the certificatation
```
GhostRipper@htb[/htb]$ curl -k https://inlanefreight.com

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
```







