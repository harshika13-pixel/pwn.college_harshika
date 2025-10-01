
# Challenge 1: Matching with *

Starting from your home directory, change your directory to /challenge, but use globbing to keep the argument you pass to cd to at most four characters. Once you're there, run /challenge/run for the flag.

## Solution:

The ` cd /ch*` is invoked with changes the directory to `/challenge`. The ```/challenge/run``` command is invoked to print the flag.

```sh
$ cd /ch*
$ /challenge/run
```

## Flag: 

```
pwn.college{4D7fJTWwWwgXfIeuLFHMEWuzQLD.QXxIDO0wyMxAzNzEzW}
```

### Notes:

When it encounters a * character in any argument, the shell will treat it as a "wildcard" and try to replace that argument with any files that match the pattern.

When zero files are matched, by default, the shell leaves the glob unchanged:
```sh
hacker@dojo:~$ touch file_a
hacker@dojo:~$ ls
file_a
hacker@dojo:~$ echo Look: nope_*
Look: nope_*
```




# Challenge 2: Matching with ?

Starting from your home directory, change your directory to /challenge, but use the ? character instead of c and l in the argument to cd. Once you're there, run /challenge/run for the flag.

## Solution:

The `cd /?ha??enge` is invoked with changes the directory to `/challenge`. The ```/challenge/run``` command is invoked to print the flag.

```sh
$ cd /?ha??enge
$ /challenge/run
```

## Flag: 

```
pwn.college{EaUOhmrhDlqk93xff7F_YCjwnaG.QXyIDO0wyMxAzNzEzW}
```

### Notes:

When it encounters a ? character in any argument, the shell will treat it as a single-character wildcard. This works like *, but only matches one character.




# Challenge 3: Matching with []

There are a bunch of files in /challenge/files. Change your working directory to /challenge/files and run /challenge/run with a single argument that bracket-globs into file_b, file_a, file_s, and file_h.

## Solution:

The `cd /challenge/files` is invoked with changes the directory to `/challenge/files`. The ```/challenge/run file_[absh]``` command is invoked to print the flag.

```sh
$ cd /challenge/files
$ /challenge/run file_[absh]
```

## Flag: 

```
pwn.college{A6-l2yUliblm-iefV_4yaoUoLc6.QXzIDO0wyMxAzNzEzW}
```

### Notes:

The square brackets are, essentially, a limited form of ?, in that instead of matching any character, [] is a wildcard for some subset of potential characters, specified within the brackets. For example, [pwn] will match the character p, w, or n. 




# Challenge 4: Matching paths with []

There are a bunch of files in /challenge/files. Starting from your home directory, run /challenge/run with a single argument that bracket-globs into the absolute paths to the file_b, file_a, file_s, and file_h files. 

## Solution:

The `/challenge/run /challenge/files/file_[absh]` command is invoked to print the flag. 

```sh
$ /challenge/run /challenge/files/file_[absh]
```

## Flag: 

```
pwn.college{Qz4Z2lf3Y7RhshV8OKW9fUISlmr.QX0IDO0wyMxAzNzEzW}
```

### Notes:

Globbing happens on a path basis, so we can expand entire paths with your globbed arguments.




# Challenge 5: Multiple Globs

There are a few happy, but diversely-named files in /challenge/files. Go cd there and run /challenge/run, providing a single argument: a short (3 characters or less) globbed word with two * globs in it that covers every word that contains the letter p.

## Solution:

The `cd /challenge/files` is invoked with changes the directory to `/challenge/files`. The ```/challenge/run *p*``` command is invoked to print the flag..

```sh
$ cd /challenge/files
$ /challenge/run *p*
```

## Flag: 

```
pwn.college{Enz2_VEw3hNBygQzo_Y-iVatp-g.0lM3kjNxwyMxAzNzEzW}
```

### Notes:

Bash supports the expansion of multiple globs in a single word.



# Challenge 6: Mixing Globs

There are a few happy, but diversely-named files in /challenge/files. Go cd there and, using the globbing you've learned, write a single, short (6 characters or less) glob that (when passed as an argument to /challenge/run) will match the files "challenging", "educational", and "pwning".

## Solution:

The `cd /challenge/files` is invoked with changes the directory to `/challenge/files`. The ```/challenge/run [ecp]*``` command is invoked to print the flag..

```sh
$ cd /challenge/files
$ /challenge/run [ecp]*
```

## Flag: 

```
pwn.college{0W149kjgGJGTOtDMXVjQPAOAPj4.QX1IDO0wyMxAzNzEzW}
```



# Challenge 7: Exclusionary globbing

Go forth to /challenge/files and run /challenge/run with all files that don't start with p, w, or n.

## Solution:

The `cd /challenge/files` is invoked with changes the directory to `/challenge/files`. The ```/challenge/run [!pwn]*``` command is invoked to print the flag..

```sh
$ cd /challenge/files
$ /challenge/run [!pwn]*
```

## Flag: 

```
pwn.college{ohK1ptwGX2bemHXmhzhvGBygfnE.QX2IDO0wyMxAzNzEzW}
```

### Notes:

We might need to filter out files sometimes. [] can help. If the first character in the brackets is a ! or (in newer versions of bash) a ^, the glob inverts, and that bracket instance matches characters that aren't listed.




# Challenge 8: Tab Completion

This challenge has copied the flag into /challenge/pwncollege, and you can freely cat that file. But you can't type the filename: you must tab-complete it. 

## Solution:

The `ls /challenge` is used to list the files. 
Then, the command `cat /challenge/pwn<TAB>` is used to display the flag. The "<TAB>" actually implies hitting the tab key, which completes the command. 
The terminal displays:

hacker@globbing~tab-completion:~$ `ls /challenge`
DESCRIPTION.md  pwncollege​
hacker@globbing~tab-completion:~$ `cat /challenge/pwncollege​`

```sh
$ ls /challenge
$ cat /challenge/pwn<TAB>
```

## Flag: 

```
pwn.college{83xVbRuyaAQl3MZp96oHboklxAH.0FN0EzNxwyMxAzNzEzW}
```

### Notes:

If tab key is hit in the shell, it'll try to figure out what you're going to type and automatically complete it.
This is more preferable than using *, since * can expand to unintended files. 




# Challenge 9: Multiple options for tab completion

This challenge has a /challenge/files directory with a bunch of files starting with pwncollege. Tab-complete from /challenge/files/p or so, and make your way to the flag.

## Solution:

First the directory is changed to /challenge/files. Then `ls p<TAB><TAB>. This will print out all the options. Then we can cat the required file. 

The terminal displays:
hacker@globbing~multiple-options-for-tab-completion:~$ `cd /challenge/files`
hacker@globbing~multiple-options-for-tab-completion:/challenge/files$ `ls pwn`
pwn                    pwncollege-flag
pwn-college            pwncollege-flamingo
pwn-the-planet         pwncollege-flyswatter
pwncollege-family      pwncollege-hacking
hacker@globbing~multiple-options-for-tab-completion:/challenge/files$ `cat pwncollege-flag`

## Flag: 

```
pwn.college{0IaGsPSr7zXbS143Ee6RDafIDv5.0lN0EzNxwyMxAzNzEzW}
```

### Notes:

If there are multiple options, by default bash will auto-expand until the first point. Eg:
```sh
hacker@dojo:~$ ls
flag  flamingo  flowers
hacker@dojo:~$ cat f<TAB>
```
Hitting the tab key will cause it to automplete till "fl". When we hit tab a second time, it'll print out those options. Other shells and configurations, instead, will cycle through the options.





# Challenge 10: Tab completion on commands

This level has a command that starts with pwncollege, and it'll give you the flag. Type pwncollege and hit the tab key to auto-complete it. 

## Solution:

The terminal displays:
hacker@globbing~tab-completion-on-commands:~$ `pwncollege-28471`

The actual command that has been used is `pwncollege<TAB>`.

## Flag: 

```
pwn.college{swmlA_mng1HWgyvZcXDdlyOMml_.0VN0EzNxwyMxAzNzEzW}
```

### Notes:

We can also tab-complete commands. But, callous auto-completes without double-checking the result can wreak havoc in your shell if you accidentally run the wrong commands. 