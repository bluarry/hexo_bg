---
title: Borya and Hanabi-codeforces
date: 2016-08-20 08:05:10
categories: [ACM题解]
tags: 
- 算法
- 题解
---

<blockquote class="blockquote-center"><h1>Borya and Hanabi-codeforces 442A</h1></blockquote>
![](http://i4.buimg.com/572447/93e486a1e8366a04.jpg)<br>
被这道题坑了，其实就是状态压缩
<!--more-->
>**Borya and Hanabi-codeforces 442A**&nbsp;&nbsp;["传送门"](http://codeforces.com/problemset/problem/442/A "传送门")<br>

## Description:
>Have you ever played Hanabi? If not, then you've got to try it out! This problem deals with a simplified version of the game.

>Overall, the game has 25 types of cards (5 distinct colors and 5 distinct values). Borya is holding n cards. The game is somewhat complicated by the fact that everybody sees Borya's cards except for Borya himself. Borya knows which cards he has but he knows nothing about the order they lie in. Note that Borya can have multiple identical cards (and for each of the 25 types of cards he knows exactly how many cards of this type he has).

>The aim of the other players is to achieve the state when Borya knows the color and number value of each of his cards. For that, other players can give him hints. The hints can be of two types: color hints and value hints.

>A color hint goes like that: a player names some color and points at all the cards of this color.

>Similarly goes the value hint. A player names some value and points at all the cards that contain the value.

>Determine what minimum number of hints the other players should make for Borya to be certain about each card's color and value.

## Input
>The first line contains integer n (1 ≤ n ≤ 100) — the number of Borya's cards. The next line contains the descriptions of n cards. The description of each card consists of exactly two characters. The first character shows the color (overall this position can contain five distinct letters — R, G, B, Y, W). The second character shows the card's value (a digit from 1 to 5). Borya doesn't know exact order of the cards they lie in.

## Output
>Print a single integer — the minimum number of hints that the other players should make.

## Example
><b>input</b> <br>
2<br>
G3 G3<br>
<b>output</b><br>
0<br>
><b>input</b> <br>
4 <br>
G4 R4 R3 B3 <br>
<b>output</b><br>
2 <br>
><b>input</b> <br>
5<br>
B1 Y1 W1 G1 R1<br>
<b>output</b><br>
4<br>

## Note
>In the first sample Borya already knows for each card that it is a green three.

>In the second sample we can show all fours and all red cards.

>In the third sample you need to make hints about any four colors.

## 题目分析
>原文意思大概是：总共有5种颜色，5种花色的牌，总共是25张牌，现在输入一个整数n，再输入n个牌的信息，<br>
然后有人知道所有牌的信息并且可以告诉你牌的信息，问你最少问这个人几次就能知道所有牌的花色及数字<br>
>这道题首先想到的是暴力枚举，事实上就是暴力枚举，我们枚举每一次问的是什么，算出当前所问次数即可<br>
那么怎么枚举，又如何判断是否可行呢？？其实我们可以用过状态压缩，用二进制的前5位代表花色，后5位代表数字<br>
那么，当询问的状态中出现以下情况则不行：<br>
&nbsp;&nbsp; 1.某种牌的花色被询问2次及两次以上，而并未询问数字，那么就不行。(询问1次可以根据其他情况推理出来)
&nbsp;&nbsp; 2.某种牌的数字被询问2次及两次以上，而并未询问花色，那么就不行.(同上)
&nbsp;&nbsp; 3.牌2次及以上未询问，也不行.

## 代码如下:
```c++
#include <iostream>
#include <stdio.h>
#include <string.h>
#include <algorithm>
using namespace std;
int map[15][15];
char ch[]={'0','R','G','Y','W','B'};

int cout_x(int x)
{
	if(0==x) return 0;
	return (cout_x(x>>1)+(x&1));
}

bool judge(int x){
	int ta=0,sum[15]={0};
	for(int i=1;i<=5;i++)
		for(int j=6;j<=10;j++)
			if(map[i][j]){
				 //统计当前问了某一花色，没问数字的次数
				if(((1<<(i-1))&x) && (!((1<<(j-1))&x)) ) 	sum[i]++;
				//统计当前询问了某一数字，没问花色的次数
				if( ((1<<(j-1))&x) && (!((1<<(i-1))&x)) )		sum[j]++;
				//统计某一张牌既没问花色，也没问数字的次数
				if((!(1<<(j-1))&x) && (!(1<<(i-1))&x))		ta++;
			}
			//判断上边出现的次数有没有超过1次，超过就不行，否则可以
			if(ta>1) return false;
			for(int i=1;i<=10;i++)
				if(sum[i]>1) return false;
			return true;
}

int main()
{
//	freopen("D:\\in.txt","r",stdin);
	int n;
	char s[3];
	while(cin >> n)
	{
		memset(map,0,sizeof(map));
		for(int i=0;i<n;i++)
		{
			cin >> s;
			int a=0;
			for(int j=1;j<=5;i++)
			{
				if(s[0]==ch[i]){a=i;break;}
			}
			int b=s[1]-'0'+5;
			map[a][b]=1;
		}
		int ans=123456;
		for(int i=0;i<(1<<10);i++)
		{

			if(judge(i))
			{
				ans=min(ans,cout_x(i));
			}
		}
		cout << ans << endl;
	}
	return 0;
}
```

## 寄语
>其实重在思路，谁都有看题解的时候，不必气馁，相信努力终会有结果。
