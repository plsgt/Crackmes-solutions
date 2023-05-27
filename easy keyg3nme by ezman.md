## Initial observations

```
 file keyg3nme     
keyg3nme: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, BuildID[sha1]=01d8f2eefa63ea2a9dc6f6ceb2be2eac2ca22a67, for GNU/Linux 3.2.0, not stripped
```

A Linux executable

```
$ ./keyg3nme 
Enter your key:  12
nope.
```

## Ghidra observations

The main function accepts an integer input, and compares the integer with a hardcoded value in `validate_key()`. The hardcoded value is 1223. Thus, upon entering 1223 as key, it accepts the value.

```
$ ./keyg3nme 
Enter your key:  1223
Good job mate, now go keygen me.
```