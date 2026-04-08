#### Level 0

**Goal:** The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

Command: 
ssh bandit0@bandit.labs.overthewire.org -p2220
Password:  bandit0

---
#### Level 0 -> Level 1

**Goal:** Read the readme file to get the password for the next level.

Command:
cat readme

Next Password: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

*Connect via SSH using the provided port. Use cat to read the contents of readme file, which contains the next password*

---
#### Level 1 -> Level 2

**Goal:** Read the file named "-" which looks like an option

Command: cat ./-

Next Password: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

*Using the command `cat -` does not return anything. So instead of writing just `-` we add the path and write `./-` and ./- explicitly tells cat the filename — in the current directory

---
#### Level 2 -> Level 3

**Goal:** Read the file named --spaces in this filename--

Command: cat ./--spaces\ in\ this\ filename--

Next Password: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

---

#### Level 3 -> Level 4

**Goal:** The password for the next level is stored in a hidden file in the **inhere** directory.

Command: 
cd inhere
cat ./...Hiding-From-You

Next Password : 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

---

#### Level 4 -> Level 5

**Goal:** The password for next level is stored in a -file07 in the inhere directory.

Command: 
cd inhere
cat ./-file07

Next Password: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

---

#### Level 5 -> Level 6

**Goal:** The password of next level is stored in ./maybehere07/.file2 in the inhere directory

Command: 
du -b -a | grep 1033
cat ./maybehere07/.file2

Next Password: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

*It lists all files and directories with their sizes in bytes and filters the output to show only those whose size contains `1033`.*

---

#### Level 6 -> Level 7

**Goal:** The password for the next level is stored **somewhere on the server** and has all of the following properties:
- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

Command: 
 find / -user bandit7 -group bandit6 -size 33c
 cat /var/lib/dpkg/info/bandit7.password

Next Password: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

---

#### Level 7 -> Level 8

**Goal:** The password for the next level is stored in the file **data.txt** next to the word millionth

Command:
cat data.txt | grep "millionth"

Next Password: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

---

#### Level 8 -> Level 9
**Goal:** The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once

Command: 
sort data.txt | uniq -u

Next Password: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

---
#### Level 9 -> Level 10

**Goal:** The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.

Command: 
strings data.txt | grep "="

Next Password: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

---
#### Level 10 -> Level 11

**Goal:** The password for the next level is stored in the file **data.txt**, which contains base64 encoded data

Command: 
cat data.txt
base64 -d data.txt

Next Password: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

---
#### Level 11 -> Level 12

**Goal:** Decode the data.txt file in rot 13

Command:
cat data.txt
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'

Decode in rot 13

Next Password: 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

---
#### Level 12 -> Level 13

**Goal:** The password is stored in data.txt in hexdump, we have to decode it.

Command: 
mkdir /tmp/silent
cp data.txt /tmp/silent
gzip -d data.gz
mv data data.bz2
bzip2 -d data.bz2
mv data data.gz
gzip -d data.gz
mv data data.tar
tar xf data.tar
rm data.tar rm data.txt
file data5.bin
mv data5.bin data.tar
tar xf data.tar
mv data6.bin data.bz2
bzip2 -d data.bz2
mv data data.tar
tar xf data.tar
mv data8.bin data.gz
gzip -d data.gz
ls
cat data

Next Password : FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn

#### Level 13 -> Level 14

**Goal:** The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level.

Commands:
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .

Now from you host machine (Kali Linux), give permission to sshkey.private of 600
chmod 600 sshkey.private
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
cd /etc/bandit_pass/
cat bandit14

Next Password: MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS

#### Level 14 -> Level 15

Goal: The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

Command: 
ssh localhost 30000
Put the previous password - MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
And you get the flag.

Next Password: 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

#### Level 15 -> Level 16

Goal: The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

Commands: 
ncat --ssl localhost 30001
Put the previous password - 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
And you get the flag.

Next Password: kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

#### Level 16 -> Level 17

Goal: 