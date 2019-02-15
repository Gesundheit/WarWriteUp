# Bandit Wargame
Bandit is the beginner friendly wargame available to play @ http://overthewire.org/wargames/bandit/. If you're a complete beginner, this is a good place to start.
## Level0
> Level Goal <br>
> The goal of this level is for you to log into the game using SSH. <br>
> The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. <br>
> The username is bandit0 and the password is bandit0. <br>
<br>
This is a simple ssh login from your terminal. Simply type the following code in your terminal:

```ssh bandit0@bandit.labs.overthewire.org -p 2220``` <br>

Enter the password and voila! You're in. <br>

## Level0 :arrow_right: Level1
> Level Goal <br>
> The password for the next level is stored in a file called readme located in the home directory.<br>
> Use this password to log into bandit1 using SSH. <br>
> Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game. <br>
<br>
After logging into the server using ssh, we are supposed to look read the file **readme** located in our directory.A simple `cat` command should be enough.

```cat readme``` <br>

Which gives us the output: <br>
> boJ9jbbUNNfktd78OOpsqOltutMc3MY1
