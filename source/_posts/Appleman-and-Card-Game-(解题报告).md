title: Appleman and Card Game - acm
date: 2016-08-18 08:57:06
categories: [题解]
tags:
- ACM题解
---
<blockquote class="blockquote-center"><h1>codeforces 462B(我的解题过程)</h1></blockquote>
![](http://i4.buimg.com/572447/3ef50cf11ff6e632.jpg)
## 1.题目： Appleman and Card Game
>** Appleman and Card Game**&nbsp;&nbsp;["传送门"](http://acm.hust.edu.cn/vjudge/problem/52962 "传送门")<br>
<hr>
<!--more-->
 <p><b>##Description</b></p>
    ```
      Appleman has n cards. Each card has an uppercase letter written on it. Toastman must choose k cards from Appleman's cards. 
    Then Appleman should give Toastman some coins depending on the chosen cards. Formally, for each Toastman's card i you should calculate how much Toastman's cards
    have the letter equal to letter on ith, then sum up all these quantities, such a number of coins Appleman should give to Toastman.
    Given the description of Appleman's cards. What is the maximum number of coins Toastman can get?
    ```
</hr>

<hr>
 <p><b>##INPUT</b></p>
    ```
      The first line contains two integers n and k (1 ≤ k ≤ n ≤ 105). The next line contains n uppercase letters without spaces
    — the i-th letter describes the i-th card of the Appleman.
    ```
</hr>

<hr>
 <p><b>##OUTPUT</b></p> 
    ```
    Print a single integer – the answer to the problem.
    ```
</hr>

<hr>
 <p><b>##SAMPLE INPUT</b></p>
<ul>
    ## INOUT</br>
    ```
    15 10
    DZFDFZDFDDDDDDF
    ```
    <br/>
    ## OUTPUT <br/>
    ```
    82
    ```
    <br/>
     ## INOUT</br>
    ```
    6 4
    YJSNPI
    ```
    <br/>
    ## OUTPUT <br/>
    ```
    4
    ```
</ul>
</hr>

## 2.题目理解：
>对于这道题，其实非常简单，无技巧可言<br/>
>这道题用来锻炼编程能力</br>
>说实话我写的并不咋的

## 3.题目代码:
```c++
#include <stdio.h>
#include <iostream>
#include <string.h>
#include <algorithm>
using namespace std;

typedef long long ll;


int main(){
    ll n,k,i=0,j=0;
	char str[100000+10];
while(~scanf("%lld%lld%s",&n,&k,&str))
	{	
		i=0,j=0;
		ll amount[26]={0};
		
		fflush(stdin);
		for(i=0;i<n;i++){
			amount[str[i] - 'A']++;
		}	
		
		
		sort(amount,amount+26);
		

		ll sum=0,x=0;
		for(i=25;i>=0;i--)
		{
			x = min( k , amount[i] );
			k -= x;
			sum += x*x;
		}
		printf("%lld\n",sum);
}
	return 0;
}
```
## 做题不要慌张！！！
