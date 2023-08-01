check for robots.txt -> we see that one endpoint is not allowed: /ftp
when we visit it and see there's a folder called quarantine -> looking inside it we see malware files for different arch. and os
so not to meddle with it for now , we also check if we can send or put a file onto that endpoint via CURL it is actually a good practice to check:
![[Pasted image 20230715182741.png]]
we see PUT method is allowed , so shall we put a file?:
![[Pasted image 20230715182938.png]]
we can read the files with pdf and md extensions so there was one so we read it
![[Pasted image 20230715183043.png]]
we also see : legal.md and announcement_encrypted.md -> the enc. file looks juicy so we download it
On googling the first has value we get:
![[Pasted image 20230715183614.png]]

we also get this .kdbx file which on further analysis we get to know that it is a keypass database file , we can decrypt it via :
```
keepass2john incident-support.kdbx > keypass.txt
```
maybe we can find the key for that above hashes
we can decrypt this file via john with the wordlist rockyou
```
john --wordlist=/usr/share/wordlists/rockyou.txt keypass.txt
```
and we get the password: `*7¡Vamos!`

