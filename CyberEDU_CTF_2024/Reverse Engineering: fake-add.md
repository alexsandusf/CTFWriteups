# fake-add

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/9d4f15ee-8196-4f14-9bbe-418022a319b2)

# Solution

First I opened it up in BinaryNinja, but you can also use dogbolt for this challenge

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/d5eea1d8-ccd4-4f5c-b029-f972d7797dc9)

These variables look interesting so lets see what they are

'<', (non-printable), '*', '*', ' ', '&', 'x', (non-printable), 'Z', (non-printable), 'h', (non-printable), ''', (newline), 'd', (non-printable), 'K', (non-printable), '_', (newline), 'd', (non-printable), 'U', (newline), 'U', (non-printable), 'U', ' ', '4', (non-printable), '*', '*', '5', '*', '!', ' ', '!', '#', '!', '#', 'd', (non-printable), 'C', 'T', 'F', '{', 't', 'h', '1', 's', '_', 'i', 's', '_', 'j', 'u', '5', 'T', '_', 'A', 'D', 'D', '}'

We can see these values contain the flag


# Flag

CTF{th1s_is_ju5T_ADD}
