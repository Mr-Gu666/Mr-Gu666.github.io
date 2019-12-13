---
layout: post
title: "Algorithm"
tags: [acm, algorithm, kmp]
---

<h1 name="catalogue">Algorithm</h1>
<h2>-字符串</h2>

<ul><a href="#kmp">-KMP</a></ul>

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