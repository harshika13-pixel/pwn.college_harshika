
# Challenge 1: Printing Variables

Have your shell print out the FLAG variable with echo, by prepending the variable name with a $ and solve this challenge. 

## Solution:

The ```echo $FLAG ``` command is invoked to print the flag.

```sh
$ echo $FLAG
```

## Flag: 

```
pwn.college{kOKzEhqScwQGf5dGElBLqSVERrB.QX3UTN0wyMxAzNzEzW}
```

### Notes:

echo is used to print stuff. it can also be used to print out variables,  by prepending the variable name with a $.




# Challenge 2: Setting Variables

To solve this level, you must set the PWN variable to the value COLLEGE.

## Solution:

The ```PWN=COLLEGE``` command is invoked to print the flag.

```sh
$ PWN=COLLEGE
```

## Flag: 

```
pwn.college{w_OAwKvFC095t2mnvgGP6_718_y.QX5UTN0wyMxAzNzEzW}
```

### Notes:

We use = (like in all other languages), to write values to variables. To be noted:
1. there are no spaces around the =! If you put spaces (e.g., VAR = 1337), the shell won't recognize a variable assignment and will, instead, try to run the VAR command (which does not exist).
2. This uses VAR and not $VAR: the $ is only prepended to access variables.
3. both the names and values of variables are case-sensitive. 



# Challenge 3: Multi-word Variables

Set the variable PWN to COLLEGE YEAH. Use quotes.

## Solution:

The ```PWN="COLLEGE YEAH"``` is invoked, which displays the flag. 

```sh
$ PWN="COLLEGE YEAH"
```

## Flag: 

```
pwn.college{AjJfNCt_Pt0N2nsE-vKO4omGAsL.QXwYTN0wyMxAzNzEzW}
```

### Notes:

If the shell sees a space, it ends the variable assignment and interprets the next word (SAUCE in this case) as a command. To set VAR to 1337 SAUCE, you need to quote it: `VAR="1337 SAUCE"`



# Challenge 4: Exporting Variables

In this challenge, you must invoke /challenge/run with the PWN variable exported and set to the value COLLEGE, and the COLLEGE variable set to the value PWN but not exported.

## Solution:

First, we assign COLLEGE to the variable PWN and export it using: `export PWN=COLLEGE`. Then, the `COLLEGE=PWN` is invoked to set the COLLEGE VARIABLE to the proper value. The ```/challenge/run``` is invoked, which displays the flag.

```sh
$ export PWN=COLLEGE
$ COLLEGE=PWN
$ /challenge/run
```

## Flag: 

```
pwn.college{USXpe_lbdOQK0LqtMAxwWxg_B-o.QXyYTN0wyMxAzNzEzW}
```

### Notes:

When you export your variables, they are passed into the environment variables of child processes.
Here is an example:
```sh
hacker@dojo:~$ VAR=1337
hacker@dojo:~$ export VAR
hacker@dojo:~$ sh
$ echo "VAR is: $VAR"
VAR is: 1337
```
Here, the child shell received the value of VAR and was able to print it out.


# Challenge 5: Printing Exported Variables

Use the env command to print out every exported variable set in your shell, and you can look through that output to find the FLAG variable.

## Solution:

```sh
$ env
```

The terminal displays:

hacker@variables~printing-exported-variables:~$ env
SHELL=/run/dojo/bin/bash
HOSTNAME=variables~printing-exported-variables
PWD=/home/hacker
MANPATH=/run/dojo/share/man:
DOJO_AUTH_TOKEN=45eb2ebd15f517691469811f2f31c76f183853d74b564028c91fdf100b38b490
HOME=/home/hacker
LANG=C.UTF-8
FLAG=pwn.college{UzrUfOrT1dVBUqQIMTXkX9xECgy.QX4UTN0wyMxAzNzEzW}
TERMINFO=/run/dojo/share/terminfo
TERM=xterm-256color
SHLVL=2
LC_CTYPE=C.UTF-8
SSL_CERT_FILE=/run/dojo/etc/ssl/certs/ca-bundle.crt
PATH=/run/challenge/bin:/run/dojo/bin:/root/.cargo/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
DEBIAN_FRONTEND=noninteractive
_=/run/dojo/bin/env


## Flag: 

```
pwn.college{UzrUfOrT1dVBUqQIMTXkX9xECgy.QX4UTN0wyMxAzNzEzW}
```

### Notes:

env command prints out every exported variable set in your shell. 




# Challenge 6: Storing Command Output

Read the output of the /challenge/run command directly into a variable called PWN, and it will contain the flag

## Solution:

The output of the `/challenge/run` command is assigned directly to the variable PWN first in the format $(). Then the variable is printed out using echo.

```sh
$ PWN=$(/challenge/run)
$ echo $PWN
```

## Flag: 

```
pwn.college{8c1NpV_uEBjBggWJAMBBWE0a5X5.QX1cDN1wyMxAzNzEzW}
```

### Notes:

We can also use backticks instead of $(): FLAG=`cat /flag` instead of FLAG=$(cat /flag). This can have a few disadvantages as this is an old version. 



# Challenge 7: Reading Input

In this challenge, your need to use read to set the PWN variable to the value COLLEGE.

## Solution:

The terminal displays:
hacker@variables~reading-input:~$ `read -p "INPUT: " PWN`
INPUT: COLLEGE

Here, the college is input by the user. 

```sh
$ read -p "INPUT: " PWN
COLLEGE
```

## Flag: 

```
pwn.college{w62A3VYHOXKlJXb-6A1CxpveEFK.QX4cTN0wyMxAzNzEzW}
```

### Notes:

The -p argument lets you specify a prompt (otherwise, it would be hard to separate input from output).



# Challenge 8: Reading Files

Read /challenge/read_me into the PWN environment variable, and it will give you the flag! The /challenge/read_me will keep changing, so you'll need to read it right into the PWN variable with one command.

## Solution:

```sh
$ read PWN < /challenge/read_me
```
This redirects /challenge/read_me into the standard input of read, and so when "read" reads into PWN, it generates the flag.

## Flag: 

```
pwn.college{g4VDDjjHlIlva_RmZEnyGskCHFT.QXwIDO0wyMxAzNzEzW}
```

### Notes:

Read user input into a variable. and redirect files into command input. Put them together, and we can read files with the shell.