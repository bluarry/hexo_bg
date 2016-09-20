---
title: codeforces 501E ( Misha and Palindrome Degree)
date: 2016-08-21 13:37:59
categories: [题解]
tags:
- ACM题解
- codeforces
---

<blockquote class="blockquote-center"><h1>codeforces 501E ( Misha and Palindrome Degree)</h1></blockquote>
![Markdown](http://i2.buimg.com/572447/cece616d34621821.jpg)
<!--more-->
>**Borya and Hanabi-codeforces 442A**&nbsp;&nbsp;["传送门"](http://codeforces.com/problemset/problem/501/E "传送门")<br>

> ## 原题大意为：给出n个数，若有一个区间，只重排那个区间的数字（可不排），使得数组是构成一个回文，<br>则这个区间就是答案之一
问你有多少个区间满足这种情况。

> ## 这题刚开始完全不会，，之后经过大神讲解才明白。<br>
>这题的大体思路是：<br>
从两端查找，然后找出第一对不相同的，以他们为左右端点，记为L,R; 分别从L,R枚举，找出两边最小的满足条件的区间<br>
然后记L找到的右区间为 right,记R找到的左区间为left，那么最后的答案就是 (l+1)*(r-left)+(n-r)*(right-l)+(l+1)*(n-r);
见下图:<br>
![](http://i4.buimg.com/572447/ba1c1d88e377c316.jpg)

## 我在找最小区间时遇到了问题，经过讲解，我明白了：
>当我们碰到某一元素的个数大于该元素总数的一半 
>1，经过该位置时，该元素并未经过n/2时，那么给点的位置为另一端点 ;
>2. 若碰到某一元素满足1，并且经过n/2时，但是两边不对称，那么此时该点为另一端点;
>3. 若满足1,2，但是这一个元素是偶数个，也就是说，中间的元素全部相同但是这个元素总共有偶数个，此时该点也为另一端点。

## 折腾了好久，终于AC了 ，代码：

```c++
#include <iostream>
#include <algorithm>
#include <vector>
#include <cstdio>
#include <cstring>
using namespace std;

typedef long long LL;
#define N 100005 
LL a[N],b[N],c[N],sum;  
  

int main()
{
	LL n;
		LL tot =0;
		cin >> n;
		for(LL i=0;i<n;i++)
		{
			cin >> a[i];
			b[a[i]]++;
			if(b[a[i]] & 1) tot ++;
			else tot--;
		}
		if(tot>1)
		{	
			cout << 0 << endl;
			return 0;
		}
		LL i;
		for(i=0;i<n/2;i++)  
    	{  
        	if(a[i] == a[n-1-i])  
         	 b[a[i]] -= 2;  
       	 else  
          	  break;  
   	    }  
   	 	if(i == n/2)  
   		{  
       		cout << n*(n+1)/2 << endl;
       		return 0;
    	}  
    	LL l=i,r=n-1-i;
    	LL left=r;
    	memset(c,0,sizeof(c));
    	for(;left >= l ;left--)
    	{
    		c[a[left]]++;
    		if(c[a[left]]*2>b[a[left]])		//出现这种情况时，会出现一下情况，顺序不能颠倒
    		{
    			if(left > ((n-1)>>1)) break; 			//此时并未经过 n/2 但是，该元素个数超过总数的一半，那么就是最小区间
    			if(a[left]!=a[n-1-left]) break;			//此时是经过了，但是出现的元素不对称，
    			if( !(b[a[left]] & 1) && left==n-1-left )  break; //此时是偶数个元素在中央
    		}
    	}
    	sum=0;
    	sum+=(l+1)*(r-left);
    	LL right=l;
    	memset(c,0,sizeof(c));
    	for(;right <= r ;right++)
    	{
    		c[a[right]]++;
    		if(c[a[right]]*2 > b[a[right]])
    		{
    			if(right < ((n-1)>>1)) break;		//同上
    			if(a[right]!=a[n-1-right]) break;
    			if( !(b[a[right]] & 1) && right==n-1-right )  break;
    		}
    	}
    	sum+=(n-r)*(right-l);
    	sum+=(l+1)*(n-r);
    	cout << sum << endl;
	return 0;
}
```

## 寄语:
>可能别说的自己并不太明白，所以重要的得自己想,尽管你会觉得好麻烦。
