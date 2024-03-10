# Ultra

### Challenge Description :



##### Author - k1n0r4

<hr>

### Solution

* unk_str after base64 decoded is `Shadows2024`. 
* The func_1 is called with arguments unk_str and the input flag(unk_str0), where xor operation is performed on each character from unk_str0 w repeated sequence of unk_str.
* The output of func_1 is passed to func_2, where an empty list unk_str3 is initialised. 
* In 2 Loops, with every iteration over the input flag, it takes 2 values from the input str and stores it in the empty str. and returned to unk_str2
* this final string is compared with a predefined set of ascii values(unk_arr0). If comparison is succesful, then the input is right.
### Solution script
On reversing func_2, by inputting the given ascii values, and perform the same opertaions. We get the input to the func_2, which on xoring with Shadow2024, the flag is obatined.
``` python 
def func_2():
    unk_str3 = [32, 0, 27, 30, 84, 79, 86, 22, 97, 100, 63, 95, 60, 34, 1, 71, 0, 15, 81, 68, 6, 4, 91, 40, 87, 0, 9, 59, 81, 83, 102, 21]
    flag_len = len(unk_str3)
    unk_str0 = ['']*flag_len

    j = 0

    for i in range(0, flag_len , 4):
        unk_str0[i] = unk_str3[j]
        unk_str0[i + 1] = unk_str3[j + 1]
        j += 2

    for i in range(2, flag_len, 4):
        unk_str0[i] = unk_str3[j]
        unk_str0[i + 1] = unk_str3[j + 1]
        j += 2

    return unk_str0
unk_str1=func_2()
print(unk_str1)
```
```[32, 0, 0, 15, 27, 30, 81, 68, 84, 79, 6, 4, 86, 22, 91, 40, 97, 100, 87, 0, 63, 95, 9, 59, 60, 34, 81, 83, 1, 71, 102, 21]```

```python
li=[32, 0, 0, 15, 27, 30, 81, 68, 84, 79, 6, 4, 86, 22, 91, 40, 97, 100, 87, 0, 63, 95, 9, 59, 60, 34, 81, 83, 1, 71, 102, 21]
a="Shadow2024Shadow2024Shadow2024Shadow2024"
for i,j in zip(li,a):
  print(' '.join(chr(i^ord(j))),end="")
```
``` shaktictf{Ul7r4_STe4l7h_SUcc3s5}```
