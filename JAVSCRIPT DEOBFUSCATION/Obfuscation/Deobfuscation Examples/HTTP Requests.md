# HTTP Requests
In the previous section, we found out that the secret.js main function is sending an empty POST request to /serial.php. In this section, we will attempt to do the same using cURL to send a POST request to /serial.php. To learn more about cURL and web requests, you can check out the Web Requests module.

# cURL
cURL is a powerful command-line tool used in Linux distributions, macOS, and even the latest Windows PowerShell versions. We can request any website by simply providing its URL, and we would get it in text-format, as follows:
```
GhostRipper@htb[/htb]$ curl http://SERVER_IP:PORT/

</html>
<!DOCTYPE html>

<head>
    <title>Secret Serial Generator</title>
    <style>
        *,
        html {
            margin: 0;
            padding: 0;
            border: 0;
...SNIP...
        <h1>Secret Serial Generator</h1>
        <p>This page generates secret serials!</p>
    </div>
</body>

</html>
```

This is the same HTML we went through when we checked the source code in the first section.

# POST Request
To send a POST request, we should add the -X POST flag to our command, and it should send a POST request:
```
GhostRipper@htb[/htb]$ curl -s http://SERVER_IP:PORT/ -X POST
```
However, POST request usually contains POST data. To send data, we can use the "-d "param1=sample"" flag and include our data for each parameter, as follows:
```
GhostRipper@htb[/htb]$ curl -s http://SERVER_IP:PORT/ -X POST -d "param1=sample"
```

# Execrise 

Question: Try applying what you learned in this section by sending a 'POST' request to '/serial.php'. What is the response you get?

Target: 94.237.57.59:58958

Answer: N2gxNV8xNV9hX3MzY3IzN19tMzU1NGcz

Reminder: Dont forget to add /serial.php to http://SERVER_IP:PORT/





