# Cyber_k

### Challenge Description :



##### Author - k1n0r4

<hr>

### Solution


We quickly find that the binary is using `rand` and `srand`.

The man page states the following for `srand`.

```
The srand() function sets its argument as the seed for a new sequence  of
       pseudo-random  integers  to  be  returned by rand().  These sequences are
       repeatable by calling srand() with the same seed value.
```


![Screenshot 2024-03-10 054402](https://github.com/dystp1a/revshaktictf24/assets/143863591/77584c38-878b-4218-9895-6bb51ebad6ed)
![Screenshot 2024-03-10 054416](https://github.com/dystp1a/revshaktictf24/assets/143863591/0b155135-301b-448b-8eb1-825523f864b3)

In each iteration, the AND operation is performed on the result of rand() with 15, and the outcome is stored in v8. Subsequently, this value is XORed with each character of the input provided. Through a loop, the program checks if the result matches the values stored in v9.

By XORing the rand() values with the given decimals, the flag is derived.


```c
#include <stdio.h>
#include <stdlib.h>

int main() {
int i,j,k;
int v8[36];
char s[40];
srand(123);
for (i = 0; i <= 34; ++i)
v8[i] = rand() & 0xF;
int v9[35] = {114,109,96,101,115,98,104,122, 108, 122, 119, 100,49,84,119,49,108,99,89,103,98,49,108,88,49,125,83,126,59,98,105,48,108,49,114};
for (j = 0; j <= 34; ++j)
       s[j]=v9[j]^v8[j];
printf("%s",s);}
```

correct input: shaktictf{wh0_s4id_fl4g_1s_r4nd0m?}
