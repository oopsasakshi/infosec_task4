## Module 7: Shell Variables

### Challenge: Printing Variables

**Task:**

The goal is to print the value of the variable named `FLAG`, which already contains the flag, instead of running `/challenge/run`.

**Commands Used:**

```bash
 ssh hacker@dojo.pwn.college
 echo $FLAG
```
**Explanation:**

To print a variable, its name is prefixed with a `$`.
Using `echo $FLAG` tells the shell to expand the variable and print its value to the terminal.

**Output/Flag:**

```bash
pwn.college{MD4YLgRmYxMcnT-3Ut1D611o10A.QX3UTN0wyN2MDM1EzW}
```

### Challenge: Setting Variables

**Task:**

This challenge focuses on assigning values to shell variables.

**Commands Used:**

```bash
 ssh hacker@dojo.pwn.college
 PWN=COLLEGE
```
**Explanation:**

In the shell, variables are set using the `=` operator without spaces.
Here, `PWN=COLLEGE` assigns the value `COLLEGE` to the variable `PWN`.

**Output:**

```bash
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{krll9rfoBUVXgPuGCjbLbTGdtqM.QX5UTN0wyN2MDM1EzW}
```

**Flag:**
```bash
pwn.college{krll9rfoBUVXgPuGCjbLbTGdtqM.QX5UTN0wyN2MDM1EzW}
```
### Challenge: Multi Word Variables

**Task:**

The goal is to assign a variable named `PWN` a value that contains multiple words `COLLEGE YEAH` and retrieve the flag.

**Commands Used:**

```bash
 ssh hacker@dojo.pwn.college
 PWN="COLLEGE YEAH"
```
**Explanation:**

In the shell, spaces input into separate tokens.
By wrapping the value in double quotes ("), the shell treats `COLLEGE YEAH` as one single value and assigns it correctly to the variable `PWN`.

**Output:**

```bash
You've set the PWN variable properly! As promised, here is the flag:
pwn.college{45fBS2LD2zunTKsGnwZj2Ojv_cu.QXwYTN0wyN2MDM1EzW}
```

**Flag:**
```bash
pwn.college{45fBS2LD2zunTKsGnwZj2Ojv_cu.QXwYTN0wyN2MDM1EzW}
```

### Challenge: Exporting Variables

**Task:**

The goal is to:
* Export the variable `PWN` with the value `COLLEGE`
* Set the variable `COLLEGE` to the value `PWN` without exporting it
* Then run `/challenge/run` so it can read only the exported variable

**Commands Used:**

```bash
 ssh hacker@dojo.pwn.college
COLLEGE=PWN
export PWN=COLLEGE
/challenge/run

```
**Explanation:**
* `PWN=COLLEGE` sets a shell variable.
* `export PWN=COLLEGE` makes `PWN` an environment variable, so `/challenge/run` can read it.
* `COLLEGE=PWN` is intentionally not exported, but the shell can still check it internally.
By default, variables you create are local to the shell and are not visible to programs you run.

**Output:**

```bash
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!

You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!

Here is your flag:
pwn.college{oyP14pEdV24CC46Hl7hyOb-nEdB.QXyYTN0wyN2MDM1EzW}
You've set the PWN variable to the proper value!
You've set the COLLEGE variable to the proper value!
```

**Flag:**
```bash
pwn.college{oyP14pEdV24CC46Hl7hyOb-nEdB.QXyYTN0wyN2MDM1EzW}
```

### Challenge: Printing Exported Variables

**Task:**

The goal is to list all exported variables and find the one that stores the flag.

**Commands Used:**

```bash
 ssh hacker@dojo.pwn.college
env

```
**Explanation:**

The `env` command prints all exported variables available to the current shell.

**Output:**

```bash
SHELL=/run/dojo/bin/bash
HOSTNAME=variables~printing-exported-variables
PWD=/home/hacker
MANPATH=/run/dojo/share/man:
DOJO_AUTH_TOKEN=WzE1MDM2NywiZW52IiwiY2xpLWF1dGgtdG9rZW4iXQ.aXfajA.mozG4eIQw03fj4lSL2l3JtPDpLc
HOME=/home/hacker
LANG=C.UTF-8
FLAG=pwn.college{ApUpbr9hs1txcU-DKcg-slS-5GI.QX4UTN0wyN2MDM1EzW}
TERMINFO=/run/dojo/share/terminfo
TERM=xterm-256color
SHLVL=2
LC_CTYPE=C.UTF-8
SSL_CERT_FILE=/run/dojo/etc/ssl/certs/ca-bundle.crt
PATH=/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
DEBIAN_FRONTEND=noninteractive
_=/run/dojo/bin/env
```

**Flag:**
```bash
pwn.college{ApUpbr9hs1txcU-DKcg-slS-5GI.QX4UTN0wyN2MDM1EzW}
```

