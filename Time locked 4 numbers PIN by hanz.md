## Initial observations

The zip opened to reveal an exe file. I did not expect an exe file since Platform was mentioned as Mac OS X. Anyways,

```
 file bro.exe 
bro.exe: PE32 executable (console) Intel 80386, for MS Windows
```

```
 wine64 bro.exe
PIN: 123
Try again.
PIN: 234
Try again.
PIN: 1123
Try again.
PIN: Try again.
PIN: 1
Try again.
You're locked for a minute for breaching in. :(
0114:fixme:console:default_ctrl_handler Terminating process 100 on event 0
```

## Ghidra analysis

Inside the `main()`, we see a few variables et defined, and a counter which increments for each incorrect attempt. There is a check condition that matches input passwords with a number, and if they match, breaks out of the loop to print success. This has to be the actual PIN.

I ran the file once again with this PIN as input and it outputs success.

### Correct PIN: 4877 