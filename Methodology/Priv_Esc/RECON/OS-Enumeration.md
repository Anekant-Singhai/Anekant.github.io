#os-enum #privesc 
To explain you priv-esc I'll use the tryhackme room `Linux Privilege Escalation` , it might seem that "Yes I've done it" or "BOO too lame" but believe me the techniques we'll use will be great , just trust the processs

# Stage 1

## Enumeration:
***
### System enumeration
starting with the basics comes the command `lscpu` that gives us the information about the system that we have a hold of

look for the processes too via `ps -aux` they are much much important , they can tell you so much about what is going on , have a keen eye on the user who is running the process
this scenario is very much common we get a process for a root user and we try to execute the `/bin/bash`
binary over there getting root access

#### Operating system

What distribution and version is used?

```bash
$ cat /etc/issue
$ cat /etc/*-release
$ cat /etc/lsb-release
$ cat /etc/redhat-release
```

What is the Kernel version? Is it 64-bit?

```bash
$ cat /proc/version   
$ uname -a
$ uname -mrs
$ rpm -q kernel
$ dmesg | grep Linux
```

What can be learned from the environmental variables?

```bash
$ env
$ set
$ cat /etc/profile
$ cat /etc/bashrc
$ cat ~/.bash_profile
$ cat ~/.bashrc
$ cat ~/.bash_logout
$ cat ~/.zshrc
```

What services are running? And what users are they running as?

```bash
$ ps aux
$ ps -elf
$ top
$ cat /etc/service
```
Which service(s) are running as root? Of these services, which are vulnerable?

```bash
$ ps aux | grep root
$ ps -elf | grep root
```

What applications are installed? What version are they? Are they currently running?

```bash
$ dpkg -l
$ dpkg -l PACKAGE-NAME
$ rpm -qa
```

What jobs are scheduled?

```bash
$ crontab -l
$ cat /etc/cron*
$ cat /etc/cron.d/*
$ cat /etc/cron.daily/*
$ cat /etc/cron.hourly/*
$ cat /etc/cron.monthly/*
$ cat /etc/crontab
$ cat /etc/at.allow
$ cat /etc/at.deny
$ cat /etc/anacrontab
```

Find command to get executable files:
````bash
find . -type f -executable -print
````

