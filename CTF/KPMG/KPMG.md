## rev
### unveiling the hidden message
![[Pasted image 20230728123440.png]]
### Enigma Binary:
1. `xor_cipher` function: This function performs a simple XOR cipher on the data starting at address `param_1` with a repeating key. The key is derived from the data starting at address `param_3`, and its length is `param_4`. The function iterates through the data and XORs each byte with the corresponding byte from the key. This function is used to decrypt the flag.
    
2. `main` function: The main function checks if there is at least one argument provided to the program (`1 < param_1`). If there is at least one argument, it compares the value of the first argument (the string at address `param_2 + 8`) with the string "error". If the comparison is successful (`iVar1 == 0`), the program decrypts the flag using the `xor_cipher` function and prints the decrypted flag. Otherwise, it prints "Not_so_easy".
![[Pasted image 20230730003633.png]]
![[Pasted image 20230730003730.png]]
![[Pasted image 20230730003519.png]]

## OSINT
### Time capsule
![[Pasted image 20230728124347.png]]
`KPMG_CTF{c7a23eb0583a89461bf7046d0eddbe31}`

### hidden network conquest
![[Pasted image 20230728124651.png]]

![[Pasted image 20230728124637.png]]
https://www.instagram.com/4dity4k/
https://www.instagram.com/santheep__k/

## Cloud
### Secure Storage Showdown
![[Pasted image 20230728130909.png]]

### IAM
![[Pasted image 20230728163421.png]]
![[Pasted image 20230728163559.png]]
Flash_cards -> aws.json
![[Pasted image 20230728163837.png]]


## Web
### Breakout unleash the flag
![[Pasted image 20230728132848.png]]
![[Pasted image 20230728132810.png]]

### Enigmatic Layrinth
![[Pasted image 20230728133902.png]]
![[Pasted image 20230728134058.png]]
![[Pasted image 20230728190713.png]]
## SQL
![[Pasted image 20230729185605.png]]
![[Pasted image 20230729185830.png]]

![[Pasted image 20230730002458.png]]
![[Pasted image 20230730123332.png]]
![[Pasted image 20230730123350.png]]
![[Pasted image 20230730130756.png]]
![[Pasted image 20230730130808.png]]
2' GROUP by 2 #
2' UNION SELECT games.id, games.name,NULL,NULL AS total_score FROM games GROUP BY games.id, games.name;  #
### IMG
![[Pasted image 20230728183720.png]]



## Crypto
## ATBASH:
![[Pasted image 20230728184711.png]]

## XOR:
```
def xor_decrypt(ciphertext, key):
    decrypted = ""
    for i in range(0, len(ciphertext), 2):
        hex_pair = ciphertext[i:i+2]
        decrypted += chr(int(hex_pair, 16) ^ ord(key))
    return decrypted

ciphertext = "06216f3b272a6f3d2a2e23226f20296f2c202b2a3c6f2e212b6f2c3d363f3b262c6f2e3d3b634518272a3d2a6f2226212b3c6f3a21263b2a636f2e6f2c272e23232a21282a6f3b206f26223f2e3d3b61450c1b09636f2e6f3e3a2a3c3b6f29203d6f3b272a6f2c3a3d26203a3c6f3c203a2363451f3a3535232a3c6f3b206f3c2023392a636f3b272a6f22363c3b2a3d262a3c6f3a212920232b6145450d363b2a3c6f2b2e212c2a6f2e212b6f242a363c6f3827263c3f2a3d6f3c2a2c3d2a3b3c6f3a213b20232b634506216f3b27263c6f2b2628263b2e236f2e3d2a212e636f272a2e3d3b3c6f2e3d2a6f2d20232b6145072e2c242a3d3c6f2e212b6f3b272621242a2d3c6f3b20282a3b272a3d6f3b272a366f3c3b3d26392a63451b206f2c20213e3a2a3d6f3b272a6f29232e283c636f2e212b6f3b272a6f2823203d366f2b2a3d26392a61454506216f2a392a3d366f2c272e23232a21282a636f24212038232a2b282a6f263c6f282e26212a2b634506216f0c1b09683c6f2b20222e2621636f3f2e3c3c2620213c6f3a212c272e26212a2b6145042a366f263c6f041f0208340c3d363f3b262c102e3d3b103a212920232b2a2b32"

# Try all possible ASCII characters (0 to 127) as the key
f = open("temp.txt","a")
for key in range(128):
    decrypted_message = xor_decrypt(ciphertext, chr(key))
    f.write(decrypted_message)
```

![[Pasted image 20230728143907.png]]
`KPMG{Cryptic_art_unfolded}`

## Infrastructure 
### forbidden telnet
![[Pasted image 20230728144238.png]]

### OTP portal
nmap:
![[Pasted image 20230728144647.png]]
anon login enabled:
![[Pasted image 20230728144748.png]]
Inside it was the sql file
![[Pasted image 20230728191826.png]]
![[Pasted image 20230729235759.png]]

## GIT 1:
gittools -> github -> dumper.sh
`ftp://anonymous:anonymous@143.110.180.89/.git/`
when did ftp got the login.html and a .git folder 
inside the commit history:
![[Pasted image 20230729194757.png]]
`ssh -i id_rsa charlie@0.cloud.chals.io -p 20749`
and cat user.txt

## GIT 2
![[Pasted image 20230729212326.png]]

![[Pasted image 20230729212449.png]]

### Hydra:
![[Pasted image 20230730144158.png]]

![[Pasted image 20230730144313.png]]


`viyl2fvhynlomzzbskfwrkpsx34cd2tfg2tz2htmagwfteuysf72twad.onion`

![[Pasted image 20230729132719.png]]

## MISC:
![[Pasted image 20230729184712.png]]
![[Pasted image 20230729184742.png]]

![[Pasted image 20230729184808.png]]

![[Pasted image 20230729184641.png]]

## Mobile Pentest
![[Pasted image 20230730004241.png]]

6StMUHY0Gpi1z2LeSitU1UigOQWgLHLWinr21

