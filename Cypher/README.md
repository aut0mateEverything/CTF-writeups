## Step 1: Scan for Open Ports

First thing, let's scan for open ports with the following `nmap` command:

```bash
nmap -sV -sC -p- --defeat-rst-ratelimit -O -A cypher.htb
```
## Scan results:
![Nmap port scan](img/nmap.png)

## Step 2: Investigate website

With only ports 80 and 22 open, we’ll start by examining the web service.

![Login page](img/loginpage.png)

## Step 3: Try SQL injection

After trying some SQL payloads we can see that there is a huge error popping up. This strongly suggests a potential SQL injection vulnerability.

![Login page after injecting 'OR 1=1](img/image.png)
