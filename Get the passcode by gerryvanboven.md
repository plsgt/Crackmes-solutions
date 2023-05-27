## Initial observations: 

```
$ sh ./crackMe
./crackMe: ./crackMe: cannot execute binary file
```

This is the output when trying to run the executable:
```
~  /Users/saugata/Desktop/Projects/crackmes/Get_the_passcode_by_gerryvanboven/crackMe; exit
zsh: exec format error: /Users/saugata/Desktop/Projects/crackmes/Get_the_passcode_by_gerryvanboven/crackMe
 Session Ended
 ```
 
Since, it is a linux executable file (ELF), I was unable to run on my Mac.

Analysing the binary using Ghidra, I can immediately see that the main() prints: "input PassCode! :" and accepts an integer input which it compares with an existing integer. Is both the numbers match, it prints "right !". With this I conclude that the existing integer is the correct password.

Thus, correct passcode is: 1245444

Verified by running the executable on Ubuntu VM and the cracked password works.