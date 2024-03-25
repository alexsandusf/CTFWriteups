# Wifiland

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/ab6b5cd6-ee7a-4459-bb75-0bbbe5bf1616)

This problem is very similar to wifi-basic, but with a couple extra steps

# Soltuion

Again lets run aircrack on the file with rockyou so we can decrypt the pcap file and get each ip address

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/22440f8c-38b9-42b9-b367-484cacb500de)

Now we can use WEP and WPA decyption key section in wireshark to decrypt the packet

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/2dfc1c9f-98e1-414e-81e0-dc41d126b2b9)

We will eventually find an ARP packet which will give us both IPs

![image](https://github.com/alexsandusf/CTFWriteups/assets/162010016/d4cd96a3-6a65-4731-92c0-43fcdd862c6e)


# Getting flag
```python3

from hashlib import sha256

ip_client = "10.0.3.19"
ip_target = "93.184.216.34"

def calculate_sha256(ip_client, ip_target):

    input_string = ip_client + ip_target
    
    hash_result = sha256(input_string.encode()).hexdigest()
    
    return hash_result

sha256_sum = calculate_sha256(ip_client, ip_target)

print('CTF{'+sha256_sum+'}')
CTF{b67842d03eadce036c5506f2b7b7bd25aaab4d1f0ec4b4f490f0cb19ccd45c70}
```

