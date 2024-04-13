# HTML INJECTION

Another major aspect of front end security is validating and sanitizing accepted user input. In many cases, user input validation and sanitization is carried out on the back end. However, some user input would never make it to the back end in some cases and is completely processed and rendered on the front end. Therefore, it is critical to validate and sanitize user input on both the front end and the back end.

HTML injection occurs when unfiltered user input is displayed on the page. This can either be through retrieving previously submitted code, like retrieving a user comment from the back end database, or by directly displaying unfiltered user input through JavaScript on the front end.

user has complete control of how their input will be displayed, they can submit HTML code, and the browser may display it as part of the page.

This may include a malicious HTML code,
  - External Login form
which can be used to trick users into logging in while actually sending their login credentials to a malicious

# Example
The following example is a very basic web page with a single button "Click to enter your name." When we click on the button, it prompts us to input our name and then displays our name as "Your name is ...":

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/3455529c-4191-4810-95b1-856fd83c6471)

If no input sanitization is in place, this is potentially an easy target for HTML Injection and Cross-Site Scripting (XSS) attacks. We take a look at the page source code and see no input sanitization in place whatsoever, as the page takes user input and directly displays it:
```
Code: html
<!DOCTYPE html>
<html>

<body>
    <button onclick="inputFunction()">Click to enter your name</button>
    <p id="output"></p>

    <script>
        function inputFunction() {
            var input = prompt("Please enter your name", "");

            if (input != null) {
                document.getElementById("output").innerHTML = "Your name is " + input;
            }
        }
    </script>
</body>

</html>
```
To test for HTML Injection, we can simply input a small snippet of HTML code as our name, and see if it is displayed as part of the page. We will test the following code, which changes the background image of the web page:
```
Code: html
<style> body { background-image: url('https://academy.hackthebox.com/images/logo.svg'); } </style>
```
Once we input it, we see that the web page's background image changes instantly:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/60427b49-8939-4277-b6e9-e2d3a37d4be6)



# Exercise 

Question: What text would be displayed on the page if we use the following payload as our input: <a href="http://www.hackthebox.com">Click Me</a>

Target: 94.237.53.3:58811

Answer: Your name is Click Me


