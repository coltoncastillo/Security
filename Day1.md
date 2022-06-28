# DAY 1

```
Stack Number	|    Username |	Password |	lin.internet
9	      | COCA-004-M	| wumbo69	 |    10.50.40.189

FW5TtIEpzQnbLyX

CTFd Server: http://10.50.22.9:8000
```

## Reporting 
#### Executive Summary 
  - Dummy Summary, for the dummies
#### Technical Summary
  - Who, what, when, where, and why of the pen testing
  
  
showdan - subscription to googleish thing for IOT devices

---
## Exploitation Research

initial access - first way into a system 
  - most common method for gaining initial access?
    - phishing, spear phishing is more targeted and specific phishing
  - other techniques:
    - default credentials, stolen credentials, password spraying, password/credential reuse, watering hole attacks
    targets of opportunity, public service exploitation, webserver exploitation, network binary exploitation
    
Learn to pair vulnerabilities to exploits
  - not every vulnerabilities will actually be exploitable

### Research
- confidential/Top Secret research isnt always better than open source research
  - *Intelligence* is processed information, *Information* is just collected info 

### Testing
- Test and verify for success
  - testing provides a number of benefits:
    - faster time to breakout of initial foothold
    - reduce risk of detection and tool failure
    - improved recovery times
   
## RECONNAISSANCE
**OSINT** - According to SANS: "Open Source Intelligence (OSINT) refers to a collection of data from public sources to be used in an intelligence context, and this type of information is often missed by link crawling search engines such as Google."

**OSINT** - According to DoD: "produced from publicly available information that is collected, exploited, and disseminated in a timely manner to an appropriate audience for addressing a specific intelligence requirement.”

Data to collect:
  - Web Data
  - Sensitive Data
  - Publicy Accessible
  - Social Media
  - Domain and IP Data
  - Much more

Scraping Data:
  - can have a python script to scrape specific data from websites
  
  ```python 
import lxml.html
import requests

page = requests.get('http://quotes.toscrape.com')
tree = lxml.html.fromstring(page.content)

authors = tree.xpath('//small[@class="author"]/text()')

print ('Authors: ',authors)
```
`Authors:  ['Albert Einstein', 'J.K. Rowling', 'Albert Einstein', 'Jane Austen', 'Marilyn Monroe', 'Albert Einstein', u’Andr\xe9 Gide', 'Thomas A. Edison', 'Eleanor Roosevelt', 'Steve Martin']`
keep this script to modify throughout activities

OCO - DO NOT SKIP STEPS 

#### Scanning steps
  1. Host Discovery
    - Find hosts that are online
  2. Host Enumeration
    - Find ports for each host that is online
  3. Host interrogation
    - Verify the service that is runnig on each open/available port
      - port 22 does not necessarily mean SSH (but it probably will)
      -  banner grab


nmap scripts are stored in /usr/share/nmap/scripts

```bash
nmap --script <filename>|<category>|<directory>
nmap --script-help "ftp-* and discovery"
nmap --script-args <args>
nmap --script-args-file <filename>
nmap --script-help <filename>|<category>|<directory>
nmap --script-trace
```
`nmap -Pn -T4 --min-rate 64654354987 10.50.22.27 -p-`
- -p- is all ports
- -p 21-24,80,8080
`nc 10.50.22.27 22`
- verifying what 22 is

`nmap -Pn -T4 --min-rate 64654354987 10.50.22.27 -p21-24,80,8080 --script=http-enum`
- shows possible directories this website has 

`nmap -Pn -T4 --min-rate 64654354987 10.50.22.27 -p21-24,80,8080 --script=http-robots.txt`
- will pull (if it exists) the robots.txt file

`nmap -Pn -T4 --min-rate 64654354987 10.50.27.25 -p445,139,135 --script=smb-os-discovery`
- if those ports are open, it will pull info from those ports (windows machine with smb open)
- confirms it is smb and pulls OS information
- (you know its a windows machine if 445, 135, 9999, 3389 are open)







