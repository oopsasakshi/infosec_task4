## Module 4: File Globbing

### Challenge: Matching With *

**Task:**

This challenge introduces the use of the * wildcard to match any sequence of
characters in file or directory names.

**Commands Used:**

```bash
ssh hacker@dojo.pwn.college
cd /ch*
/challenge/run

```
**Explanation:**

The `*` wildcard matches any number of characters (including zero).
Instead of typing the full directory name /challenge, the pattern /c* expands to /challenge.

By changing the working directory under condition that argument passed to cd to at most four characters is satisfied .

**Output:**

```bash
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{IIB_-vwwlN7JItkxqrOSnCafbyU.QXxIDO0wyN2MDM1EzW}
```
**Flag:**

``` bash
pwn.college{IIB_-vwwlN7JItkxqrOSnCafbyU.QXxIDO0wyN2MDM1EzW}
```

### Challenge: Matching With ?

**Task:**

This challenge focuses on using the ? wildcard, which matches exactly one character.

**Commands Used:**

```bash
ssh hacker@dojo.pwn.college
 cd /?ha??enge
/challenge/run

```
**Explanation:**

The` ?` wildcard substitutes one single character.
In `/?ha??enge, the ? matches the missing character (c and l), resolving to /challenge.

**Output:**

```bash
You ran me with the working directory of /challenge! Here is your flag:
pwn.college{8Xi4wAKS2xK2RoqgsDvPNliWLGn.QXyIDO0wyN2MDM1EzW}
```
**Flag:**

``` bash
pwn.college{8Xi4wAKS2xK2RoqgsDvPNliWLGn.QXyIDO0wyN2MDM1EzW}
```

### Challenge: Matching With []

**Task:**

This challenge focuses on using the [] wildcard, which allow matching specific characters.

**Commands Used:**

```bash
ssh hacker@dojo.pwn.college
 cd /challenge/files
/challenge/run file_[absh]

```
**Explanation:**

Square brackets allow matching specific characters.
The shell expands file_[absh] to the actual existing filename 
before running /challenge/run.

**Output:**
```bash
You got it! Here is your flag!
pwn.college{MCWppd7hhc_g1b6rI1IZl7yA6z0.QXzIDO0wyN2MDM1EzW}
```
**Flag:**

``` bash
pwn.college{MCWppd7hhc_g1b6rI1IZl7yA6z0.QXzIDO0wyN2MDM1EzW}
```

### Challenge: Matching Paths With []

**Task:**

This challenge focuses on using square bracket globbing ([]) on absolute paths. The 
goal is to pass a single argument to the program that expands into the 
correct file paths located in a different directory.

**Commands Used:**

```bash
ssh hacker@dojo.pwn.college
 cd /home/hacker
/challenge/run
/challenge/run /challenge/files/file_[absh]


```
**Explanation:**

Here, square brackets [] are used to match exactly one character within an absolute file path.
The glob pattern is applied to the full path, 
allowing files located in a different directory to be matched.
The expression [absh] expands to the characters b, a, s, or h, which resolves
the pattern into multiple valid file paths inside /challenge/files.

**Output:**
```bash
You got it! Here is your flag!
pwn.college{w9y0GwaV3aHqVSxfrRoDe-sanMy.QX0IDO0wyN2MDM1EzW}
```
**Flag:**

``` bash
pwn.college{w9y0GwaV3aHqVSxfrRoDe-sanMy.QX0IDO0wyN2MDM1EzW}
```

### Challenge: Multiple Globs

**Task:**

This challenge demonstrates how multiple glob patterns can be combined in a 
single argument to match files with specific characteristics.

**Commands Used:**

```bash

ssh hacker@dojo.pwn.college
/challenge/run *p*

```
**Explanation:**

Here, multiple * wildcards are used within a single glob pattern.The pattern 
*p* matches any filename that contains the letter p anywhere in its name.Since all required files include p, the glob 
expands to the correct set of filenames.

**Output:**

```bash
You got it! Here is your flag!
pwn.college{w9y0GwaV3aHqVSxfrRoDe-sanMy.QX0IDO0wyN2MDM1EzW}
```
**Flag:**

``` bash
pwn.college{w9y0GwaV3aHqVSxfrRoDe-sanMy.QX0IDO0wyN2MDM1EzW}
```

### Challenge: Mixing Globs

**Task:**

This challenge focuses on combining square-bracket character ([]) with wildcard globbing (*) to find the file with challenge specifications.

**Commands Used:**

```bash

ssh hacker@dojo.pwn.college
 cd /challenge/files
 ls
/challenge/run [c*ep]
/challenge/run [cep*]
/challenge/run [cep]*
```
**Explanation:**

* `c*ep` gives error because * inside square brackets is treated as a literal character, not a wildcard.
* `cep*` also fails because * inside [] does not expand to multiple characters.
*  `[cep]*` gives the file as
    - `cep` matches exactly one character: c, e, or p
    - `*` is placed outside the character class, allowing it to match the rest of the filename

This correctly expands to challenging, educational, and pwning only.

**Output:**

```bash
You got it! Here is your flag!
pwn.college{YuyTOxJK7rql-GRAHhE_vP8XdI6.QX1IDO0wyN2MDM1EzW}
```
**Flag:**

``` bash
pwn.college{YuyTOxJK7rql-GRAHhE_vP8XdI6.QX1IDO0wyN2MDM1EzW}
```

### Challenge: Exclusionary Globbing

**Task:**

This challenge shows how to use exclusionary globbing to select files that do not start with certain letters by using square brackets , ! , *.
The goal is to pass all files except those starting with p, w, or n to /challenge/run.

**Commands Used:**

```bash

ssh hacker@dojo.pwn.college
 cd /challenge/files
 ls
/challenge/run [!pwn]
/challenge/run [!pwn]*
```
**Explanation:**

Here:
* `!` at the start of the brackets inverts the match, excluding p, w, and n.
* `!pwn` matches filenames starting with any other character.
* allows the rest of the filename to be matched.


This expands to all required filenames while excluding pwning, wonderful, and nice, satisfying the challenge conditions.

**Output:**

```bash
You got it! Here is your flag!
pwn.college{08aPQmpqlsZ1K8QSMcuYCpQOpto.QX2IDO0wyN2MDM1EzW}
```
**Flag:**

``` bash
pwn.college{08aPQmpqlsZ1K8QSMcuYCpQOpto.QX2IDO0wyN2MDM1EzW}

```
### Challenge: Tab Completion

**Task:**

This challenge demonstrates the importance of tab completion in the Linux shell and how it helps safely and accurately reference filenames that cannot be typed manually.

**Commands Used:**

```bash
ssh hacker@dojo.pwn.college
ls /challenge
cat /challenge/pwn<TAB>

```
**Explanation:**

Tab completion allows the shell to automatically complete filenames when the *Tab* key is pressed. This ensures the correct file path is used without manually typing the full name, making file access accurate and reliable.

**Output/Flag:**
```bash
pwn.college{M0HUbJB9IJm7MSELyDc0oxdYTAP.0FN0EzNxwyN2MDM1EzW}
```

### Challenge: Multiple Options For Tab Completion

**Task:**

This challenge demonstrates how tab completion behaves when multiple files share the same starting characters. The goal is to use the Tab key to explore available options and  identify the file containing the flag.

**Commands Used:**

```bash

ssh hacker@dojo.pwn.college
 cd /challenge/files
 /challenge/files/pwn
cat /challenge/files/pwncollege-hacking
cat /challenge/files/pwncollege-family
cat /challenge/files/pwn-college
cat /challenge/files/pwncollege-flag
```
**Explanation:**

When multiple filenames start with the same prefix, pressing Tab once completes the command up to the longest common part. Pressing Tab again lists all matching options.

By repeatedly using tab completion and checking each expanded filename, the correct file containing the flag was found ,`pwncollege-flag`.

**Output:**

```bash
pwn                    pwncollege-family      pwncollege-hacking
pwn-college            pwncollege-flamingo
pwn-the-planet         pwncollege-flyswatter

No flag in this file!
No flag in this file!

hack-the-planet        pwn-the-planet         pwncollege-flamingo
pwn                    pwncollege-family      pwncollege-flyswatter
pwn-college            pwncollege-flag        pwncollege-hacking

pwn.college{oWvXmNY-yYVILGQzBKw9BOHWpba.0lN0EzNxwyN2MDM1EzW}
```
**Flag:**

``` bash
pwn.college{oWvXmNY-yYVILGQzBKw9BOHWpba.0lN0EzNxwyN2MDM1EzW}

```


### Challenge: Globbing Tab Completion On Commands

**Task:**

This challenge shows that tab completion can also be used for commands, not just filenames. The goal is to use the Tab key to auto-complete the correct command and execute it to get the flag.

**Commands Used:**

```bash

ssh hacker@dojo.pwn.college
 pwncollege-13388
```
**Explanation:**

When a command prefix is typed and Tab is pressed, the shell completes it to the full command if a matching one exists. By tab-completing the command that starts with pwncollege, the correct command is expanded and executed.

**Output:**

```bash
Correct! Here is your flag:
pwn.college{QX_JWOFGkug7G8KEiCf0gUuFpwg.0VN0EzNxwyN2MDM1EzW}
```
**Flag:**

``` bash
pwn.college{QX_JWOFGkug7G8KEiCf0gUuFpwg.0VN0EzNxwyN2MDM1EzW}

```

