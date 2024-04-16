# Repeating Requests 

we successfully bypassed the input validation to use a non-numeric input to reach command injection on the remote server. If we want to repeat the same process with a different command, we would have to intercept the request again, provide a different payload, forward it again, and finally check our browser to get the final result.

As you can imagine, if we would do this for each command, it would take us forever to enumerate a system, as each command would require 5-6 steps to get executed. However, for such repetitive tasks, we can utilize request repeating to make this process significantly easier.

Request repeating allows us to resend any web request that has previously gone through the web proxy. This allows us to make quick changes to any request before we send it, then get the response within our tools without intercepting and modifying each request.

# Proxy History
To start, we can view the HTTP requests history in Burp at (Proxy>HTTP History):

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/b03c7556-92fe-44b4-a605-a1a763b5d62f)

In ZAP HUD, we can find it in the bottom History pane or ZAP's main UI at the bottom History tab as well:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/b263e7d4-45a2-41bf-94b9-8f4ea4026e59)

Both tools also provide filtering and sorting options for requests history, which may be helpful if we deal with a huge number of requests and want to locate a specific request. Try to see how filters work on both tools.

Note: Both tools also maintain WebSockets history, which shows all connections initiated by the web application even after being loaded, like asynchronous updates and data fetching. WebSockets can be useful when performing advanced web penetration testing, and are out of the scope of this module.

If we click on any request in the history in either tool, its details will be shown:

Burp:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/1550547a-49ce-4b3c-8752-46d36215066b)

ZAP:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/2b36ca37-c53e-4518-a4e4-49dec97d8dbc)

Tip: While ZAP only shows the final/modified request that was sent, Burp provides the ability to examine both the original request and the modified request. If a request was edited, the pane header would say Original Request, and we can click on it and select Edited Request to examine the final request that was sent.

# Repeating Requests
 ## Burp 
Once we locate the request we want to repeat, we can click [CTRL+R] in Burp to send it to the Repeater tab, and then we can either navigate to the Repeater tab or click [CTRL+SHIFT+R] to go to it directly. Once in Repeater, we can click on Send to send the request:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/5e554c7c-b34d-40cd-9660-7bfc1e58d222)

### Tip: We can also right-click on the request and select Change Request Method to change the HTTP method between POST/GET without having to rewrite the entire request.

## ZAP
In ZAP, once we locate our request, we can right-click on it and select Open/Resend with Request Editor, which would open the request editor window, and allow us to resend the request with the Send button to send our request:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/7053347e-54c5-4037-bb63-f585bbf23bfc)

We can also see the Method drop-down menu, allowing us to quickly switch the request method to any other HTTP method.

We can achieve the same result within the pre-configured browser with ZAP HUD. We can locate the request in the bottom History pane, and once we click on it, the Request Editor window will show, allowing us to resend it. We can select Replay in Console to get the response in the same HUD window, or select Replay in Browser to see the response rendered in the browser:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/f6bfd42a-8733-4339-9bba-07ca051f5ece)


###  Tip: By default, the Request Editor window in ZAP has the Request/Response in different tabs. You can click on the display buttons to change how they are organized. To match the above look choose the same display options shown in the screenshot.


## Request on both ZAP and Burps
So, let us try to modify our request and send it. In all three options (Burp Repeater, ZAP Request Editor, and ZAP HUD), we see that the requests are modifiable, and we can select the text we want to change and replace it with whatever we want, and then click the Send button to send it again:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/2ec9e2ae-7be3-46e4-be58-246ecaaf711b)


 As we can see, we could easily modify the command and instantly get its output by using Burp Repeater. Try doing the same in ZAP Request Editor and ZAP HUD to see how they work.

Finally, we can see in our previous POST request that the data is URL-encoded. This is an essential part of sending custom HTTP requests, which we will discuss in the next section.

## Excerise 

Question: Try using request repeating to be able to quickly test commands. With that, try looking for the other flag.

Target: 94.237.53.3:39302
