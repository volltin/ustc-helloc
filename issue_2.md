# Hello C (Issue 2)

**Welcome to follow us on WeChat: USTC_CS**

![QRCODE](https://raw.githubusercontent.com/volltin/ustc-helloc/master/qrcode.jpg)

## Program 1 : 生成 1 到 n 这 n 个数字的所有排列。

```c
/**********************************************************************
 * Permutation
 * 2016-10-27
 ************************************************************************/

#include <stdio.h>
#define NUM_N 4

void print_array(int *arr, int n)
{
	for (int i = 0; i < n; ++i) printf("%d ", arr[i]);
	printf("\n");
}

void permutation(int *arr, int begin, int end)
{
	int t;
    if (begin == end) print_array(arr, end + 1);
    else
    {
        for(int i = begin; i <= end; ++i) 
        {
            t = arr[i]; arr[i] = arr[begin]; arr[begin] = t;
            permutation(arr, begin + 1, end);
            t = arr[i]; arr[i] = arr[begin]; arr[begin] = t; // restore it.
        }
    }
}

int main()
{
    int a[NUM_N];
    for (int i = 0; i < NUM_N; ++i) a[i] = i + 1;
    permutation(a, 0, NUM_N - 1);
    return 0;
}



```

## Program 2 : （约瑟夫问题）编号为 1，2,...,n 的 n 个人围成一圈，依次报数 1,2,3 ，每次报到 3 的人退出，下一个人重新从 1 开始报数，求解剩下的最后一个人初始编号为多少。

```c
/**********************************************************************
 * Josephus Problem
 * 2016-10-27
 ************************************************************************/

#include <stdio.h>
#include <stdlib.h>

typedef struct linkedlist linkedlist;

struct linkedlist
{
    linkedlist *prev, *next;
    int value;
};

linkedlist* build_circle(int n)
{
    linkedlist *head, *tail;
    linkedlist *t;
    tail = head = (linkedlist*)malloc(sizeof(linkedlist));
    tail->value = 1;
    for (int i = 2; i <= n; ++i)
    {
        t = (linkedlist*)malloc(sizeof(linkedlist));
        t->value = i;
        t->prev = tail;  // link to previous item
        tail->next = t;
        tail = t;
    }
    // OK, now we roll the line into a circle
    tail->next = head;
    head->prev=tail;
    return head;
}

int main()
{
    int n = 1;  // we skip the input process...
    linkedlist* head = build_circle(n);
    while(head->next != head)
    {
        head = head->next->next;   // 1, 2, 3, kick out
        head->prev->next = head->next;
        head->next->prev = head->prev;
        head = head->next;
    }
    printf("The last one is %d\n", head->value);
    return 0;
}
```

## Program 3 : 输入 a 和 n，a 代表一个数字，计算 a+aa+aaa+...+ aaa...a（n 位）。

```c
/*
 * problem description:
 * input : a and n, 
 * 	a reprensents the number, 
 * 	n reprensents the number of digits
 * output: Sn
 * 	Sn=a+aa+aaa+...+ a...a
 * 			------
 * 		    the number of a is n	
 * */
#include <stdio.h>
#include <math.h> 
int main()
{
	int a,n,i,Sn=0,j=0;
	printf("请输入一个数和您需要的位数\n");
	scanf("%d%d",&a,&n);
	/*
	 * for-loop, in each loop :
	 * first: we calculate corresponding 11...1
	 *  	for example: in t-th loop, j is 11..11, 
	 * 	the number of 1 is t.
	 * second: calculate corresponding addend a*j, 
	 * 	and add it with augend Sn
	 * */
	for(i=1;i<=n;i++)
	{
		// in t-th looper, variable j is 11..11, the number of 1 is t in total
		j=j+pow(10,i-1);
		// add the product of a and j to the result Sn
		Sn=Sn+a*j;
	}
	printf("Sn=%d",Sn);
	return 0;
}

```

## Program 4 : 对 4 个数进行排序并输出

```c
/*
 * problem description:
 * input:  four numbers
 * output: sort the four number and output them ascend
 * */

#include <stdio.h>
int main()
{
	int a[4],i,j,m;
	printf("please input four number:\n");
	for(i=0;i<4;i++)
	{
		scanf("%d",&a[i]);
	}
	/*
	 * Selection Sort:
	 * in i-th loop, choose the smallest number and exchange with i-th number
	 * */
	for(i=0;i<4;i++)
	{
		for(j=i+1;j<4;j++)
		{
			if(a[i]>a[j])
			{
				m=a[i];
				a[i]=a[j];
				a[j]=m;
			}
		}
	}	
	printf("由小到大的顺序是：\n");
	for(i=0;i<4;i++)
		printf("%d\t",a[i]);
	return 0;
}
```
