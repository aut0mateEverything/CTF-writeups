## Step 1: Scan for Open Ports

First thing, let's scan for open ports with the following `nmap` command:

```bash
nmap -sV -sC -p- --defeat-rst-ratelimit -O -A cypher.htb
```
## Scan results:
![Nmap port scan](img/nmap.png)

## Step 2: Investigate website

With only ports 80 and 22 open, we’ll start by examining the web service.

