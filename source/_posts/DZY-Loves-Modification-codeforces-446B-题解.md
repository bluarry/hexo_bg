---
title: DZY Loves Modification(codeforces 446B)题解
date: 2016-08-19 08:36:46
categories: [ACM]
tags: 
- ACM
- 算法
- 题解
---

<blockquote class="blockquote-center"><h1>codeforces 446B题解</h1></blockquote>
![](http://i4.buimg.com/572447/255164a8de885ede.png)
>**DZY Loves Modification(codeforces 446B)**&nbsp;&nbsp;["传送门"](http://codeforces.com/problemset/problem/446/B "传送门")<br>
<!--more-->
## Description
> As we know, DZY loves playing games. One day DZY decided to play with a n × m matrix. To be more precise, he decided to modify the matrix with exactly k operations.<br>

>Each modification is one of the following:<br>
	
 >&nbsp;&nbsp;&nbsp;&nbsp;1.Pick some row of the matrix and decrease each element of the row by p. This operation brings to DZY the value of pleasure equal to the sum of elements of the row before the decreasing. <br>
 >&nbsp;&nbsp;&nbsp;&nbsp;2.Pick some column of the matrix and decrease each element of the column by p. This operation brings to DZY the value of pleasure equal to the sum of elements of the column before the decreasing. 	<br>

 ## INPUT
 >The first line contains four space-separated integers n, m, k and p (1 ≤ n, m ≤ 103; 1 ≤ k ≤ 106; 1 ≤ p ≤ 100).Then n lines follow. Each of them contains m integers representing aij (1 ≤ aij ≤ 103) — the elements of the current row of the matrix.<br>

 ## Output
 >Output a single integer — the maximum possible total pleasure value DZY could get.<br>

 #Sample Input
 > Input<br>
2 2 2 2<br>
1 3<br>
2 4<br>
>Output<br>11
>Input<br>
2 2 5 2<br>
1 3<br>
2 4<br>
>Output<br>11
## Hint
```
For the first sample test, we can modify: column 2, row 2. After that the matrix becomes:


1 1
0 0

For the second sample test, we can modify: column 2, row 2, row 1, column 1, column 2. After that the matrix becomes:


-3 -3
-2 -2
```

## 题意解释：<br>
> 这题的意思是，给你个矩阵，对它的行和列进行操作，即每次对每一行或者每一列减p，<br>
在之前应该求出操作每一行和列的和，求k次操作之后所能得到的所有行和列的最大和。

## 题目分析:<br>
>这题说难其实不难，可是我却犯了一个重大的错误，说出来共勉，就是我开数组直接开到main中<br>
结果内存爆炸啦，之后开到全局之后就好啦，至于原因这里不赘述，请去百度<br>
言归正传，这道题要求的是行和列的和，可以预处理出来，然后，最后再处理，达到k次之后<br>
可将对行和对列进行i次和k-i次的操作，最后要减去一个 i*(k-i)*p才能得到正解<br>
对了，这题用了优先队列，不会的话可以先去百度。。。

## ac代码：<br>
```c++
#include <iostream>
#include <stdio.h>
#include <string.h>
#include <algorithm>
#include <queue>
typedef long long ll;
using namespace std;


ll A[1005][1005];
ll s1[1000005],s2[1000005]; 
ll n,m,k,p;

ll sum_row(ll m,ll i){
	ll s=0;
	for(ll j=1;j<=m;j++) s+=A[i][j];
		return s;
}
ll sum_cow(ll n,ll i){
	ll s=0;
	for(ll j=1;j<=n;j++) s+=A[j][i];
		return s;
}
int main()
{	
//	freopen("D:\\in.txt","r",stdin);
	while(cin >> n >> m >> k >> p){
		ll i,j;
		memset(A,0,sizeof(A));
		memset(s1,0,sizeof(s1));
		memset(s2,0,sizeof(s2));
		for(i=1;i<=n;i++)
			for(j=1;j<=m;j++)
				cin >> A[i][j];
		priority_queue<ll>q1;
		priority_queue<ll>q2;
		for(i=1;i<=n;i++){
			q1.push(sum_row(m,i));
		}
		//同样求每一列
		for(i=1;i<=m;i++){
			q2.push(sum_cow(n,i));
		}
		//对每一行枚举从0到k次操作所能得到的happy值，并存入s1中
		for(i=1;i<=k;i++)
		{
			ll tem=q1.top();
			q1.pop();
			s1[i]=s1[i-1]+tem;
			tem-=p*m;
			q1.push(tem);
		}
		//队列同上
		for(i=1;i<=k;i++)
		{
			ll tem=q2.top();
			q2.pop();
			s2[i]=s2[i-1]+tem;
			tem-=p*n;
			q2.push(tem);
		}
		//最后枚举进行k次操作所能得到的最大解
		ll sum=-999999990000000;
		for(i=0;i<=k;i++){
			ll s=s1[i]+s2[k-i];
			sum=max(sum,s-i*(k-i)*p);
		}
		cout << sum <<  endl;
	}
	return 0;
}
```
## 最后说一句，写题解只为指导学习，并不是给你答案，所以，多思考才是对的