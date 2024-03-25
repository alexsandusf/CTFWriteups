# wifi-basic

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/9e59cfdc-1a03-4af1-a67d-6fb049d58f25)

# Solution

For this challenge we are givin a pcap file as well as a python file to calcualte the flag

# Step 1:

We need to find three values bssid, essid, and psk.

We can use air-crack to solv the challenge 

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/68bd7e72-3eb9-4547-bedc-0a79748dac5a)

Just by running the pcap with aircrack we can get the BSSID as well as the ESSID. We just need to run it using rockyou to find the psk.

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/1691c3b7-6ec5-467f-8e94-119b7a7d51c3)

# Getting the flag

Now that we have all the values all we need to do is enter it into the given python program and run it to get the flag.


# Flag

CTF{73841584e4c011c940e91c76bf1c12a7a4850e4b3df0a27ba8a35388c316d468}
