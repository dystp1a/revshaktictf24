# revshaktictf24

![Screenshot 2024-03-09 100544](https://github.com/dystp1a/revshaktictf24/assets/143863591/d2285efd-a354-4968-a30d-a74e1c55a15e)

Challenge writeup:

From the pseudocode, it takes an input and reverses it and stores it in s, and checks if it equal to s2.
On reversing the string stored in s2, we get the flag




![Screenshot 2024-03-10 054402](https://github.com/dystp1a/revshaktictf24/assets/143863591/77584c38-878b-4218-9895-6bb51ebad6ed)
![Screenshot 2024-03-10 054416](https://github.com/dystp1a/revshaktictf24/assets/143863591/0b155135-301b-448b-8eb1-825523f864b3)
We quickly find that the binary is using `rand` and `srand`.

The man page states the following for `srand`.

```
The srand() function sets its argument as the seed for a new sequence  of
       pseudo-random  integers  to  be  returned by rand().  These sequences are
       repeatable by calling srand() with the same seed value.
```
Each iteration of rand is `and` with 15 and stored in v8. which is then xor'd with each of the entered input. Through a loop, it is checked, if it equal to the values provided in v9.

On xoring the rand() values and the given decimals, we get the flag 

![Screenshot 2024-03-09 113600](https://github.com/dystp1a/revshaktictf24/assets/143863591/9dd96a80-8014-42b7-a9d5-cd4ff55c56bf)




```python 
import base64

def func_1(unk_str0, unk_str):
    flag_len = len(unk_str0)
    unk_str_len = len(unk_str)

    unk_str1 = bytearray(unk_str0, 'utf-8')

    for i in range(flag_len):
        unk_str1[i] = unk_str1[i] ^ ord(unk_str[i % unk_str_len])

    return unk_str1.decode('utf-8')

def func_2(unk_str0):
    flag_len = len(unk_str0)
    unk_str3 = [''] * flag_len

    j = 0

    for i in range(0, flag_len , 4):
        unk_str3[j] = unk_str0[i]
        unk_str3[j + 1] = unk_str0[i + 1]
        j += 2

    for i in range(2, flag_len, 4):
        unk_str3[j] = unk_str0[i]
        unk_str3[j + 1] = unk_str0[i + 1]
        j += 2

    return ''.join(unk_str3)

def main():
    unk_str = "U2hhZG93MjAyNA=="
    unk_str = base64.b64decode(unk_str.encode('ascii')).decode('ascii')

    unk_str0 = input("Enter the input: ")

    unk_str1 = func_1(unk_str0, unk_str)

    unk_str2 = func_2(unk_str1)

    unk_arr0 = [32, 0, 27, 30, 84, 79, 86, 22, 97, 100, 63, 95, 60, 34, 1, 71, 0, 15, 81, 68, 6, 4, 91, 40, 87, 0, 9, 59, 81, 83, 102, 21]

    for i in range(len(unk_str0)):
        if unk_arr0[i] != ord(unk_str2[i]):
            exit(0)

    print("\nCorrect Flag!\n")

if __name__ == "__main__":
    main()
```

* unk_str after base64 decoded is `Shadows2024`. 
* The func_1 is called with arguments unk_str and the input flag(unk_str0), where xor operation is performed on each character from unk_str0 w repeated sequence of unk_str.
* The output of func_1 is passed to func_2, where an empty list unk_str3 is initialised. 
* In 2 Loops, with every iteration over the input flag, it takes 2 values from the input str and stores it in the empty str. and returned to unk_str2
* this final string is compared with a predefined set of ascii values(unk_arr0). If comparison is succesful, then the input is right.

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
