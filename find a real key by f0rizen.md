## Initial analysis

```
$ file crackme       
crackme: ELF 64-bit LSB pie executable, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, not stripped
```

```
$ ./crackme 
Usage: ./crackme FLAG
$ ./crackme haha
Wrong flag
```

## Ghidra analysis

We can see that the program expects the value of flag to be passed with the executable. The `if` condition is satisfied when no arguments are passed with the executable.

This brings us to the `else` condition, where we pass the flag as argument to the crackme. We see that the function expects the flag to be of 21 characters. Then, the function stores the charcters of a string, each shifted by 34 in a byte array. Further down the code, there is a hardcoded array of integers. Finally, we can see that the function xors each element of the byte array with the correcponding element of the flag, and compares that with the corresponding element of the integer array. 

So, on reversing the xor, we can get the flag as: `flag = byteArray xor integerArray`

So, I have written a simple python script which gives me the flag.

```python
randomString = "sup3r_s3cr3t_k3y_1337" # hardcoded
randomStringInt = [0]*len(randomString)

for i in range(len(randomString)):	
	randomStringInt[i] = ord(randomString[i]) - 34
	
# store the xor output array values in an array
arrayPassInt = [55, 63, 47, 118, 43, 98, 40, 33, 52, 15, 119, 98, 72, 39, 117, 8, 86, 106, 104, 78, 104]

flag = ""

#retrieve one of the xor input by xoring the output with the second input
for i in range(21):
	flag += chr(randomStringInt[i] ^ arrayPassInt[i])

print(flag)
```

### Flag: flag{\_y0u\_f0und\_key\_} 

## Confirmation 

```shell
$ ./crackme asbdr
Wrong flag
$ ./crackme flag{_y0u_f0und_key_}
You found a flag! flag{_y0u_f0und_key_}
```