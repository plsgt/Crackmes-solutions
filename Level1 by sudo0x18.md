## Initial observations

```
 file level1 
level1: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=89f40555f67806b4082e5785d91836bb6baaaa9d, for GNU/Linux 3.2.0, not stripped
```

```
 ./level1 
zsh: exec format error: ./level1
```

```
~  /Users/saugata/Desktop/Projects/crackmes/Level1_by_sudo0x18/level1 ; exit;
zsh: exec format error: /Users/saugata/Desktop/Projects/crackmes/Level1_by_sudo0x18/level1

Saving session...
...copying shared history...
...saving history...truncating history files...
...completed.

[Process completed]
```

Since, it is a linux executable file (ELF), I was unable to run on my Mac.

## Running Ghidra:

The `main()` shows that the program takes some string as input and sends the input as argument to `checkPass()` for verification.

The `checkPass()` compares the input string by each character sequentially with a predefined character set. If all the characters in each position match, then it is a match for the password. From this function, we get the correct password.

The correct password is: sudo0x18

### Verified by running the executable on Ubuntu VM and the cracked password works.