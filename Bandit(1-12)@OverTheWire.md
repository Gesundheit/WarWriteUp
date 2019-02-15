# Bandit Wargame
Bandit is the beginner friendly wargame available to play @ http://overthewire.org/wargames/bandit/. If you're a complete beginner, this is a good place to start.
## Level0
> The goal of this level is for you to log into the game using SSH. <br>
> The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. <br>
> The username is bandit0 and the password is bandit0. <br>
<br>
This is a simple ssh login from your terminal. Simply type the following code in your terminal:

```ssh bandit0@bandit.labs.overthewire.org -p 2220``` <br>

Enter the password and voila! You're in. <br>

## Level0 :arrow_right: Level1
> The password for the next level is stored in a file called **readme** located in the home directory.<br>
> Use this password to log into bandit1 using SSH. <br>
> Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game. <br>
<br>
After logging into the server using ssh, we are supposed to look read the file **readme** located in our directory. A simple `cat` command should be enough.

```bandit0@bandit:~$ cat readme``` <br>
> boJ9jbbUNNfktd78OOpsqOltutMc3MY1 <br>

## Level1 :arrow_right: Level2
> The password for the next level is stored in a file called **-** located in the home directory. <br>
<br>
To login to bandit1 simply use the ssh command:

```bandit0@bandit:~$ ssh bandit1@localhost```<br>

Enter the password obtained from the last level and we're in.<br>

Now we're supposed to read a file with the name "-". <br>
A quick `ls` shows that a file exists with the name "-". When `cat` sees the string - as a filename, it treats it as a synonym for stdin. To get around this, you need to alter the string that cat sees in such a way that it still refers to a file called "-". The usual way of doing this is to prefix the filename with a path - `./-`

```bandit1@bandit:~$ cat ./-``` <br>
> CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9 <br>

## Level2 :arrow_right: level3
> The password for the next level is stored in a file called **spaces in this filename** located in the home directory <br>
<br>
Login to bandit2 the same way as we did above. <br>
To `cat` a file with spaces in its name simply add quotation marks `" "` around the filename, like so: 

```bandit2@bandit:~$ cat "spaces in this filename"``` <br>
> UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK <br>

## Level3 :arrow_right: level4
> The password for the next level is stored in a **hidden** file in the **inhere** directory.

A quick `ls` command shows the existing inhere directory

```
bandit3@bandit:~$ ls
inhere
```
<br>
Now we navigate to **inhere** directory and look for all hidden files using `ls -a` 

```
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ls -a
.  ..  .hidden
```
<br>
Sure enough, we find the hidden file there. Now we simply read it using `cat`

```bandit3@bandit:~/inhere$ cat .hidden```<br>
> pIwrPrtPN36QITSp3EQaw936yaFoFgAB <br>

## Level4 :arrow_right: Level5
> The password for the next level is stored in the only human-readable file in the inhere directory.<br>
> Tip: if your terminal is messed up, try the “reset” command.<br>

Using `ls -a` to view all files in the **inhere** directory
```
bandit4@bandit:~/inhere$ ls -a
.   -file00  -file02  -file04  -file06  -file08
..  -file01  -file03  -file05  -file07  -file09
```
<br>
Now, we know that the password is stored in a human-readable file in this directory. Using the `file` command to view the type of files we have in this directory. You can either check all files one by one or use `./*` which checks all files in current directory.
```
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```
<br>
Now we simply read `-file07` because it exists as an ASCII file

``` bandit4@bandit:~/inhere$ cat ./-file07``` <br>
> koReBOKuIDDepwhWk7jZC0RTdopnAYKh <br>'

## Level5 :arrow_right: Level6
>The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties: <br>
>    human-readable <br>
>    1033 bytes in size <br>
>    not executable <br>

After navigating to inhere, we will use `ls -a` again to check for hidden files
```
bandit5@bandit:~/inhere$ ls -a
.            maybehere03  maybehere08  maybehere13  maybehere18
..           maybehere04  maybehere09  maybehere14  maybehere19
maybehere00  maybehere05  maybehere10  maybehere15
maybehere01  maybehere06  maybehere11  maybehere16
maybehere02  maybehere07  maybehere12  maybehere17
```
<br> 
As you can see there are a lot of folders and going through each one will be tiresome. We will use the `find` command again. Using the information given in the challenge, we will modify our `find` command.
```
bandit5@bandit:~/inhere$ find -readable -size 1033c ! -executable
./maybehere07/.file2
```
<br>
So we know where the password is stored. 
```bandit5@bandit:~/inhere$ cat ./maybehere07/.file2```<br>
> DXjZPULLxYr17uwoI01bNLQbtFemEgo7 <br>

## Level6 :arrow_right: Level7
> The password for the next level is stored somewhere on the server and has all of the following properties:<br>
> owned by user bandit7<br>
> owned by group bandit6<br>
> 33 bytes in size<br>

We will use the `find` command to find the file passing `/` as an argument to search the entire server.

```
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c
/var/lib/dpkg/info/bandit7.password
```
<br>
Now a simple `cat` command will give us our password:
```bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password```<br>
> HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs <br>

## Level7 :arrow_right: Level8
> The password for the next level is stored in the file **data.txt** next to the word **millionth** <br>

For this challenge, we will use the `grep` command, to find a specific string in **data.txt**
```
bandit7@bandit:~$ ls
data.txt
bandit7@bandit:~$ grep "millionth" data.txt
millionth	cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```
<br>
> cvX2JJa4CFALtqS87jk27qwqGhBM9plV <br>

## Level8 :arrow_right: Level9
> The password for the next level is stored in the file data.txt and is the only line of text that occurs only once <br>
For this challenge we need to use the `sort` and `uniq` commands.
```
bandit8@bandit:~$ sort data.txt | uniq -u
``` 
<br>
Simply using a uniq




















