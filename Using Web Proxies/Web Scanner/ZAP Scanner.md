# ZAP Scanner
ZAP also comes bundled with a Web Scanner similar to Burp Scanner. ZAP Scanner is capable of building site maps using ZAP Spider and performing both passive and active scans to look for various types of vulnerabilities.

# Spider
Let's start with ZAP Spider, which is similar to the Crawler feature in Burp. To start a Spider scan on any website, we can locate a request from our History tab and select (Attack>Spider) from the right-click menu
Another option is to use the HUD in the pre-configured browser. Once we visit the page or website we want to start our Spider scan on, we can click on the second button on the right pane (Spider Start), which would prompt us to start the scan:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/970b5967-d552-452c-bcb5-8e2e0736d98d)

Once we click on Start on the pop-up window, our Spider scan should start spidering the website by looking for links and validating them, very similar to how Burp Crawler works. We can see the progress of the spider scan both in the HUD on the Spider button or in the main ZAP UI, which should automatically switch to the current Spider tab to show the progress and sent requests. 

When our scan is complete, we can check the Sites tab on the main ZAP UI, or we can click on the first button on the right pane (Sites Tree), which should show us an expandable tree-list view of all identified websites and their sub-directories:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/86d8be57-2b05-4b9b-93d6-e1fbdd54929f)

# Passive Scanner
 ZAP Spider runs and makes requests to various end-points, it is automatically running its passive scanner on each response to see if it can identify potential issues from the source code, like missing security headers or DOM-based XSS vulnerabilities. This is why even before running the Active Scanner, we may see the alerts button start to get populated with a few identified issues. 

 The alerts on the left pane shows us issues identified in the current page we are visiting, while the right pane shows us the overall alerts on this web application, which includes alerts found on other pages:

 ![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/544d28e6-3bb3-4f6a-8f1a-1621b3ef063d)

 We can also check the Alerts tab on the main ZAP UI to see all identified issues. If we click on any alert, ZAP will show us its details and the pages it was found on:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/4c827176-f9c1-4e5c-9db3-d6a1a351c0cd)

# Active Scanner
 we can click on the Active Scan button on the right pane to start an active scan on all identified pages. If we have not yet run a Spider Scan on the web application, ZAP will automatically run it to build a site tree as a scan target. 

 Once the Active Scan starts, we can see its progress similarly to how we did with the Spider Scan:

 ![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/6176c0cb-2c8e-4e81-8295-bce49a628c1a)

 Active Scanner will try various types of attacks against all identified pages and HTTP parameters to identify as many vulnerabilities as it can.
 
 This is why the Active Scanner will take longer to complete. As the Active Scan runs, we will see the alerts button start to get populated with more alerts as ZAP uncovers more issues. 

 Furthermore, we can check the main ZAP UI for more details on the running scan and can view the various requests sent by ZAP:

 ![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/07352c3b-bf7c-45e9-834a-f3ae84d9cd3e)

 Once the Active Scan finishes, we can view the alerts to see which ones to follow up on. While all alerts should be reported and taken into consideration, the High alerts are the ones that usually lead to directly compromising the web application or the back-end server. If we click on the High Alerts button, it will show us the identified High Alert:

 ![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/066ffdd1-2c45-4ba7-8f04-f674e250af43)

 We can also click on it to see more details about it and see how we may replicate and patch this vulnerability:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/09dbf727-d9ce-4a7e-815b-64292f027599)

In the alert details window, we can also click on the URL to see the request and response details that ZAP used to identify this vulnerability, and we may also repeat the request through ZAP HUD or ZAP Request Editor:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/f5c12b88-e969-4c83-a118-263391952553)

# Reporting

Finally, we can generate a report with all of the findings identified by ZAP through its various scans. To do so, we can select (Report>Generate HTML Report) from the top bar, which would prompt us for the save location to save the report. We may also export the report in other formats like XML or Markdown. Once we generate our report, we can open it in any browser to view it:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/1c7aa8f7-438e-4a12-9289-c9f309cf6df3)

#Exercise 
Question: Run ZAP Scanner on the target above to identify directories and potential vulnerabilities. Once you find the high-level vulnerability, try to use it to read the flag at '/flag.txt'

Target: 83.136.253.251:53977

