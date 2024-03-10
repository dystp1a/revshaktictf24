
![Screenshot 2024-03-10 054402](https://github.com/dystp1a/revshaktictf24/assets/143863591/77584c38-878b-4218-9895-6bb51ebad6ed)
![Screenshot 2024-03-10 054416](https://github.com/dystp1a/revshaktictf24/assets/143863591/0b155135-301b-448b-8eb1-825523f864b3)

We quickly find that the binary is using `rand` and `srand`.

The man page states the following for `srand`.

```
The srand() function sets its argument as the seed for a new sequence  of
       pseudo-random  integers  to  be  returned by rand().  These sequences are
       repeatable by calling srand() with the same seed value.
```
the `and` operation is done on each iteration of rand  with 15 and stored in v8, which is then xor'd with each character of the entered input. Through a loop, it is checked, if it equal to the values provided in v9.

On xoring the rand() values and the given decimals, we get the flag 

![Screenshot 2024-03-09 113600](https://github.com/dystp1a/revshaktictf24/assets/143863591/9dd96a80-8014-42b7-a9d5-cd4ff55c56bf)
