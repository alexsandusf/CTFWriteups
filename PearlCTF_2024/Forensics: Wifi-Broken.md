### Problem:
WiFi broken

### Description: 
I suspect my former friend is upto something wrong. I tried to access his network but for that, I need the password to his wifi. Enclose the password in pearl{} when you find it.

---------------------------------------------------------------------------------------

All we need to do for this one is use aircrack to find the key.

aircrack-ng 'findme.cap' -w rockyou.txt

This will find the key which is also the flag

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/91be4039-e55c-4584-9e84-07ef56127fee)

