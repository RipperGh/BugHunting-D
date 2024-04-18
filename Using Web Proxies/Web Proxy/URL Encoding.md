# URL Encoding
t is essential to ensure that our request data is URL-encoded and our request headers are correctly set. Otherwise, we may get a server error in the response. This is why encoding and decoding data becomes essential as we modify and repeat web requests. Some of the key characters we need to encode are:
  - Spaces: May indicate the end of request data if not encoded
  - &: Otherwise interpreted as a parameter delimiter
  - #: Otherwise interpreted as a fragment identifier

To URL-encode text in Burp Repeater, we can select that text and right-click on it, then select (Convert Selection>URL>URL encode key characters), or by selecting the text and clicking [CTRL+U]. Burp also supports URL-encoding as we type if we right-click and enable that option, which will encode all of our text as we type it.

On the other hand, ZAP should automatically URL-encode all of our request data in the background before sending the request, though we may not see that explicitly.

There are other types of URL-encoding, like Full URL-Encoding or Unicode URL encoding, which may also be helpful for requests with many special characters.

# Decoding
While URL-encoding is key to HTTP requests, it is not the only type of encoding we will encounter. It is very common for web applications to encode their data, so we should be able to quickly decode that data to examine the original text. On the other hand, back-end servers may expect data to be encoded in a particular format or with a specific encoder, so we need to be able to quickly encode our data before we send it.

The following are some of the other types of encoders supported by both tools:
  - HTML
  - Unicode
  - Base64
  - ASCII hex

To access the full encoder in Burp, we can go to the Decoder tab. In ZAP, we can use the Encoder/Decoder/Hash by clicking [CTRL+E]. With these encoders, we can input any text and have it quickly encoded or decoded. For example, perhaps we came across the following cookie that is base64 encoded, and we need to decode it: eyJ1c2VybmFtZSI6Imd1ZXN0IiwgImlzX2FkbWluIjpmYWxzZX0=

We can input the above string in Burp Decoder and select Decode as > Base64, and we'll get the decoded value:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/1cff2728-887f-4170-995a-ca6ff93aa8f0)

In recent versions of Burp, we can also use the Burp Inspector tool to perform encoding and decoding (among other things), which can be found in various places like Burp Proxy or Burp Repeater:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/28d4f611-beb5-4aae-a260-0b5f3b60396b)

In ZAP, we can use the Encoder/Decoder/Hash tool, which will automatically decode strings using various decoders in the Decode tab:

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/71341a01-b46c-4771-91d8-970723b2f9be)

### Tip: We can create customized tabs in ZAP's Encoder/Decoder/Hash with the "Add New Tab" button, and then we can add any type of encoder/decoder we want the text to be shown in. Try to create your own tab with a few encoders/decoders.

# Encoding
As we can see, the text holds the value {"username":"guest", "is_admin":false}.

if we were performing a penetration test on a web application and find that the cookie holds this value, we may want to test modifying it to see whether it changes our user privileges. 

So, we can copy the above value, change guest to admin and false to true, and try to encode it again using its original encoding method (base64):

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/ba6d9f44-2c03-41b0-ba2e-fad615a7b8f4)

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/49b5716d-f20d-4d86-8d6a-e84bdb5cb825)

### Tip: Burp Decoder output can be directly encoded/decoded with a different encoder. Select the new encoder method in the output pane at the bottom, and it will be encoded/decoded again. In ZAP, we can copy the output text and paste it in the input field above.

# Excerise 

Question: The string found in the attached file has been encoded several times with various encoders. Try to use the decoding tools we discussed to decode it and get the flag.

Target: encoded_flag.zip

Answer: HTB{3nc0d1n6_n1nj4}

how I got to answer was 
1) Decode Value in encoded flag using base64, did it a total of 4 times 

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/3818933b-6e83-4457-ad83-7933420c61ae)

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/72331742-b16d-45d9-ac78-749bced28268)

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/6c95fb0b-7531-4f10-80bc-3add08e5119b)

2) afterwards I decode using  ASCII values and then with binary to get an answer
![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/d581ef9b-4dfc-4e9e-94d2-f5e4c73168cc)

![image](https://github.com/RipperGh/BugHunting-D/assets/165308866/247b3844-0587-410c-ab5e-4c4e9f9a1c2f)


