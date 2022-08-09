---
title: "Greedy"
date: 2022-08-06T22:08:48+08:00
menu:
  sidebar:
    name: greedy algorithm
    identifier: algorithm-note-greedy
    parent: algorithm-note
    weight: 10
tags: ["Basic", "Multi-lingual"]
categories: ["Basic"]
---

Greedy algorithm 譯為貪心演算法，或稱貪婪法。  
主要將一個問題分成好幾個部分，並從中採用最優選擇，試圖將所有的最優選擇堆疊成為最優解。

- 優點：簡單、高效，通常作為其它演算法的輔助演算法來使用。
- 缺點：忽略總體上可能情況，使得不少情況下容易無法得出最優解。
***

### 相關問題類型
***

#### Codeforces 練習題目
[1714C Minimum Varied Number /0807](https://codeforces.com/problemset/problem/1714/C)
```C++
#include <bits/stdc++.h>
using namespace std;
 
 
int main(){
	int t;
	cin>>t;
	while(t--){
		int s;
		cin>>s;
		string ans = "";
		for(int i=9;i>0;i--){
			if(s == 0) break;
			else if(s>=i){
				s-=i;
				ans += i+'0';
			}
		}
		reverse(ans.begin(),ans.end());
		cout<< ans <<"\n";
	}
	return 0;
}
```
***

#### 最短路徑問題
***
#### 最小生成樹問題
***
#### 霍夫曼編碼問題
***

#### K 中心問題
***

### 資料來源
[Greedy Algorithms Explained with Examples](https://www.freecodecamp.org/news/what-is-a-greedy-algorithm/)