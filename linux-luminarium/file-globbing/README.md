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

```bash
You got it! Here is your flag!
pwn.college{w9y0GwaV3aHqVSxfrRoDe-sanMy.QX0IDO0wyN2MDM1EzW}
```
**Flag:**

``` bash
pwn.college{w9y0GwaV3aHqVSxfrRoDe-sanMy.QX0IDO0wyN2MDM1EzW}
```
