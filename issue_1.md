# Hello C (Issue 1)

**Welcome to follow us on WeChat: USTC_CS**
![QRCODE](https://raw.githubusercontent.com/volltin/ustc-helloc/master/qrcode.jpg)

## Program 1 : Example of string copy 

```c
/* 
 *  Example of string copy 
 */

#include <stdio.h>
#define BUF_SIZE 1024
int main()
{
    char src[BUF_SIZE], dst[BUF_SIZE];
    // Assumption :: input string length < BUF_SIZE, or it'll suffer from overflow.
    scanf("%s", src);
    /*
      Note: 
      1. declare i in for-loop, `-std=c99` required if compiler fails
      2. strcpy can be done in just 1 line.
      3. don't use strlen here -- it is just a waste of time for we can copy it until meet with '\0'
      4. see the brackets around `A = B`? It is a common notation for such case 
           that we really need `A = B` instead of `A == B` (sometimes A = B may just be a mistake). 
    */
    for (int i = 0; (dst[i] = src[i]); ++i);
    return 0;
}
```

## Program 2 : Example of string concat

```c
/* 
 *  Example of string concat 
 */

#include <stdio.h>
#define BUF_SIZE 1024

void strcpy(char *dst, char *src)
{
    for (int i = 0; (dst[i] = src[i]); ++i);
}

/* strcat(A, B) => AB (This will change what was in a) */
void strcat(char *dst, char *src)
{
    int i = 0;
    // Note: i updates to i + 1, and the value of expression `i++` is i
    while (dst[i++]);
    // Note: after while-loop exits, `i` is just after '\0' (because of i++),
    //   so just fix it with `i - 1` 
    strcpy(&dst[i - 1], src);
}

int main()
{
    char src[BUF_SIZE], dst[BUF_SIZE];
    // Assumption :: sum of input string length < BUF_SIZE, or it'll suffer from overflow.
    printf("Please input two strings for concat: \n");
    scanf("%s%s", src, dst);
    strcat(dst, src);
    printf("result: %s\n", dst);
    return 0;
}
```
