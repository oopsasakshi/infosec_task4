## Module 6: Practicing Piping

### Challenge: Redirecting Output

**Task:**

This challenge teaches how to redirect command output to a file using the `>` operator. The goal is to write the word `PWN` into a file named `COLLEGE`.

**Commands Used:**

```bash
 ssh hacker@dojo.pwn.college
 PWN > COLLEGE
 echo PWN > COLLEGE
```
**Explanation:**

The `echo` command is used to generate the text `PWN.`
The `>` operator redirects this output into the file `COLLEGE` instead of displaying it on the screen.
Finally, the file `COLLEGE` contains exactly `PWN`, which satisfies the challenge requirement.

**Output:**

```bash
Correct! You successfully redirected 'PWN' to the file 'COLLEGE'! Here is your
flag:
pwn.college{suPJ97hQsBi0teH9R3WTFd-aS6A.QX0YTN0wyN2MDM1EzW}
```

**Flag:**
```bash
pwn.college{suPJ97hQsBi0teH9R3WTFd-aS6A.QX0YTN0wyN2MDM1EzW}
```

### Challenge: Redirecting More Output


**Task:**

This challenge focuses on redirecting the output of a command into a file. The goal is to run `/challenge/run` and redirect its standard output to a file named `myflag`.

**Commands Used:**

```bash
 ssh hacker@dojo.pwn.college
 /challenge/run > myflag
 cat myflag
```
**Explanation:**

`/challenge/run` prints the flag as output.
Using the `>` operator sends this output into the file myflag instead of displaying it on the screen.
When the output is redirected correctly, the challenge writes the flag into myflag, which can then be read using cat myflag.

**Output:**

```bash
[FLAG] Here is your flag:
[FLAG] pwn.college{YqR0yp1aPXHxp2Vm_-qQaO3Xe4o.QX1YTN0wyN2MDM1EzW}
```

**Flag:**
```bash
pwn.college{YqR0yp1aPXHxp2Vm_-qQaO3Xe4o.QX1YTN0wyN2MDM1EzW}
```


### Challenge: Appending Output


**Task:**

This challenge demonstrates how to append command output to an existing file instead of overwriting it .

**Commands Used:**

```bash
 ssh hacker@dojo.pwn.college
 /challenge/run >> /home/hacker/the-flag
cat /home/hacker/the-flag
```
**Explanation:**

The program writes the flag in two parts.
The first part is written directly to the file, and the second part is the challenge.

Using `>>` adds the second part to the end of the same file, keeping the first part intact.
If `>` were used, the second part would replace the first.

**Output:**

```bash
 |
\|/ This is the first half:
 v
pwn.college{YI6YbSld733TXWhElTXID15z5JO.QX3ATO0wyN2MDM1EzW}
                              ^
     that is the second half /|\
                              |
```

**Flag:**
```bash
pwn.college{YI6YbSld733TXWhElTXID15z5JO.QX3ATO0wyN2MDM1EzW}
```

### Challenge: Redirecting Errors


**Task:**

This challenge demonstrates how to separate normal output and error messages by redirecting them into different files.

**Commands Used:**

```bash
 ssh hacker@dojo.pwn.college
  /challenge/run > myflag 2> instructions
cat myflag
cat instructions 
```
**Explanation:**

Using `>` sends the normal output into `myflag`.
Using `2>` sends the error messages into `instructions`.

**Output:**

```bash
[FLAG] Here is your flag:
[FLAG] pwn.college{MrUBehH7autnpwFy1ftbwxmRxDW.QX3YTN0wyN2MDM1EzW}
```

**Flag:**
```bash
pwn.college{MrUBehH7autnpwFy1ftbwxmRxDW.QX3YTN0wyN2MDM1EzW}
```
### Challenge: Redirecting Input


**Task:**

This challenge focuses on sending data from a file into a program . The challenge requires to write the word `COLLEGE` into a file named `PWN`, then run `/challenge/run` so that it reads its input from the `PWN` .

**Commands Used:**

```bash
 ssh hacker@dojo.pwn.college
 echo COLLEGE > PWN
 PWN >/challenge/run
 /challenge/run < PWN
```
**Explanation:**

While `>` redirects output to a file, `<` redirects input from a file into a program. By using `/challenge/run < PWN`, the program reads the word `COLLEGE` directly from the file, satisfying the challenge requirement.

**Output:**

```bash
Reading from standard input...
Correct! You have redirected the PWN file into my standard input, and I read
the value 'COLLEGE' out of it!
Here is your flag:
pwn.college{IRUmbWJ6FRmZtn8yjWx2v98_Nrj.QXwcTN0wyN2MDM1EzW}
```

**Flag:**
```bash
pwn.college{IRUmbWJ6FRmZtn8yjWx2v98_Nrj.QXwcTN0wyN2MDM1EzW}
```
