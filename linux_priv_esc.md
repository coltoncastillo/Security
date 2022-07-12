#### ENUMERATION FOR PRIVILEGE ESCALATION
  - What are your techniques and processes?
  - Any particular order?
  - Anything else you should be doing while on the box?
---
`sudo -l` to check what commands the current user can sudo
---
#### SUID/SGID
  - lets you run something as a specific user or specific group
  - can abuse for your own convenience

---
#### Unsecure Permissions
  - Cron
  - World Writable files and directories (any authorized user can write to (/tmp is a good one))
  - Dot '.' in the path
  - fsssds
