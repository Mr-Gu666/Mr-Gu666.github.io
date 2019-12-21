---
layout: post
title: "Algorithm"
tags: [acm, algorithm]
---

<h1><a name="catalogue">Algorithm</a></h1>
<ul>
	<h2>-字符串</h2>
		<ul><a href="#kmp">-KMP</a></ul>
	<h2>-动态规划</h2>
    <ul><a href="#ZeroOnePack">-01背包</a></ul>
    <ul><a href="#CompletePack">-完全背包</a></ul>
</ul>

<h3><a name="kmp">KMP</a></h3>
```c++
const int N = 1e6+2;
int next[N];
//存储的是自身下标
//abdabce 0001200
char S[N],T[N];
int slen,tlen;

//获得next数组
void getNext(){
	int j,k;
	j = 0,k = -1;
	next[0] = -1;
	while(j<tlen){
		//若k刚开始 或 T串k位置和j位置的字符相等
		if(k==-1||T[j]==T[k]){	
			next[++j]=++k;
		}else{
			k = next[k];
		}
	}
}

//返回T第一次完全匹配的位置
int KMP_Index(){
	int i = 0,j = 0;
	getNext();
	while(i<slen && j<tlen){
		if(j==-1 || S[i]==T[j]){
			i++;
			j++;
		}else{
			j = next[j];
		}
	}
	if(j==tlen){
		return i-tlen;
	}else{
		return -1;
	}
}

//返回T在S中匹配了多少次
int KMP_Count(){
	int ans = 0,i = 0,j = 0;
	if(slen==1 && tlen==1){
		if(S[0]==T[0])
			return 1;
		else
			return 0;
	}
	getNext();
	for(int i=0;i<slen;i++){
	while(j>0 && S[i]!=T[j]){
			j = next[j];
		}
		if(S[i]==T[j]){
			j++;
		}
		if(j==tlen){
			ans++;
			j = next[j];
		}
	}
	return ans;
}
```

<p style="text-align: right"><a href="#catalogue"><-back</a></p>
<h3><a name="ZeroOnePack">01背包</a></h3>
```c++
//背包最大容积
const int M = 2e5+5;
//物品最多种类
const int N = 1e5+5;
//n个物体，背包m大小，c[]物体重量，w[]物体价值
int dp[M],c[N],w[N],n,m;
void ZeroOnePack(int cc,int ww){
	for(int i=m;i>=cc;i--){
		dp[i] = max(dp[i],dp[i-cc]+ww);
	}
}

```

<p style="text-align:right"><a href="#catalogue"><-back</a></p>
<h3><a name="CompletePack">完全背包</a></h3>
```c++
//背包最大容量
const int M = 10005;
//物品种类
const int N = 10005;
int m,n,dp[M],c[N],w[N];
void CompletePack(int cc,int ww){
    for(int i=cc;i<=m;i++){
        dp[i]=max(dp[i],dp[i-cc]+ww);
    }
}

```

<p style="text-align:right"><a href="#catalogue"><-back</a></p>