# OverTheWire: Bandit Walkthrough

**Connection Details:**
* Host: `bandit.labs.overthewire.org`
* Port: `2220`
* Initial Credentials: `bandit0` / `bandit0`

---

## Level 0 -> Level 1
**Password:** `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`
**Objective:** Read the readme file
![Figure 1: Level 0 -> Level 1](/images/bandit0.png)
```
cat readme
```
## Level 1 -> Level 2
**Password:** `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`
**Objective:** read dashed file name (-)
![Figure 2: Level 1 -> Level 2](/images/bandit1_2.png)
```
cat ./-
```
why not cat -? "-" is treated as a flag in linux and assumes you want to add extra options to the cat program like cat -h
for example, the "./" ensures the os knows its a path not a flag option.


## Level 2 -> Level 3
**Password:** `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`
**Objective:** read dashed and spaced file name "--spaces in this filename--"
![Figure 3: Level 2 -> Level 3](/images/bandit2_3.png)
```
cat ./--spaces\ in\ this\ filename--
```
why the backslash \? the backslash escapes the special meaning of the space in linux (as a seperator), the backslash tells the os that the space is not a command but part of the file's name

## Level 3 -> Level 4
**Password:** `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`
**Objective:** navigate to folder then find hidden file
![Figure 4: Level 3 -> Level 4](/images/bandit3_4.png)

```
cd inhere
ls 
ls -la (to show all hidden files)
cat ./...Hiding-From-You
```

## Level 4 -> Level 5
**Password:** `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`
**Objective:** find the only file that is human readable
![Figure 4: Level 4 -> Level 5](/images/bandit4_5.png)
```
ls
cd inhere/
ls
ls -la
file ./-file*
(the * is a wildcard meaning anything can be here also length doesn't matter the * can be a bunch of characters but the -file section has to match, this will give you an output of what each file is, look for the text file)
cat ./-file07

```

## Level 5 -> Level 6
**Password:** `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`
**Objective:** find file in the in here directory with size 1033 bytes human readable and not executable

![Figure 5: Level 5 -> Level 6](/images/bandit5_6.png)

```
cd inhere/
cd maybehere00
cd ../
find -readable -size 1033c (couldn't find a way to search by non executable)
cat ./maybehere07/.file2
```

## Level 6 -> Level 7
**Password:** `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`
**Objective:** The password for the next level is stored somewhere on the server and has all of the following properties:

owned by user bandit7
owned by group bandit6
33 bytes in size
![Figure 5: Level 6 -> Level 7](/images/bandit6_7.png)
![Figure 5: Level 6 -> Level 7](/images/username_find_man.png)
![Figure 5: Level 6 -> Level 7](/images/group_find_man.png)
![Figure 5: Level 6 -> Level 7](/images/size_find_man.png)



```
ls
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```
why 2>/dev/null?
2 is standard error output while 1 is standard output, basically telling the
program or binary to send all error outputs like permission denied to the
shredder a.k.a /dev/null
and c in 33c stands for bytes

## Level 7 -> Level 8
**Password:** `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`
**Objective:** The password for the next level is stored in the file 
data.txt next to the word millionth

![Figure 6: Level 7 -> Level 8](/images/bandit7_8.png)

```
ls
cat data.txt (dont, dont make the same mistake I did please)
grep millionth data.txt
or
cat data.txt | grep millionth
```
Either way works the | operator just pipes or feeds the output from a specific program
or binary to another binary usualy, in this case grep binary which filters through 
whatever you gave it plus extra filters if you want

## Level 8 -> Level 9
**Password:** `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM`
**Objective:** The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

![Figure 7: Level 8 -> Level 9](/images/bandit8_9.png)

```
ls
cat data.txt
sort data.txt | uniq -u
```
I tried uniq -u and sort -u however only after sorting the text to show all
the duplicates only then should you pipe it "|" to uniq -u since uniq only
works if the lines are next to each other
## Level 9 -> Level 10
**Password:** `FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey`
**Objective:** The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.
![Figure 8: Level 9 -> Level 10](/images/bandit9_10.png)

```
ls
cat data.txt
strings data.txt | grep =
```
I tried sort but strings is basically built for human readable text, you can
use it even against binaries to find human readable well ... strings I then
piped it into grep for the = sign (might not have been the correct metho but
it worked)

## Level 10 -> Level 11
**Password:** `dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr`
**Objective:** The password for the next level is stored in the file data.txt, which contains base64 encoded data
![Figure 9: Level 10 -> Level 11](/images/bandit10_11.png)


```
ls
cat data.txt
cat data.txt | base64 -d
```
base64 is a type of encoding, the -d option is to decode

## Level 11 -> Level 12
**Password:** `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`

**Objective:** The password for the next level is stored in the file data.txt, 
where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

![Figure 10: Level 11 -> Level 12](/images/bandit11_12.png)

```
 cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
Rot 13 is when the letter have been shiften by 13 letters 
its a weak form of encryption called a ceaser cipher

The 'A-Za-z' is what tr should look for and N is 'a' + 13 spaces and A is 'n' plus 13 because
its one more than 'z' therfore it wraps around back to 'a'

## Level 12 -> Level 13
**Password:** `FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn`

**Objective:** The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command “mktemp -d”. Then copy the datafile using cp, and rename it using mv (read the manpages!)

![Figure 11: Level 12 -> Level 13](/images/bandit12_13.png)

```
ls
cat data.txt
xxd -r data.txt
##(here you must check what the file is and rename it with the specific extension
##.bz2 for bzip2 .gz for gunzip .tar for tar)
file data.bin
## then rename using mv
mv blabla or to blabla.gz .bz2 or .tar
## repeat until you find a ASCII text file where you will see the password

```
xxd is a binary that both makes and reverses hexdumps, we'll use it to reverse the hexdump to a binary again. Why binary? because a hexdump is usualy taken of a binary, a hexdump shows the raw bytes of the file represented in hexadecimal (base-16) each byte being represented by two digit hexadecimal numbers (00 - FF) FF being the highest hexadecimal goes to (0,1,2,3,4,5,6,7,8,9,A,B,C,D,E,F)

## Level 13 -> Level 14
**Password:** 
```
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEAxkkOE83W2cOT7IWhFc9aPaaQmQDdgzuXCv+ppZHa++buSkN+
gg0tcr7Fw8NLGa5+Uzec2rEg0WmeevB13AIoYp0MZyETq46t+jk9puNwZwIt9XgB
ZufGtZEwWbFWw/vVLNwOXBe4UWStGRWzgPpEeSv5Tb1VjLZIBdGphTIK22Amz6Zb
ThMsiMnyJafEwJ/T8PQO3myS91vUHEuoOMAzoUID4kN0MEZ3+XahyK0HJVq68KsV
ObefXG1vvA3GAJ29kxJaqvRfgYnqZryWN7w3CHjNU4c/2Jkp+n8L0SnxaNA+WYA7
jiPyTF0is8uzMlYQ4l1Lzh/8/MpvhCQF8r22dwIDAQABAoIBAQC6dWBjhyEOzjeA
J3j/RWmap9M5zfJ/wb2bfidNpwbB8rsJ4sZIDZQ7XuIh4LfygoAQSS+bBw3RXvzE
pvJt3SmU8hIDuLsCjL1VnBY5pY7Bju8g8aR/3FyjyNAqx/TLfzlLYfOu7i9Jet67
xAh0tONG/u8FB5I3LAI2Vp6OviwvdWeC4nOxCthldpuPKNLA8rmMMVRTKQ+7T2VS
nXmwYckKUcUgzoVSpiNZaS0zUDypdpy2+tRH3MQa5kqN1YKjvF8RC47woOYCktsD
o3FFpGNFec9Taa3Msy+DfQQhHKZFKIL3bJDONtmrVvtYK40/yeU4aZ/HA2DQzwhe
ol1AfiEhAoGBAOnVjosBkm7sblK+n4IEwPxs8sOmhPnTDUy5WGrpSCrXOmsVIBUf
laL3ZGLx3xCIwtCnEucB9DvN2HZkupc/h6hTKUYLqXuyLD8njTrbRhLgbC9QrKrS
M1F2fSTxVqPtZDlDMwjNR04xHA/fKh8bXXyTMqOHNJTHHNhbh3McdURjAoGBANkU
1hqfnw7+aXncJ9bjysr1ZWbqOE5Nd8AFgfwaKuGTTVX2NsUQnCMWdOp+wFak40JH
PKWkJNdBG+ex0H9JNQsTK3X5PBMAS8AfX0GrKeuwKWA6erytVTqjOfLYcdp5+z9s
8DtVCxDuVsM+i4X8UqIGOlvGbtKEVokHPFXP1q/dAoGAcHg5YX7WEehCgCYTzpO+
xysX8ScM2qS6xuZ3MqUWAxUWkh7NGZvhe0sGy9iOdANzwKw7mUUFViaCMR/t54W1
GC83sOs3D7n5Mj8x3NdO8xFit7dT9a245TvaoYQ7KgmqpSg/ScKCw4c3eiLava+J
3btnJeSIU+8ZXq9XjPRpKwUCgYA7z6LiOQKxNeXH3qHXcnHok855maUj5fJNpPbY
iDkyZ8ySF8GlcFsky8Yw6fWCqfG3zDrohJ5l9JmEsBh7SadkwsZhvecQcS9t4vby
9/8X4jS0P8ibfcKS4nBP+dT81kkkg5Z5MohXBORA7VWx+ACohcDEkprsQ+w32xeD
qT1EvQKBgQDKm8ws2ByvSUVs9GjTilCajFqLJ0eVYzRPaY6f++Gv/UVfAPV4c+S0
kAWpXbv5tbkkzbS0eaLPTKgLzavXtQoTtKwrjpolHKIHUz6Wu+n4abfAIRFubOdN
/+aLoRQ0yBDRbdXMsZN/jvY44eM+xRLdRVyMmdPtP8belRi2E2aEzA==
-----END RSA PRIVATE KEY-----

```
**Objective:** The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Look at the commands that logged you into previous bandit levels, and find out how to use the key for this level.

![Figure 12: Level 13 -> Level 14](/images/bandit13_14.png)


```
ls
cat sshkey.private
## copy it and paste it into your own file (I named it the same)
## then ssh into the next level
ssh bandit14@bandit.labs.overthewire.org -p 2220 -i sshkey.private
```

## Level 14 -> Level 15
**Password:** `8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo`
**Objective:** The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

![Figure 13: Level 14 -> Level 15](/images/bandit14_15.png)

```
ls
## look at previous objective and see the file for the curent password is only readable by our current user now
## being 14
cat  /etc/bandit_pass/bandit14
## create a connection to port 30000 with netcat (nc)
nc localhost 30000
## paste curent level password
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS

```

## Level 15 -> Level 16
**Password:** `kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx`
**Objective:** The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL/TLS encryption.

Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.

![Figure 14: Level 15 -> Level 16](/images/bandit15_16.png)

```
ls
## s_client is the easiest point and click ssl/tls client I've found
openssl s_client -connect localhost:30001
## paste and enter pasword
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

```

## Level 16 -> Level 17
**Password:** 
```
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----

```
**Objective:** The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

Helpful note: Getting “DONE”, “RENEGOTIATING” or “KEYUPDATE”? Read the “CONNECTED COMMANDS” section in the manpage.

![Figure 15: Level 16 -> Level 17](/images/bandit16_17.png)

```
## nmap scan to see what ports in the 31000-32000 range are actually active and what services they run
nmap -sV -p 31000-32000 localhost
## connect to port with -quiet flag because without it we get a keyupdate error when we paste our key because
## apparently the k in the beggining of the password counts as a comamnd
openssl s_client --connect localhost:31790 -quiet
## paste password
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

```

## Level 17 -> Level 18
**Password:** `x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO`
**Objective:** There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19

![Figure 16: Level 17 -> Level 18](/images/bandit17_18.png)

```
ls
## shows difference of files
diff passwords.new password.old
## double check if its in the passwords.new
cat passwords.new | grep x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

## Level 18 -> Level 19
**Password:** `cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8`
**Objective:** The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.
(check the note from the other level)

![Figure 17: Level 18 -> Level 19](/images/bandit18_19.png)
```
## ssh has a feauture to just send a comamnd via ssh, just append it at the end
ssh bandit18@bandit.labs.overthewire.org -p 2220 cat readme
```

## Level 19 -> Level 20
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 20 -> Level 21
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 21 -> Level 22
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 22 -> Level 23
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 23 -> Level 24
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 24 -> Level 25
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 25 -> Level 26
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 26 -> Level 27
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 27 -> Level 28
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 28 -> Level 29
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 29 -> Level 30
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 30 -> Level 31
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 31 -> Level 32
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 32 -> Level 33
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 33 -> Level 34
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```
