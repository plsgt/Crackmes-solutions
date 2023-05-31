## Initial observations

```console
$ file hackme_reach_lvl_9000.exe 
hackme_reach_lvl_9000.exe: PE32+ executable (console) x86-64, for MS Windows
```

```console
$ wine64 hackme_reach_lvl_9000.exe
Welcome to Ph-Fox CLI game!
Note! the level will reset when you close the program.
Reach Level 9000 to get the flag! Goodluck!!

=====================================
Press enter to continue...
Level: 1/9000
140 + 584
Answer:
```

So, we understand that there are two ways to get the flag:

1. get to level 9000 by solving each level correctly.
2. RE the exe to jump to level 9000 directly.

## Ghidra observations

The `main()` stores a few binary numbers in different strings, aptly named confuse1, confuse2,... . Converting from binary to ASCII revealed that those are red herrings, and not directly related to the levels. Further down, we can see that there are two variables:   

```cpp
max_level = 9000;
current_lvl = 1;
```

and the rest of the code goes on. If we can modify the `current_lvl` to be 9000 at the beginning of program execution, then we should be able to get the flag. Thus, we patch the line:
```assembly
00401bbd c7 85 5c         MOV           dword ptr [RBP + 0x25c],0x1
		02 00 00 
		28 23 00 00
```
to

```
00401bbd c7 85 5c         MOV           dword ptr [RBP + 0x25c],0x2328
		02 00 00 
		28 23 00 00
```

then save and export the file to original format. Now, when we run the program, it gives us the flag. It does not matter what value we input for the level 9000 question.

```console
$ wine64 hackme_reach_lvl_9000_mod.exe 
Welcome to Ph-Fox CLI game!
Note! the level will reset when you close the program.
Reach Level 9000 to get the flag! Goodluck!!

=====================================
Press enter to continue...
Level: 9000/9000
140 + 584
Answer:
flag{Sh13sh_R3v3rs3_Engineering_G0dz69}
OWO SHIESHH YOU'RE ON FIRE!!!
``` 

### Answer: flag{Sh13sh_R3v3rs3_Engineering_G0dz69}