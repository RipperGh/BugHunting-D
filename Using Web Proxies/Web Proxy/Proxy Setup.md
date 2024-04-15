# Proxy Setup

We can set up these tools as a proxy for any application, such that all web requests would be routed through them so that we can manually examine what web requests an application is sending and receiving. This will enable us to understand better what the application is doing in the background and allows us to intercept and change these requests or reuse them with various changes to see how the application responds.

# Pre-Configured Browser
To use the tools as web proxies, we must configure our browser proxy settings to use them as the proxy or use the pre-configured browser. Both tools have a pre-configured browser that comes with pre-configured proxy settings and the CA certificates pre-installed, making starting a web penetration test very quick and easy.

In Burp's (Proxy>Intercept), we can click on Open Browser, which will open Burp's pre-configured browser, and automatically route all web traffic through Burp:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/c833df3c-e4ce-40ee-9774-27b27f726072)

In ZAP, we can click on the Firefox browser icon at the end of the top bar, and it will open the pre-configured browser:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/86a0169a-d49f-41cc-8a47-e98b1f6258ba)

## Proxy Setup

In many cases, we may want to use a real browser for pentesting, like Firefox. To use Firefox with our web proxy tools, we must first configure it to use them as the proxy. We can manually go to Firefox preferences and set up the proxy to use the web proxy listening port. Both Burp and ZAP use port 8080 by default, but we can use any available port. If we choose a port that is in use, the proxy will fail to start, and we will receive an error message.

Note: In case we wanted to serve the web proxy on a different port, we can do that in Burp under (Proxy>Options), or in ZAP under (Tools>Options>Local Proxies). In both cases, we must ensure that the proxy configured in Firefox uses the same port.

Instead of manually switching the proxy, we can utilize the Firefox extension Foxy Proxy to easily and quickly change the Firefox proxy. This extension is pre-installed in your PwnBox instance and can be installed to your own Firefox browser by visiting the Firefox Extensions Page and clicking Add to Firefox to install it.

Once we have the extension added, we can configure the web proxy on it by clicking on its icon on Firefox top bar and then choosing options:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/3fb1d295-f4f1-4d37-883b-1fa0136c9ab9)

Once we're on the options page, we can click on add on the left pane, and then use 127.0.0.1 as the IP, and 8080 as the port, and name it Burp or ZAP:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/83162bf1-58ee-45a5-b0f2-f855e32df739)

Note: This configuration is already added to Foxy Proxy in PwnBox, so you don't have to do this step if you are using PwnBox.

Finally, we can click on the Foxy Proxy icon and select Burp/ZAP.

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/673710cc-fdfb-4776-869d-35c064ac8348)

# Installing CA Certificate 
Another important step when using Burp Proxy/ZAP with our browser is to install the web proxy's CA Certificates. If we don't do this step, some HTTPS traffic may not get properly routed, or we may need to click accept every time Firefox needs to send an HTTPS request.

We can install Burp's certificate once we select Burp as our proxy in Foxy Proxy, by browsing to http://burp, and download the certificate from there by clicking on CA Certificate:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/89e96b53-03ac-4542-9c74-cda9f4ae10ba)

To get ZAP's certificate, we can go to (Tools>Options>Dynamic SSL Certificate), then click on Save:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/a5eb8f06-869f-4622-a5fe-cb6b373f5baf)

We can also change our certificate by generating a new one with the Generate button.

Once we have our certificates, we can install them within Firefox by browsing to about:preferences#privacy, scrolling to the bottom, and clicking View Certificates:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/97554e57-5dbc-4966-9c5f-520c03509af0)

After that, we can select the Authorities tab, and then click on import, and select the downloaded CA certificate:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/10bebae0-ecbb-4091-9d9d-98ef8e309434)

Finally, we must select Trust this CA to identify websites and Trust this CA to identify email users, and then click OK:
![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/769fb022-b4c2-4f2e-8526-728615612e6c)









