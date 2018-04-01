---
layout: post
title: "Hello World"
date: 2018-4-1
categories:
  - HelloWorld
description: Hello World
image: https://github.com/GaryStack/GaryStack.github.io/blob/master/background/Other/%E9%9D%9E%E5%8A%A8%E6%BC%AB/08.jpg?raw=true
image-sm: https://github.com/GaryStack/GaryStack.github.io/blob/master/background/Other/%E9%9D%9E%E5%8A%A8%E6%BC%AB/08.jpg?raw=true
---

Hello World

```javascript
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
#include <cstdlib>
#define mod 1000000007
long long ans=0;

using namespace std;

struct Matrix{
	long long a[130][130];
	int n,m;
	Matrix(int nn,int mm)
	{
		memset(a,0,sizeof(a));
		n=nn;m=mm;
	}
	void init(int x)
	{
		n=m=x;
		for(int i=0;i<x;i++) a[i][i]=1;
	}
	Matrix operator*(const Matrix &b)
	{
		Matrix ans(n,b.m);
		for(int i=0;i<n;i++)
			for(int j=0;j<b.m;j++)
				for(int k=0;k<m;k++)
					(ans.a[i][j]+=(a[i][k]*b.a[k][j])%mod)%=mod;
		return ans;
	}
}st(1,10),ma(10,10);
Matrix fstpow(Matrix a,long long b)
{
	Matrix res(a.n,a.n);
	res.init(a.n);
	while(b){
		if(b&1) res=res*a;
		a=a*a,b>>=1;
	}
	return res;
}
int main()
{
	long long n;scanf("%lld",&n);
	for(int i=1;i<10;i++) st.a[0][i]=1;
	if(n==1) {
		printf("10");
		return 0;
	}
	for(int i=0;i<10;i++)
		for(int j=0;j<10;j++)	
			if(abs(i-j)<=2) ma.a[i][j]++;
	
	ma=st*fstpow(ma,n-1);
	for(int i=0;i<10;i++) ans=(ans+ma.a[0][i])%mod;
	printf("%lld\n",ans);
	return 0;
}
```
