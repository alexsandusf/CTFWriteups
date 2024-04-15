

![Pasted image 20240412211510](https://github.com/alexsandusf/CTFWriteups/assets/162010016/95e0c040-ac91-4c26-abaf-7c5573205a2d)

The challenge for this linux jail was that we couldn't use certain symbles such as * " ' or the word "flag". My solution was to just use eval echo {a..z} which will print out letters a through z and eventually we will get to f and be able to print the word flag.

```bash

echo eval {a..z}lag.txt

```
