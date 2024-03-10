
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
