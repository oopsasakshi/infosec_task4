## Module 8: Data Manipulation

### Challenge: Translating Characters

**Task:**

The program `/challenge/run` outputs the flag with all letter cases swapped . The goal is to restore the flag by reversing this transformation using `tr`.

**Commands Used:**

```bash
 ssh hacker@dojo.pwn.college
 /challenge/run | tr a-z A-Z
 /challenge/run | tr a-zA-Z A-Za-z
```
**Explanation:**

* `tr` command translates characters position by position.
* `a-zA-Z  A-Za-z` swaps the case of all lowercase to uppercase letters and vice-versa.
* Piping the output into `tr` reverses the case swap in one step.

**Output:**

```bash
yOUR CASE-SWAPPED FLAG:
pwn.college{scWNEXjIpYtBzBx0YyOSRTJNvMr.01MxEzNxwyN2MDM1EzW}
```

**Flag:**
```bash
pwn.college{scWNEXjIpYtBzBx0YyOSRTJNvMr.01MxEzNxwyN2MDM1EzW}
```
### Challenge: Deleting Characters

**Task:**

The goal is to filter out  extra characters (^ and %) from the program `/challenge/run` using `-d` flag. 

**Commands Used:**

```bash
 ssh hacker@dojo.pwn.college
 /challenge/run | tr -d ^%
```
**Explanation:**

* The `tr -d` option deletes specified characters from the input stream.
* By piping the output into` tr -d ^%`, all occurrences of ^ and % are removed.

**Output:**

```bash
Your character-stuffed flag:
pwn.college{8MaaOh3IA3FesO9Sq5M1lEYAG0_.0FNxEzNxwyN2MDM1EzW}
```

**Flag:**
```bash
pwn.college{8MaaOh3IA3FesO9Sq5M1lEYAG0_.0FNxEzNxwyN2MDM1EzW}
```
### Challenge: Deleting Newlines

**Task:**

The goal is to remove newline characters from the output of `/challenge/run` so the flag appears as a single continuous line. 

**Commands Used:**

```bash
 ssh hacker@dojo.pwn.college
 /challenge/run | tr -d "\n"
```
**Explanation:**

Using `tr -d "\n"` deletes all newline characters from the stream, joining the output into one line to give correct flag.

**Output:**

```bash
Your line-split flag: pwn.college{g1lpx3tnD4aIdAjR3Vic9AjAUR7.0VNxEzNxwyN2MDM1EzW}
```

**Flag:**
```bash
pwn.college{g1lpx3tnD4aIdAjR3Vic9AjAUR7.0VNxEzNxwyN2MDM1EzW}
```
### Challenge: Extracting the First Lines with `head`

**Task:**

The goal is to use `head` to extract only the first 7 lines of output from `/challenge/pwn` and pipe them into `/challenge/college` .

**Commands Used:**

```bash
 ssh hacker@dojo.pwn.college
 /challenge/pwn | head -n 7 | /challenge/college
```
**Explanation:**

`head -n 7` limits the stream to the first seven lines only.
These selected lines are then piped into `/challenge/college` to give the flag.

**Output:**

```bash
Congratulations, you piped the right codes!
pwn.college{4YsPM7Sg0FDzTePZ7ts9ms_OmpL.0lNxEzNxwyN2MDM1EzW}
```

**Flag:**
```bash
pwn.college{4YsPM7Sg0FDzTePZ7ts9ms_OmpL.0lNxEzNxwyN2MDM1EzW}
```
### Challenge: Extracting Specific Sections Of Text

**Task:**

The goal is to extract the flag characters from `/challenge/run` by selecting the correct column using `cut -d` and then join the output into a single line.

**Commands Used:**

```bash
 ssh hacker@dojo.pwn.college
 /challenge/run | cut -d " " -f 1 | tr -d "\n"
/challenge/run | cut -d " " -f 2 | tr -d "\n"
```
**Explanation:**

The output of `/challenge/run` is split into multiple columns separated by spaces. 
* `cut` command is used to isolate the column that contains the flag characters
* `-d " "` specifies the space delimiter and `-f` selects the required column
* Since the flag appears one character per line, the output is finally piped through `tr -d "\n"` to remove newlines and reconstruct the complete flag.

**Output:**

```bash
69732239524454531317343130703156953222967418602193942243151333101731238189411446919183856910013266351912429004173661488681162835410011276564135771627990196492074623311984523069225621188824355297062778229325140763549231666198465721416339232452964118692200801898618089842023141118894019

pwn.college{s3ESXtilt1IJA8TF-istez7QQGa.01NxEzNxwyN2MDM1EzW}
```

**Flag:**
```bash
pwn.college{s3ESXtilt1IJA8TF-istez7QQGa.01NxEzNxwyN2MDM1EzW}
```
### Challenge: Sorting Data

**Task:**

The goal is to sort the contents of `/challenge/flags.tx`t so that the real flag appears last.

**Commands Used:**

```bash
 ssh hacker@dojo.pwn.college
 sort -r /challenge/flags.txt
```
**Explanation:**

The `sort` command organizes lines alphabetically by default. Since the real flag is to be last when sorted, using the `-r` we  reverse the order , bringing the real flag into starting. 

**Output/Flag:**

```bash
pwn.college{c2zAE1W-Zg2gvL1KsAExJcdB8JA.0FM0MDOxwyN2MDM1EzW}
```
