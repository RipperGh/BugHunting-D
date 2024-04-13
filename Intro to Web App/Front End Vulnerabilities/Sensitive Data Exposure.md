# Sensitive Data Exposure

All of the front end components we covered are interacted with on the client-side. Therefore, if they are attacked, they do not pose a direct threat to the core back end of the web application and usually will not lead to permanent damage. However, as these components are executed on the client-side, they put the end-user in danger of being attacked and exploited if they do have any vulnerabilities.

majority of web application penetration testing is focused on back end components and their functionality, it is important also to test front end components for potential vulnerabilities, as these types of vulnerabilities can sometimes be utilized to gain access to sensitive functionality

Sensitive Data Exposure refers to the availability of sensitive data in clear-text to the end-user. 
  - Usually found in source code
  - This HTML source doe not back end code
  - Viewing Page Source in web browser
  - also can be vied in Burp Suite


Take a moment to browse the page source a bit.

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/8364093c-281c-422b-b5bd-fb57476da9ad)


Sometimes we may find login credentials, hashes, or other sensitive data hidden in the comments of a web page's source code or within external JavaScript code being imported. Other sensitive information may include exposed links or directories or even exposed user information, all of which can potentially be leveraged to further our access within the web application or even the web application's supporting infrastructure (webserver, database server, etc.).

## Example

At first glance, this login form does not look like anything out of the ordinary:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/3288a84a-6cde-4ff0-9f9d-6cc0c222c9ed)

Let's take a look at at the page source:

```
Code: html
<form action="action_page.php" method="post">

    <div class="container">
        <label for="uname"><b>Username</b></label>
        <input type="text" required>

        <label for="psw"><b>Password</b></label>
        <input type="password" required>

        <!-- TODO: remove test credentials test:test -->

        <button type="submit">Login</button>
    </div>
</form>

</html>
```
We see that the developers added some comments that they forgot to remove, which contain test credentials:
```
Code: html
<!-- TODO: remove test credentials test:test -->
```
The comment seems to be a reminder for the developers to remove the test credentials. Given that the comment has not been removed yet, these credentials may still be valid.

Although it is not very common to find login credentials in developer comments, we can still find various bits of sensitive and valuable information when looking at the source code, such as test pages or directories, debugging parameters, or hidden functionality. There are various automated tools that we can use to scan and analyze available page source code to identify potential paths or directories and other sensitive information.

# Prevention

Ideally, the front end source code should only contain the code necessary to run all of the web applications functions, without any extra code or comments that are not necessary for the web application to function properly. It is always important to review the code that will be visible to end-users through the page source or run it through tools to check for exposed information.
t is also important to classify data types within the source code and apply controls on what can or cannot be exposed on the client-side. Developers should also review client-side code to ensure that no unnecessary comments or hidden links are left behind.

# Exercise 
Questions: 
  Check the above login form for exposed passwords. Submit the password as the answer.

Target: 94.237.49.166:52405

Anwser: HiddenInPlainSight

  
