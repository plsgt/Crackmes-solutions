## Initial observations

```console
$ file alien_bin
alien_bin: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=51cd70ffbffd95a93eaf9d83e1f76c6274ef9c1b, for GNU/Linux 3.2.0, not stripped
```

```console
$ ./alien_bin
Feed me the right password: pass
ERROR
```

## Ghidra observations

Looking at `main()`, we can see that memory is allocated for the user passed input, and that is compared with another string. The inbuilt password is generated inside a loop.

We go out of Ghidra and use lptrace to see the password that the user passed string is being compared to. When we use this same string as our password, we are successful.

```console
$ ltrace ./alien_bin 
malloc(50)                                                                                                                    = 0x564c2aab62a0
printf("Feed me the right password: ")                                                                                        = 28
__isoc99_scanf(0x564c28c55025, 0x564c2aab62a0, 0, 0Feed me the right password: pass
)                                                                          = 1
malloc(50)                                                                                                                    = 0x564c2aab6b00
strcmp("pass", "bd23cf3f56baa86bc")                                                                                           = 14
puts("ERROR"ERROR
)                                                                                                                 = 6
+++ exited (status 0) +++

$ ./alien_bin 
Feed me the right password: bd23cf3f56baa86bc
blip blop :)
```

### Password: bd23cf3f56baa86bc
