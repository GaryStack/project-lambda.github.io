---
layout: post
title: "POJ 2406 Power Strings"
date: 2018-5-8
categories:
  - 题解
description: 都是抄的
image: https://img01.sogoucdn.com/app/a/100520024/edce971fa31bce8f165e09db85fe5c96
image-sm: https://img01.sogoucdn.com/app/a/100520024/edce971fa31bce8f165e09db85fe5c96
---


## [ 题目链接](http://poj.org/problem?id=2406)


## 输入输出样例

**Sample Input**

abcd

aaaa

ababab

.

**Sample Output**

1

4

3

### 题解：

这个题实际上是有一个结论的，刚开始我并不知道有这个结论，结果还想从小到大枚举长度来做（~~傻得一匹~~）

然后这个结论是，如果设当前的长度是len，next数组是1~len的话。

如果存在`len%(len-next[len])==0`，则存在一个循环字节，且这个字节的循环次数是`len/(len-next[len])`。

反之，则不存在这样的字节。

#### 举例子式的证明：

设S=q1q2q3q4q5q6q7q8，并设next[8] = 6，此时str = S[len - next[len]] = q1q2，由字符串特征向量next的定义可知，q1q2q3q4q5q6 = q3q4q5q6q7q8，即有q1q2＝q3q4，q3q4＝q5q6，q5q6＝q7q8，即q1q2为循环子串，且易知为最短循环子串。由以上过程可知，若len可以被len - next[len]整除，则S存在循环子串，否则不存在。

~~我才不会告诉你我其实不会证明这个结论~~

恳请过路dalao不吝赐教这个结论应该如何证明。

### 代码：

```cpp
#include <iostream>
#include <cstring>
#include <cstdio>
#include <algorithm>

using namespace std;

const int maxn=10000000+5;

int next[maxn];
char tmp[maxn];

void GetNext(int len){

    memset(next,0,sizeof(next));
    next[0]=-1;
    int i=0,j=-1;
    while(i<len)
    {
    	while(j!=-1 && tmp[i]!=tmp[j]) j=next[j];
    	next[++i]=++j;
	}
}

int main()
{
    while(scanf("%s",tmp)==1){
        if(tmp[0]=='.') break;
        int len=strlen(tmp);
        GetNext(len);
        if(len%(len-next[len])==0){
            printf("%d\n",len/(len-next[len]));
        }
        else printf("1\n");
    }

    return 0;
}

```

——根本不会KMP的GaryStack
