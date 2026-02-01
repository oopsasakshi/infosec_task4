# OverTheWire Bandit: Levels 11-23

---


## Level 11 → Level 12

**Task:**

The goal of this level was to read the contents of `data.txt` and transform each letter with the one that is 13 places ahead in the alphabet to get the password.

**Command Used:**
```bash
ssh bandit11@bandit.labs.overthewire.org -p 2220
 cat data.txt | tr A-Za-z N-ZA-Mn-za-m
```
**Explanation:**

The file `data.txt` contained text where each letter was shifted , to get the flag:

* `tr` was used to replace characters and transform the text back into readable form
* `A-Za-z  N-ZA-Mn-za-m` maps each letter to another letter 13 positions ahead

**Output:**

```bash
The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```
**Flag:**

```bash
7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```

## Level 12 → Level 13

**Task:**

Recover the password hidden as a hexadecimal dump of repeatedly compressed data.

**Command Used:**
```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
 mktemp -d
cp data.txt /tmp/tmp.TT0iDQUycL
cd /tmp/tmp.TT0iDQUycL

xxd -r data.txt > data.bin
file data.bin
mv data.bin data.gz
gunzip data.gz
ls

file data
mv data data.bz2
bunzip2 data.bz2
ls

file data
mv data data.gz
gunzip data.gz
ls

file data
tar -xf data
ls

file data5.bin
tar -xf data5.bin
ls

file data6.bin
mv data6.bin data6.bz2
bunzip2 data6.bz2
ls

file data6
tar -xf data6
ls

file data8.bin
mv data8.bin data8.gz
gunzip data8.gz
ls

cat data8

```
**Explanation:**

In this challenge:
* `mktemp -d`
   * Creates a safe temporary directory to work in
* `cp data.txt /tmp/tmp.TT0iDQUycL`
   * Copies the challenge file into the temporary workspace
* `xxd -r data.txt > data.bin`
   * Converts hexadecimal text back into raw binary data
* `-r` tells `xxd` to reverse the hex dump
* `file <filename>`
   * Detects the actual file type, regardless of extension
* `mv <file> <newname>`
   * Renames the file so tools like gzip or bunzip2 can recognize it
* `gunzip <file>.gz`
   * Extracts files compressed using gzip
* `bunzip2 <file>.bz2`
   * Extracts files compressed using bzip2
* `tar -xf <file>`
   * Extracts files from a tar archive
   * -x = extract
   * -f = specify file

**Output:**

```bash
/tmp/tmp.TT0iDQUycL
The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```
**Flag:**

```bash
FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```

## Level 13 → Level 14

**Task:**

The password for bandit14 is stored in a file that only user bandit14 can read. Bandit13 provides a private SSH key instead of a password.

**Command Used:**
```bash
ssh bandit13@bandit.labs.overthewire.org -p 2220
ls
exit 
scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .
icacls sshkey.private /inheritance:r
icacls sshkey.private /grant:r "$($env:USERNAME):R"
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
cat /etc/bandit_pass/bandit14

```
**Explanation:**

In this challenge :

* `scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private .`
    * Securely copies (`scp`) the private SSH key file named `sshkey.private`
      from the `bandit13` home directory  to the current directory in my local machine
    * The `-P 2220` option specifies the SSH port used by Bandit.
  
* `icacls sshkey.private /inheritance:r`
    * Removes all inherited Windows permissions from the private key file.
    * SSH rejects private keys if they are accessible by others, so inheritance must be removed first.

* `icacls sshkey.private /grant:r "$($env:USERNAME):R"`
    * Grants read-only permission to my current Windows user account (`$($env:USERNAME):R`).
    * This makes the private key secure enough for SSH to accept it.
    * Without this step, SSH will refuse to use the key with a “bad permissions” error.

* `ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220`
    * Initiates an SSH connection to the Bandit server on *port 2220*.
    * The `-i sshkey.private` option tells SSH to authenticate using the private key instead of a password.
    * Logs in directly as bandit14
  
**Output/Flag:**

```bash
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```
## Level 14 → Level 15

**Task:**

A service running on `port 30000` expects the current level password as input.
The goal is to send the password to this service and retrieve the password for the next level.

**Command Used:**

```bash
 ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
 echo "MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS" | nc localhost 30000
```
**Explanation:**

In this challenge :

* `echo "MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS"` outputs the current level password.
*  `| `(pipe) edirects the output of `echo` as input to another command.
* `nc localhost 30000` uses netcat to connect to a service running on `port 30000` on the local machine.
  * `nc` is a tool that lets you talk to programs over the network using the terminal.
  
**Output:**

```bash
Correct!
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```

**Flag:**

```bash
8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo
```
## Level 15 → Level 16

**Task:**

A service running on `port 30001` requires the current level password to be submitted using SSL/TLS encryption.
The goal is to establish an encrypted connection and send the password to retrieve the next level password.

**Command Used:**

```bash
  ssh bandit15@bandit.labs.overthewire.org -p 2220
 echo "8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo" | openssl s_client -connect localhost:30001 -quiet
```
**Explanation:**

In this challenge :
* `openssl s_client`
   * Creates an `SSL/TLS` encrypted client connection.
   * `SSL/TLS` is used to encrypt data during transmission so that sensitive information like passwords cannot        be read by others on the network.
   * `nc` sends plain text only and service on port 30001 expects encrypted data so it ignores or rejects plain       text.
* `-connect localhost:30001`connects to the service running on port 30001.
* `-quiet` suppresses SSL handshake messages (like DONE , RENEGOTIATING ,KEYUPDATE) and displays only the server    response.
  
**Output:**

```bash
 localhost:30001 -quiet
Can't use SSL_get_servername
depth=0 CN = SnakeOil
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN = SnakeOil
verify return:1
Correct!
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```

**Flag:**

```bash
kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
```
## Level 16 → Level 17

**Task:**

Find the one `SSL/TLS` service between ports `31000–32000` that returns the next credentials.

**Command Used:**

```bash
 ssh bandit16@bandit.labs.overthewire.org -p 2220
nmap -p 31000-32000 localhost
echo "kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx" | openssl s_client -connect localhost:31046 -quiet
echo "kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx" | openssl s_client -connect localhost:31518 -quiet
echo "kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx" | openssl s_client -connect localhost:31691 -quiet
echo "kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx" | openssl s_client -connect localhost:31790 -quiet
```

### **Explanation:**

In this challenge:
* `nmap -p 31000-32000 localhost`
  * Scans all ports between `31000 and 32000` on the local machine.
  * Identifies which ports are open and have a service listening.
* `echo "kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx" | openssl s_client -connect localhost:<port> -quiet`
  * The command sends the current password into an encrypted SSL connection to a specific open port while             suppressing handshake noise to display only the server’s actual response.
* Each open port was tested one by one:
  * Some ports returned SSL errors .
  * Some ports simply echoed the password back .
  * `3179` port returned a RSA private key.
* copied the rsa to key17 txt file on the local machine.

  
**Output:**

```bash
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

Correct!
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

EReVavePLFHtFlFsjn3hyzMlvSuSAcRD
```

**Flag:**

```bash
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

EReVavePLFHtFlFsjn3hyzMlvSuSAcRD
```
## Level 17 → Level 18

**Task:**

To access bandit17, we must first log in using the RSA private key obtained in the previous level.
The goal is to find password for the next level that is only line that differs between two files.

**Command Used:**

```bash
notepad key17
icacls key17 /inheritance:r
icacls key17 /grant:r "$($env:USERNAME):(R)"
ssh -i key17 bandit17@bandit.labs.overthewire.org -p 2220

```
**Explanation:**

While login:
* `icacls key17 /inheritance:r`
   * ensures the private key does not inherit access rights from parent folders, which SSH considers insecure.
* `icacls key17 /grant:r "$($env:USERNAME):(R)"`
   * grants read-only permission to the current user only.SSH requires private keys to be readable only by the           owner; otherwise, it refuses to use the key.
     
In this challenge :

* After successful login, the home directory contains two files:
  * `passwords.old`
  * `passwords.new`
* The diff command compares both files line by line and prints only the changed line.
  * `<` line from the first file (passwords.old)
  * `> `line from the second file (passwords.new)
**Output:**

```bash
42c42
< BMIOFKM7CRSLI97voLp3TD80NAq5exxk
---
> x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

**Flag:**

```bash
x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```

## Level 18 → Level 19

**Task:**

The password for the next level is stored in a file named readme in the home directory but the .bashrc file has been modified to immediately log out upon SSH login.

**Command Used:**

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220
ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat readme"
```
**Explanation:**

In this challenge, logging in via SSH starts an interactive shell, which automatically executes `.bashrc` that immediately logs us out, blocking normal access.

By passing a command directly to SSH, no interactive shell is started.
Since `.bashrc` is never executed, the command runs successfully and the readme file can be read before logout.
  
**Output/Flag:**

```bash
 cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
```
## Level 19 → Level 20

**Task:**

A setuid program in the home directory allows commands to be executed as another user.
The goal is to use this binary to access the password for the next level stored in `/etc/bandit_pass`.

**Command Used:**

```bash
ssh bandit19@bandit.labs.overthewire.org -p 2220
ls
./bandit20-do
./bandit20-do cat /etc/bandit_pass/bandit20
```
**Explanation:**

In this challenge :
* The file `bandit20-do` is a setuid binary.
  * A setuid binary runs with the permissions of its owner, not the user executing it.
* When the program is run without any arguments, it shows instructions that make it clear it can run commands as the `bandit20` user.
* By using the binary to `cat` the password file, the contents of `/etc/bandit_pass/bandit20` can be read.
  
**Output/Flag:**

```bash
0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
```
## Level 20 → Level 21

**Task:**

The goal is to send the correct password through setuid binary and receive the password for the next level.

**Command Used:**

```bash
ssh bandit20@bandit.labs.overthewire.org -p 2220
ls
cat /etc/bandit_pass/bandit20
echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" | nc -l 1234 &
./suconnect 1234
```
**Explanation:**

In this challenge :
* `suconnect` is a setuid binary that runs with higher privileges.It connects to localhost on a port given     as an argument.
* `echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" | nc -l 1234 &`
    * `echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" |` sends passwords to `nc -l 1234 & `
* `nc -l 1234` starts netcat in listening mode on port 1234.This acts as a local server, waiting for a          connection.
* `&` runs the command in the background.
     * This allows the terminal to be used to run suconnect at the same time.
     * When `suconnect` connects to this port, the password is automatically sent.
* `./suconnect 1234` executes the setuid binary.
    * Connects to localhost on `port 1234`.
    * Reads the password sent by `nc`.

**Output:**
```bash
Read: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
Password matches, sending next password
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```
**Flag:**
```bash
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
```
## Level 21 → Level 22

**Task:**

The goal is to inspect the cron job, understand what it does, and retrieve the password it stores.

**Command Used:**

```bash
ssh bandit21@bandit.labs.overthewire.org -p 2220
 ls /etc/cron.d
 cat /etc/cron.d/cronjob_bandit22
 cat /usr/bin/cronjob_bandit22.sh
 cat  /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```
**Explanation:**

In this challenge :
* `cron` is a time-based scheduler that runs commands automatically.
* The cron configuration file `/etc/cron.d/cronjob_bandit22` shows that a script is executed every minute as `bandit22`.
* The script `/usr/bin/cronjob_bandit22.sh` copies the password for bandit22 into a file inside `/tmp` and makes it readable.
* Directory listing of `/tmp` is restricted, so the file cannot be discovered using `ls`.
* Once the cron job runs, the password file exists and can be accessed directly using its exact path.

**Output/Flag:**
```bash
tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```

## Level 22 → Level 23

**Task:**

A cron job automatically runs a script that stores the password using a generated filename.
The goal is to understand how this filename is created and use it to locate and read the next level’s password.

**Command Used:**

```bash
ssh bandit23@bandit.labs.overthewire.org -p 2220
 ls /etc/cron.d
 cat /etc/cron.d/cronjob_bandit23
 cat /usr/bin/cronjob_bandit23.sh
 echo I am user bandit23 | md5sum
 cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```
**Explanation:**

In this challenge :
* `/usr/bin/cronjob_bandit23.sh` reveals that the cron script stores the password in `/tmp` using a filename generated from a hash of the string `I am user bandit23`, allowing the filename to be recreated by following the same logic.
* `echo I am user bandit23 | md5sum` is used to generate the same hash that the cron script uses as the filename.The output of this command is a hash value, and only the first part of this output is required, as it represents the exact filename.
* Using `cat /tmp/8ca319486bfbbc3663ea0fbe81326349` reads the file created by the cron job, which contains the password for the next level.
      
**Output:**
```bash
#!/bin/bash
myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)
echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"
cat /etc/bandit_pass/$myname > /tmp/$mytarget
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```

**Output/Flag:**
```bash
0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```
