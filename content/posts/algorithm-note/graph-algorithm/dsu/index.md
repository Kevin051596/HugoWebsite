---
title: "Graph Dsu"
date: 2022-08-08T22:56:21+08:00
draft: true
menu:
  sidebar:
    name: graph dsu
    identifier: algorithm-note-graph-algorithm-dsu
    parent: algorithm-note-graph-algorithm
    weight: 12
tags: ["Basic", "Multi-lingual"]
categories: ["Basic"]
---

### Disjoint Set
***
### 練習題
***
[1702 Split Into Two Set](https://codeforces.com/problemset/problem/1702/E)
```C++
#include <bits/stdc++.h>
using namespace std;

int find(vector<int>& v, int x){
	if(x == v[x]) return x;
	else return find(v, v[x]);
}

bool solve(vector<pair<int, int>>& grid){
	int n = grid.size();
	vector<int> v(n+1,0);
	vector<int> result(n+1,0);
	for(int i=1;i<=n;i++) v[i] = i;
	for(int i=0;i<n;i++){
		if(grid[i].first == grid[i].second) return false;
		result[grid[i].first]++;
		result[grid[i].second]++;
		int a = find(v, grid[i].first);
		int b = find(v, grid[i].second);
		if(a!=b) v[b] = a;
	}
	for(int i=1;i<=n;i++) result[find(v, i)]++;	
	for(int i=1;i<=n;i++) if(result[i]!=0 && result[i]&1) return false;
	return true;
}

int main(){
	int t;
	cin>>t;
	while(t--){
		int n;
		cin>>n;
		vector<pair<int,int>> dom;
		for(int i=0;i<n;i++){
			int a,b;
			cin>>a>>b;
			dom.push_back({a,b});
		}
		if(solve(dom)) cout<<"YES"<<"\n";
		else cout<<"No"<<"\n";
	}
	return 0;
}
```