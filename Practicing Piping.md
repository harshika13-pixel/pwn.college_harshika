
# Challenge 1: Redirecting output

In this challenge, you must use output redirection to write the word PWN (all uppercase) to the filename COLLEGE (all uppercase).

## Solution:

The `echo PWN > COLLEGE` writes the word "PWN" to the file COLLEGE, hence displays the flag. 

```sh
$ echo PWN > COLLEGE
```

## Flag: 

```
pwn.college{4cyvTArOccOdFIDXJaxXx4HoFmH.QX0YTN0wyMxAzNzEzW}
```

### Notes:

Redirecting stdout to files can be accomplished with the > character.




# Challenge 2: Redirecting more output

In this level, /challenge/run will once more give you a flag, but only if you redirect its output to the file myflag. Your flag will end up in the myflag file.

## Solution:

The terminal displays:

hacker@piping~redirecting-more-output:~$ `/challenge/run > myflag`
[INFO] WELCOME! This challenge makes the following asks of you:
[INFO] - the challenge will check that output is redirected to a specific file path : myflag
[INFO] - the challenge will output a reward file if all the tests pass : /flag

[HYPE] ONWARDS TO GREATNESS!

[INFO] This challenge will perform a bunch of checks.
[INFO] If you pass these checks, you will receive the /flag file.

[TEST] You should have redirected my stdout to a file called myflag. Checking...

[PASS] The file at the other end of my stdout looks okay!
[PASS] Success! You have satisfied all execution requirements.
hacker@piping~redirecting-more-output:~$ `cat myflag`

[FLAG] Here is your flag:
[FLAG] pwn.college{gtSiv6J-LXl8FOROvMhSL02e9i3.QX1YTN0wyMxAzNzEzW}



```sh
$ /challenge/run > myflag
$ cat myflag
```

## Flag: 

```
pwn.college{gtSiv6J-LXl8FOROvMhSL02e9i3.QX1YTN0wyMxAzNzEzW}
```

### Notes:

/challenge/run will still print to your terminal, despite you redirecting stdout. That's because it communicates its instructions and feedback over standard error, and only prints the flag over standard out.




# Challenge 3: Appending output

Run /challenge/run with an append-mode redirect of the output to the file /home/hacker/the-flag. The practice will write the first half of the flag to the file, and the second half to stdout if stdout is redirected to the file. If you properly redirect in append-mode, the second half will be appended to the first, but if you redirect in truncation mode (>), the second half will overwrite the first and you won't get the flag.

## Solution:

```sh
$ /challenge/run >> /home/hacker/the-flag
$ cat /home/hacker/the-flag
```


## Flag: 

```
pwn.college{8hG_u141lf8rDqMeQ-9bHWMs9Ay.QX3ATO0wyMxAzNzEzW}
```

### Notes:

when we use > to redirect output and again use > to redirect output in the same file the previous one gets delted and second one is redirected. we use >> to append the second output to the first output.




# Challenge 4: Redirecting errors

In this challenge, you will need to redirect the output of /challenge/run to myflag, and the "errors" (in this case, the instructions) to instructions. You can find the instructions/feedback in instructions and the flag in myflag when you successfully pull this off. 

## Solution:

The ```/challenge/run > myflag 2> instructions``` is invoked, which redirects the errors to instructions and the output to myflag. Then we can print both files using cat. `cat myflag` will display the file. 

```sh
$ /challenge/run > myflag 2> instructions
$ cat instructions
$ cat myflag
```

## Flag: 

```
pwn.college{U6Kk6vvm3e0N_MQJZgNKJX77jBe.QX3YTN0wyMxAzNzEzW}
```

### Notes:

A File Descriptor (FD) is a number that describes a communication channel in Linux. 
FD 0: Standard Input
FD 1: Standard Output
FD 2: Standard Error

A > without a number implies 1>, which redirects FD 1 (Standard Output). 
We can redirect multiple file descriptors at the same time.



# Challenge 5: Redirecting input

Use /challenge/run, which will require you to redirect the PWN file to it and have the PWN file contain the value COLLEGE. 

## Solution:

```sh
$ echo COLLEGE > PWN
$ /challenge/run < PWN
```

The first command writes COLLEGE to PWN, and then PWN file is redirected using <. 

## Flag: 

```
pwn.college{kQcF_b7mj5S3BSzg8Wc4RB9SA13.QXwcTN0wyMxAzNzEzW}
```



# Challenge 6: Grepping stored results

Redirect the output of /challenge/run to /tmp/data.txt.
This will result in a hundred thousand lines of text, with one of them being the flag, in /tmp/data.txt.
grep that for the flag. 

## Solution:

The first command redirects the output and the second finds the flag. "pwn.college" is used because the flag begins with it.

```sh
$ /challenge/run > /tmp/data.txt
$ grep pwn.college /tmp/data.txt
```

## Flag: 

```
pwn.college{0tFMChU5VOOMyOoYQbnZ2f60nTH.QX4EDO0wyMxAzNzEzW}
```




# Challenge 7: Grepping live output

/challenge/run will output a hundred thousand lines of text, including the flag. grep for the flag, by using the | (pipe) operator. 

## Solution:

```sh
$ /challenge/run | grep pwn.college
```

## Flag: 

```
pwn.college{AWlcL8OfZlpXp_lamMZq_BupFO7.QX5EDO0wyMxAzNzEzW}
```

### Notes:

Standard output from the command to the left of the pipe will be connected to (piped into) the standard input of the command to the right of the pipe.



# Challenge 8: Grepping errors

Grep through errors directly. 

## Solution:

```sh
$ /challenge/run 2>&1 | grep pwn.college
```

## Flag: 

```
pwn.college{sRv3l40dizyvzIZSRStNuwbkdb_.QX1ATO0wyMxAzNzEzW}
```

### Notes:

>& operator redirects a file descriptor to another file descriptor. This means that we can have a two-step process to grep through errors: first, we redirect standard error to standard output (2>& 1) and then pipe the now-combined stderr and stdout as normal (|)



# Challenge 9: Filtering with grep -v

In this challenge, /challenge/run will output the flag to stdout, but it will also output over 1000 decoy flags (containing the word DECOY somewhere in the flag) mixed in with the real flag. Use grep -v to filter out all the lines containing "DECOY" and reveal the real flag.

## Solution:

```sh
$ /challenge/run | grep -v DECOY
```

## Flag: 

```
pwn.college{IiEKjxzxacTj-oxz0uEOLIu1SQs.0FOxEzNxwyMxAzNzEzW}
```

### Notes:

While normal grep shows lines that MATCH a pattern, grep -v shows lines that do NOT match a pattern. 

Here, the command displays all lines which do NOT have the word "DECOY"




# Challenge 10: Duplicating piped data with tee

This process' /challenge/pwn must be piped into /challenge/college, but you'll need to intercept the data to see what pwn needs from you. 

## Solution:

```sh
$ /challenge/pwn | tee fl | /challenge/college
$ cat fl
```
This shows: SECRET_ARG should be "YB8e1HP6"

```sh
/challenge/pwn --secret YB8e1HP6 | /challenge/college
```

## Flag: 

```
pwn.college{YB8e1HP6OpgGN-9JVSwBNZL-k5C.QXxITO0wyMxAzNzEzW}
```

### Notes:

The tee command duplicates data flowing through your pipes to any number of files provided on the command line. 




# Challenge 11: Process substitution for input

diff two sets of command outputs: /challenge/print_decoys, which will print a bunch of decoy flags, and /challenge/print_decoys_and_flag which will print those same decoys plus the real flag.

Use process substitution with diff to compare the outputs of these two programs and find your flag.

## Solution:

``` sh
diff <(/challenge/print_decoys) <(/challenge/print_decoys_and_flag)
```
This displays `24a25`, which implies that the second file has an extra 25th line, which is my required flag and displays the flag.

## Flag: 

```
pwn.college{ktyjiPcVi2wzuTi-T5QmP4Bd1vY.0lNwMDOxwyMxAzNzEzW}
```




# Challenge 12: Writing to multiple programs

In this challenge, we have /challenge/hack, /challenge/the, and /challenge/planet. Run the /challenge/hack command, and duplicate its output as input to both the /challenge/the and the /challenge/planet commands.

## Solution: 

```sh
$ /challenge/hack | tee >(/challenge/the) >(/challenge/planet)
```

## Flag: 

```
pwn.college{81wvmP0vXSCXH7nnwcOgvHTtlXL.QXwgDN1wyMxAzNzEzW}
```

### Notes:

tee stored the output of /hack and stored it to 3 diff places stdout, /planet and /the.




# Challenge 13: Split-piping stderr and stdout

In this challenge, you have:
/challenge/hack: this produces data on stdout and stderr
/challenge/the: you must redirect hack's stderr to this program
/challenge/planet: you must redirect hack's stdout to this program

## Solution: 

```sh
$ /challenge/hack> >(/challenge/planet) 2> >(/challenge/the)
```

## Flag: 

```
pwn.college{I6PyAQWhcj7NSDuKyF8G4xqr3o6.QXxQDM2wyMxAzNzEzW}
```

### Notes:

/planet gets the stdout from /hack and /the gets the stderr from /hack. The first > is redirection and second > is process substitution.




# Challenge 14: Named pipes

Create a /tmp/flag_fifo file and redirect the stdout of /challenge/run to it. If you're successful, /challenge/run will write the flag into the FIFO. 

HINT: The blocking behavior of FIFOs makes it hard to solve this challenge in a single terminal. You may want to use the Desktop or VSCode mode for this challenge so that you can launch two terminals.

## Solution:

The terminal displays:

hacker@piping~named-pipes:~$ `/challenge/run > /tmp/flag_fifo`
You're successfully redirecting /challenge/run to a FIFO at /tmp/flag_fifo!
Bash will now try to open the FIFO for writing, to pass it as the stdout of
/challenge/run. Recall that operations on FIFOs will *block* until both the
read side and the write side is open, so /challenge/run will not actually be
launched until you start reading from the FIFO!


hacker@piping~named-pipes:~$ `mkfifo /tmp/flag_fifo`
hacker@piping~named-pipes:~$ `cat /tmp/flag_fifo`
You've correctly redirected /challenge/run's stdout to a FIFO at /tmp/flag_fifo! Here is your flag:
pwn.college{Quz5k4aFkLMI2BzuRdHg7T9C7iU.01MzMDOxwyMxAzNzEzW}

## Flag: 

```
pwn.college{Quz5k4aFkLMI2BzuRdHg7T9C7iU.01MzMDOxwyMxAzNzEzW}
```

### Notes:

FIFOs (named pipes) are like pipes you make yourself. They show up as a file on the system, but instead of saving data, they just pass it around in memory.

You can create one with mkfifo filename. if you ls -l, it shows up with a p at the start instead of a - (so we know it’s a pipe and not a normal file).

Unlike process substitution pipes (/dev/fd/...), these FIFOs stick around until you delete them.

Writing to a FIFO (like echo hi > myfifo) won’t actually run unless there’s a reader waiting on the other side (cat myfifo). Otherwise, it just sits there “blocked” until someone picks it up.