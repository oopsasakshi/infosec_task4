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

### Challenge: Grepping Stored Results

**Task:**

This challenge combines output redirection and searching. The goal is to store a large output in a file and then search it for the flag.

**Commands Used:**
```bash
ssh hacker@dojo.pwn.college
/challenge/run > /tmp/data.txt
grep pwn /tmp/data.txt
```

**Explanation:**

The output of `/challenge/run` is first stored in a file to avoid the cluttering .
The `grep` command searches the file for lines containing the keyword related to the flag.

**Output:**
```bash
pwn
pwn.college{YkoXZWYr5E1oy0OieJBAbH97L6v.QX4EDO0wyN2MDM1EzW}
pwned
pwns
pwning
```

**Flag:**
```bash
pwn.college{YkoZXWYr5Eloy00ieJBAhB97L6v.QX4ED00wyN2MDM1EzW}
```
### Challenge: Grepping Live Output

**Task:**

This challenge demonstrates searching output without saving it to a file by using pipes.

**Commands Used:**
```bash
ssh hacker@dojo.pwn.college
/challenge/run | grep pwn.college
```

**Explanation:**

The pipe `|` sends the output of `/challenge/run` directly into `grep`.
`grep` filters the  output and prints only the matching line containing pwn.college.

Output/Flag::
```bash
pwn.college{IpsW_fHQifW4F-MROyHFHSZCgi.QX5ED00wyN2MDM1EzW}
```


### Challenge: Grepping Errors

**Task:**

This challenge focuses on searching error output instead of normal output. The goal is to redirect error messages into a pipe and use `grep` to find the flag from them.

**Commands Used:**

```bash
ssh hacker@dojo.pwn.college
/challenge/run 2>&1 | grep pwn.college
```

**Explanation:**

Normally, the pipe (`|`) only passes normal output to the next command.
In this challenge:
* `2>&1` redirects error output into normal output
* `| grep pwn.college` then searches that combined output
* `grep` filters and displays only the line containing the flag

This allows the flag to be extracted even though it was printed as an error.

**Output:**

```bash

[PASS] You have passed the checks on the process on the other end of my stderr!
[PASS] Success! You have satisfied all execution requirements.
pwn.college{gzA6bYfwuxbmfV6DQZOBQHYjAAB.QX1ATO0wyN2MDM1EzW}
```

**Flag:**

```bash
pwn.college{gzA6bYfwuxbmFVDQZOBQHYjAAB.QX1AT00wyN2MDM1EzW}
```


### Challenge: Filtering with grep -v

**Task:**

This challenge demonstrates how to exclude unwanted lines from output. The goal is to remove all lines containing DECOY and reveal the real flag.

**Commands Used:**
```bash
ssh hacker@dojo.pwn.college
/challenge/run | grep -v DECOY
```

**Explanation:**

The `-v` option tells grep to exclude lines containing the word DECOY.
By filtering out the decoys, only the real flag remains.

**Output/Flag:**

```bash
pwn.college{QNaxYQv4nOMmk_64IMxV5rPRAta.OFOxEzNxwyN2MDM1EzW}
```


### Challenge: Filtering with sed

**Task:**

This challenge focuses on cleaning unwanted text from command output. The goal is to remove repeated garbage strings from the output.

**Commands Used:**
```bash
ssh hacker@dojo.pwn.college
/challenge/run | sed "s/FAKEFLAG//g"
```

**Explanation:**

The `sed` command is used to replace text patterns.
Here, `s/FAKEFLAG//g` tells sed to remove every occurrence of FAKEFLAG from the output.

By piping the output of `/challenge/run` into `sed`, all the unwanted text is stripped away.

**Output:/Flag**
```bash
pwn.college{sIH6k5ohQDZkhtBirbzLR99BmKD.01NxQTMywyN2MDM1EzW}
```


### Challenge: Duplicating Piped Data with tee

**Task:**

This challenge demonstrates how to send data from one program to another while also viewing or saving a copy of that data. The goal is to understand how piping works between programs and how tee can be used for inspection and debugging.

**Commands Used:**

```bash
ssh hacker@dojo.pwn.college
/challenge/pwn | tee /tmp/secret | /challenge/college
cat /tmp/secret
/challenge/pwn --secret I_iHbjyv | /challenge/college
```

**Explanation:**

`/challenge/pwn | tee /tmp/secret | /challenge/college` failed because `/challenge/pwn` requires a secret argument and only printed a usage message.
The `tee` command was used to duplicate the output:
* One copy is written to the file `/tmp/secret`
* The other copy is passed forward through the pipe
  After giving the secret argument `--secret I_iHbjyv` , `/challenge/pwn` produced the correct output, which was passed directly into `/challenge/college` to give the flag.

**Output:**
```bash
Usage: /challenge/pwn --secret [SECRET_ARG]
SECRET_ARG should be "I_iHbjvy"

Correct! Passing secret value to /challenge/college...
Great job! Here is your flag:
pwn.college{I_iHbjyvX5bIaU9ewGkbZPIoV.QXxIT00wyN2MDM1EzW}
```

**Flag:**
```bash
pwn.college{I_iHbjyvX5bIaU9ewGkbZPIoV.QXxIT00wyN2MDM1EzW}
```

### Challenge: Process Substitution For Input

**Task:**

This challenge introduces process substitution . The goal is to find a hidden flag by comparing the live outputs of two different programs without saving them to physical files.

**Commands Used:**

```bash
ssh hacker@dojo.pwn.college
 diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag)
```

**Explanation:**

`/challenge/print_decoys` prints only fake flags, while `/challenge/print_decoys_and_flag` prints the same fake flags plus the real one.
Process substitution `<(command)` lets `diff` compare their outputs directly without using files.

**Output:**
```bash
67a68
> pwn.college{sp8GquA054J-Jq1EWBobtBZlrc2.0lNwMDOxwyN2MDM1EzW}
```

**Flag:**
```bash
pwn.college{sp8GquA054J-Jq1EWBobtBZlrc2.0lNwMDOxwyN2MDM1EzW}
```
### Challenge: Writing To Multiple Programs

**Task:**

This challenge demonstrates how to send the same output to multiple programs at the same time.
The goal is to take the output from `/challenge/hack` and provide it simultaneously as input to both `/challenge/the` and `/challenge/planet`.

**Commands Used:**

```bash
ssh hacker@dojo.pwn.college
/challenge/hack | tee >(/challenge/the) | >(/challenge/planet)
/challenge/hack | tee >(/challenge/the) >(/challenge/planet)
```

**Explanation:**

The pipe `|` sends this output forward, while `tee` duplicates it (splits the data into multiple streams).
Using process substitution `>(command)`, the duplicated output is written directly into the input of `/challenge/the` and `/challenge/planet`.

**Output:**
```bash
Congratulations, you have duplicated data into the input of two programs! Here
is your flag:
pwn.college{8ia7__u5efKAlo3vXX8VmUFQTHk.QXwgDN1wyN2MDM1EzW}
```

**Flag:**
```bash
pwn.college{8ia7__u5efKAlo3vXX8VmUFQTHk.QXwgDN1wyN2MDM1EzW}
```

### Challenge: Split Piping Stderr And Stdout

**Task:**

This challenge demonstrates how to separate a program’s normal output and error output and send them to two different programs.

**Commands Used:**

```bash
ssh hacker@dojo.pwn.college
/challenge/hack | >( /challenge/planet) | 2> >( /challenge/the )
/challenge/hack | tee >( /challenge/planet ) 2> >( /challenge/the )
/challenge/hack > >( /challenge/planet ) 2> >( /challenge/the )
```

**Explanation:**

The `>` operator redirects standard output, while `2>` redirects standard error.
Process substitution `>(command)` turns a program into a writable input stream.
Here:
* `> >( /challenge/planet )` sends stdout into `/challenge/planet`
* `2> >( /challenge/the )` sends stderr into `/challenge/the`

**Output:**
```bash
Congratulations, you have learned a redirection technique that even experts
struggle with! Here is your flag:
pwn.college{4eHgLKmYVo_uJWOElB6AhveI4cD.QXxQDM2wyN2MDM1EzW}
```

**Flag:**
```bash
pwn.college{4eHgLKmYVo_uJWOElB6AhveI4cD.QXxQDM2wyN2MDM1EzW}
```
### Challenge: Named Pipes

**Task:**

This challenge introduces named pipes (FIFOs), which allow two separate programs to communicate through a shared pipe file.
The goal is to redirect the output of `/challenge/run` into a FIFO and read it from another process to retrieve the flag.

**Commands Used:**

```bash
ssh hacker@dojo.pwn.college
mkfifo /tmp/flag_fifo
cat /tmp/flag_fifo
 /challenge/run > /tmp/flag_fifo
```

**Explanation:**

Here:
* `mkfifo /tmp/flag_fifo` creates a named pipe.
* `cat /tmp/flag_fifo` starts a reader and waits for data.
* In another terminal, `/challenge/run > /tmp/flag_fifo` starts the writer.
 Named pipes block until both a reader and a writer are connected. Once both sides are active, data flows through the pipe instantly.This is why two terminals are required.

**Output:**
```bash
You've correctly redirected /challenge/run's stdout to a FIFO at
/tmp/flag_fifo! Here is your flag:
pwn.college{oz6yGW8GKjFPrkfUP5PZjaBKxnN.01MzMDOxwyN2MDM1EzW}
```

**Flag:**
```bash
pwn.college{oz6yGW8GKjFPrkfUP5PZjaBKxnN.01MzMDOxwyN2MDM1EzW}
```
