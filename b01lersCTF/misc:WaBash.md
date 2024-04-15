## WaBash
-------------------------------
![Pasted image 20240412195114 1](https://github.com/alexsandusf/CTFWriteups/assets/162010016/0586ca12-a42b-45cd-b6bf-84d301da140b)


This was a fun linux jail challenge during b01lersCTF where all commands and spaces were added with "wa". For example trying to use cat would lead to wacat

My solution was to use $ to create a seperate command followed by cat<flag.txt which will print the flag without using a space

```bash
Soltuion: $a$(cat<flag.txt)
```
