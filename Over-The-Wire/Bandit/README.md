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
**Password:** ``
**Objective:** ```bash

```

## Level 12 -> Level 13
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 13 -> Level 14
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 14 -> Level 15
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 15 -> Level 16
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 16 -> Level 17
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 17 -> Level 18
**Password:** `[Insert Password Here]`
**Objective:** ```bash

```

## Level 18 -> Level 19
**Password:** `[Insert Password Here]`
**Objective:** ```bash

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
