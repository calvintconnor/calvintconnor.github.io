
---
title: "Upgrade A Unix/Windows Shell"
layout: single
read_time: true
comments: true
share: true
author_profile: true
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: /assets/christopher-burns-Kj2SaNHG-hg-unsplash.jpg
excerpt: "<br><br><br>"
categories:
  - tutorial
tags:
  - cybersecurity
  - penetration testing
---

Too often we get dropped into a shell that has no arrow keys and looks and feels broken. As a beginner, and as I once did, you might sorrowfully accept that this will be the state of all your shells for the rest of your life. However, this does not have to be the case. This blog post is here to show you what I stumbled upon months into my hacking journey so that you can fly where I tripped.


Upgrading A Unix Shell

The most common method of upgrading your shell on a Unix machine is by using Python. Python allows us to spawn a pseudo-shell far fancier than anything you could imagine.

You can use the ‘which’ command to find out what Python, if any, is installed on your box. Please note that using the 'which' command only shows you programs in $PATH, but Python will almost always be there. This is good to add to your tool belt, but soon you will just skip over it.

```
which python python2 python3
```

Now that we know which Python is installed, you can usually guess Python3, we can use it to spawn a python pseudo-shell.

```
python3 -c 'import pty; pty.spawn("/bin/bash")'
```
We will configure sending raw input through our reverse shell. Doing the control ctrl-z command will put the current process in the background, allowing us to interact with our system without closing the connection.

```
Ctrl-z  # the keyboard shortcut
stty raw -echo; fg
```
Here you could also have typed the stty and fg commands separately, but I run into less errors when I do them together. Remember, ; allows us to string together multiple different commands. The fg command stands for ‘foreground’ and brings the background process back into focus.

Finally, we change an environment variable to allow us to clear the console and have color output.

```
export TERM=xterm-256color
```
At this point I will usually press enter a few times and clear my screen to have my upgraded shell. Below is copyable version of all the commands you need in order.

```
python3 -c 'import pty; pty.spawn("/bin/bash")' # try python2 as well
CTRL + Z
stty raw -echo; fg # can enter separately
# Press Enter
export TERM=xterm-256color
# Press Enter a few times and clear screen
```
Upgrading A Unix Shell With zsh
Sometimes things fail. The above will not always work and I have more often than I would like to admit gotten a bricked shell with the commands above. If you are using Kali Linux there is a good chance that your zsh shell is breaking things. Use the following command to verify if you are running zsh.

```
ps -p $$
```
If you are running something like zsh or fish from the command above, we might have to temporarily switch our terminal to bash. To temporarily switch to a bash shell, run the following command in your terminal.

```
exec bash –login
```

Confirm that you are now in a bash shell by running ps -p $$ and continue upgrading your shell as normal.

## Script
In the case that Python is not installed on the target machine you can also use the script command. This may sound confusing at first if you have used the script command before, but script allows us to use the -c command option to get a usable TTY shell.

```
script -qc /bin/bash /dev/null
```
Here we included the /dev/null option to change the output directory of the log file. Script is meant to record input commands, so if you do not include a place to store this log file it will default to creating one in your current directory. To leave as little trace as possible we send this log file to /dev/null.

## Other Languages
Here is a collection of other languages that would allow you to upgrade a shell.

```
#perl
perl -e 'exec "/bin/sh";'

#ruby
exec "/bin/sh"
ruby -e 'exec "/bin/sh"'

#lua
lua -e "os.execute('/bin/sh')"

#expect
Create and run file with following code:
#!/usr/bin/expect
spawn sh
interact

```
## Conclusion
Always remember you have tons of options to upload some binary to achieve an upgraded shell that way as well if your shell is proving increasingly difficult to work with. These techniques do not apply to Windows machines, however, there will be a separate post on this.



