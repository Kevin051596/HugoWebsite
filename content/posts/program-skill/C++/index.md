---
title: "5 C++ Common Skills"
date: 2022-08-07T21:05:13+08:00
draft: false
menu:
  sidebar:
    name: 5 C++ Skills
    identifier: algorithm-note-5-C++-common-skills
    parent: program-skills
    weight: 10
tags: ["Basic", "Multi-lingual"]
categories: ["Basic"]
---

### 1. String
***

##### 刪除元素方式
1. [erase()](https://cplusplus.com/reference/string/string/erase/)
	- erase(iterator,刪除長度)
    - erase(刪除起點,刪除終點)( 皆是 iterator )
```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	vector<string> s1(2,"0123456789");
	s1[0].erase(5); //012346789
	s1[1].erase(5,3); //0123489
	
	for(auto el:s1) cout<<el<<"\n";

	vector<string> s2(2,"0123456789");
	s2[0].erase(s[0].begin()+2); //013456789
	s2[1].erase(s[1].begin()+2,s[1].end()); //01
	
	for(auto el:s2) cout<<el<<"\n";
	return 0;
}
```
2. [remove()](https://cplusplus.com/reference/algorithm/remove/)
    - remove 是删除和指定元素值相同的所有元素，但删除掉的元素會被其他元素代替  
    - 也就是說 remove 需要和 erase 搭配使用才能完整的删除
```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	vector<string> s(2,"0123456789");
	s[0].erase(remove(s[0].begin(),s[0].end(),'2'),s[1].end()); //013456789
	
	remove(s1.begin(),s1.end(),'0'); //1234567899
	
	for(auto el:s) cout<<el<<"\n";
	return 0;
}
```

3. other function
    - [pop_back()](https://cplusplus.com/reference/string/string/pop_back/) 刪除最後一個元素
    - [clear()](https://cplusplus.com/reference/string/string/clear/) 全部清除 
```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	vector<string> s(2,"0123456789");
	s[0].pop_back(); //012345678
	s[1].clear(); // null
	for(auto el:s) cout<<el<<"\n";
	return 0;
}
```

##### 查找元素方式
>若無法找到，則會回傳 npos(18446744073709551615)

1. [find()](https://cplusplus.com/reference/string/string/find/) & [rfind()](https://cplusplus.com/reference/string/string/rfind/)
	- find(尋找字符,從何處開始尋找)
	- rfind 只是從最後一個開始倒回來搜索，功能與 find 一樣
```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	string s1 ="abcdefghi";
	auto find1 = s1.find('a'); //0
	auto find2 = s1.find('bcd'); //3
	auto find3 = s1.rfind('a'); //0
	auto find4 = s1.rfind('bcd'); //3
	
	string s2 = "abcdaefghi";
	auto find5 = s2.find('a',2); //4
	auto find6 = s2.rfind('a',2); //0
	
	//cout ...
	return 0;
}
```
2. [find_first_of()](https://cplusplus.com/reference/string/string/find_first_of/) & [find_last_of()](https://cplusplus.com/reference/string/string/find_last_of/)
	- find_first_of 查詢第一個符合該字串的任意字符
	- find_first_of(尋找字符,從何處開始尋找)
	- find_last_of 只是從最後一個開始倒回來搜索，功能與 find_first_of 一樣
```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	string s ="abcdefghijklmnopqrstuvwxyz";
	auto find1 = s.find_first_of("hugo"); //6
	s[find1] = '*';
	auto find2 = s.find_first_of("hugo"); //7
	auto find3 = s.find_first_of("hugo",8); //14
	auto find4 = s.find_last_of("hugo"); //20

	//cout ...
	return 0;
}
```
3. [find_first_not_of()](https://cplusplus.com/reference/string/string/find_first_not_of/) & [find_last_not_of()](https://cplusplus.com/reference/string/string/find_last_not_of/)
	- find_first_not_of 查詢第一個不存在搜索字串中的字符
	- find_first_of(搜索字串,從何處開始尋找)
	- find_last_of 只是從最後一個開始倒回來搜索，功能與 find_first_not_of 一樣
```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	string s ="abcdef";
	size_t find = s.find_first_not_of("abcdgh"); //4
	auto find2 = s.find_last_not_of("abcdgh"); //5

	return 0;
}
```
> auto 為 find 變數自動賦予的就是 size_t 

##### 加入元素方式

1. [+= operator](https://cplusplus.com/reference/string/string/operator+=/)  
```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	string s ="Hello ";
	s += "Hugo!";
	cout<<s; //Hello Hugo!
	return 0;
}
```
2. [push_back()](https://cplusplus.com/reference/string/string/push_back/)
	- 只能接受 char 型態的資料 
```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	string s ="Hello ";
	s.push_back('H');
	cout<<s; //Hello H
	return 0;
}
``` 
3. [insert()](https://cplusplus.com/reference/string/string/insert/)
	- insert(iterator, char);
	- 只能接受 char 型態的資料 
```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	string s ="Hello ";
	s.insert(s.begin(),'H'); 
	s.insert(s.begin()+3,'H');
	cout<<s; //HHeHllo
	return 0;
}
```
4. [append()](https://cplusplus.com/reference/string/string/append/)
```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	string s ="Hello ";
	s.append("Hugo!");
	cout<<s; //Hello Hugo!
	return 0;
}
``` 

##### 替換元素方式

1. [substr()](https://cplusplus.com/reference/string/string/substr/)
	- substr(起始位置, 複製字符長度); 
```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	string s ="Hello";
	string s1 = s.substr(0,2); //He
	string s2 = s.substr(2,3); //llo

	cout<<s1<<"\n"<<s2;
	return 0;
}
```
2. [replace()](https://cplusplus.com/reference/string/string/replace/)
	- replace(被替換起點,被替換長度,替換字串)
```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	string s1 ="Hello";
	string s2 ="Hugo";
	s1.replace(2,1,s2); //HeHugolo;
	
	string s3 ="Hello";
	string s4 ="Hugo";
	s3.replace(2,1,s4.substr(0,2)); //HeHulo;

	cout<<s1<<"\n"<<s3;
	return 0;
}
```
3. [swap()](https://cplusplus.com/reference/string/string/swap/)
	- swap(交換字串);
```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	string s1 ="Hello";
	string s2 ="Hugo";
	s1.swap(s2); //Hugo
	
	string s3 ="Hello";
	string s4 ="Hugo";
	string s5 = s4.substr(0,2);
	s3.swap(s5); //Hu
	
	cout<<s1<<"\n"<<s3;
	return 0;
}
```
##### 題型紀錄
[1703 Double String /0808](https://codeforces.com/problemset/problem/1703/D)

### 2. Vector
***
##### 增加元素方式
> 版本提醒：emplace_back()、emplace() 皆於 C++ 11 加入

1. [push_back()](https://cplusplus.com/reference/vector/vector/push_back/) & [emplace_back()](https://cplusplus.com/reference/vector/vector/emplace_back/)
	- emplace_back() 與 push_back() 差異
		- push_back() 過程: 創建、拷貝至容器
		- emplace_back() 過程: 直接於容器創建
	- 結論: 使用 emplace_back() 效率較高，但若顧慮版本，使用 push_back() 更安全
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	vector<int> v;
	
	v.push_back(1);
	v.emplace_back(2);
	
	for(int i:v) cout<<i<<" ";
	cout<<"\n"; //1 2
	return 0;
}
```
2. [insert()](https://cplusplus.com/reference/vector/vector/insert/) & [emplace()](https://cplusplus.com/reference/vector/vector/emplace/)
	- insert() 與 emplace() 差異
		- insert() 可以插入多個元素
		- emplace() 只能插入一個元素 
		- insert() 過程: 創建、拷貝至容器
		- emplace() 過程: 直接於容器創建
	- 結論: 使用 emplace() 效率較高，但若顧慮版本，或者需要插入多個元素，則使用 insert() 更好
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	vector<int> v1(3,9);
	vector<int> v2 = {0,1,2,3,4,5};
	
	v1.insert(v1.begin()+1,v2.begin(),v2.end());
	for(int i:v1) cout<<i<<" ";
	cout<<"\n"; //9 0 1 2 3 4 5 9 9
	
	v1.emplace(v1.begin()+1, 100);
	for(int i:v1) cout<<i<<" ";
	cout<<"\n"; //9 100 0 1 2 3 4 5 9 9
	
	return 0;
}
```
3. [at()](https://cplusplus.com/reference/vector/vector/at/)
	- at(取代位置)
> 不可超過 vector 容器當前長度

```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	vector<int> v(5,9);
	v.at(2) = 100;
	for(int i:v) cout<<i<<" "; //9 9 100 9 9
	return 0;
}
```

##### 刪除元素方式

1. [pop_back()](https://cplusplus.com/reference/vector/vector/pop_back/)
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	vector<int> v = {0,1,2};
	v.pop_back();
	for(int i:v) cout<<i<<" "; //0 1
	return 0;
}
```
2. [erase()](https://cplusplus.com/reference/vector/vector/erase/)
	- erase(iterator)
	- erase(刪除起點, 刪除終點)( 皆是 iterator ) 
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	vector<int> v1 = {0,1,2,3,4,5,6,7,8,9};
	v1.erase(v1.begin()+5);
	for(int i:v1) cout<<i<<" "; //0 1 2 3 4 6 7 8 9
	cout<<"\n"; 
	
	vector<int> v2 = {0,1,2,3,4,5,6,7,8,9};
	v2.erase(v2.begin(),v2.begin()+2); 
	for(int i:v2) cout<<i<<" "; //2 3 4 5 6 7 8 9
	
	return 0;
}
```
3. [clear()](https://cplusplus.com/reference/vector/vector/clear/)
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	vector<int> v1 = {0,1,2,3,4,5,6,7,8,9};
	v1.clear();
	
	for(int i:v1) cout<<i<<" "; //null
	return 0;
}
```

### 3. Map
***
>map 容器基本型態(key, value)

##### 增加元素方式

1. [operator](https://cplusplus.com/reference/map/map/operator=/)
	- 可以透過 `＝`、`+` 為 map 容器增加元素
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	map<char,int> mp;
	vector<char> v = {'a','e','i','o','u'};
	
	for(int i=0;i<v.size();i++) mp[v[i]] = i;
	mp['e'] = 100;
	
	for(int i=0;i<mp.size();i++) cout<<mp[v[i]]<<" "; //0 100 2 3 4
	return 0;
}
```
2. [at()](https://cplusplus.com/reference/map/map/at/)
	- 直接於指定 map 鍵位更換元素 
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	map<string,int> mp = {{"abc",0},{"ccc",11},{"xyz",135}};
	mp.at("abc") = 100;
	
	for(auto x:mp) cout<<x.first<<" "<<x.second<<"\n";
	// abc 0
	// ccc 100
	// xyz 135
	return 0;
}
```

##### 刪除元素方式

1. [erase()](https://cplusplus.com/reference/map/map/erase/)
	- erase(key)
	- erase(iterator)
	- erase(刪除起點, 刪除終點)( 皆是 iterator ) 
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	map<string,int> mp = {{"abc",123},{"ccc",456},{"xyz",789},{"hgj",0}};
	mp.erase("abc"); //刪除"abc"
	mp.erase(mp.begin()); //刪除"ccc"
	
	for(auto x:mp) cout<<x.first<<" "<<x.second<<"\n";
	//hgj 0
	//xyz 789
	return 0;
}
```
> map 會根據 `key` 自動排列

2. [clear()](https://cplusplus.com/reference/map/map/clear/)
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	map<string,int> mp = {{"abc",123},{"ccc",456},{"xyz",789},{"hgj",0}};
	mp.clear();
	
	for(auto x:mp) cout<<x.first<<" "<<x.second<<"\n";//null
	return 0;
}
```

##### 查找元素方式

1. [find()](https://cplusplus.com/reference/map/map/find/)
	- find(key) 此為 `iterator` 型態 
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	map<string,int> mp = {{"abc",123},{"ccc",456},{"xyz",789},{"hgj",0}};
	auto it = mp.find("ccc");
	
	cout<<it->first<<" "<<it->second; //ccc 456
	return 0;
}
```
2. [lower_bound()](https://cplusplus.com/reference/map/map/lower_bound/) & [upper_bound()](https://cplusplus.com/reference/map/map/upper_bound/)
	- lower_bound(key)，尋找此 `key` 以下的第一個元素
	- upper_bound(key)，尋找此 `key` 之上的第一個元素
	- 皆為 `iterator` 型態
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	map<string,int> mp = {{"abc",123},{"ccc",456},{"xyw",789},{"xyy",455}};
	auto it1 = mp.lower_bound("ccc");
	auto it2 = mp.upper_bound("ccc");
	
	cout<<it1->first<<" "<<it1->second<<"\n"; //ccc 456
	cout<<it2->first<<" "<<it2->second; //xyw 789
	return 0;
}
```

### 4. Queue & Stack
***
##### 基本元素操作
- [push()](https://cplusplus.com/reference/queue/queue/push/) & [pop()](https://cplusplus.com/reference/queue/queue/pop/)
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	vector<int> v = {0,1,2,3,4,5,6,7,8,9};
	queue<int> q;
	for(int i:v) q.push(i);
	do{
		cout<<q.front()<<" ";
		q.pop();
	}while(!q.empty()); //0 1 2 3 4 5 6 7 8 9
	return 0;
}
```
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	vector<int> v = {0,1,2,3,4,5,6,7,8,9};
	stack<int> s;
	for(int i:v) s.push(i);
	do{
		cout<<s.top()<<" ";
		s.pop();
	}while(!s.empty()); //9 8 7 6 5 4 3 2 1 0
	return 0;
}
```

##### 其他操作

1. [swap()](https://cplusplus.com/reference/queue/queue/swap/)
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	queue<int> q1, q2;
	for(int i=0;i<10;i++) q1.push(i);
	for(int i=9;i>=0;i--) q2.push(i);
	q1.swap(q2);
	
	while(!q1.empty()){
		printf("%d ",q1.front());
		q1.pop();
	} //9 8 7 6 5 4 3 2 1 0
	return 0;
}
```
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	stack<int> s1, s2;
	for(int i=0;i<10;i++) s1.push(i);
	for(int i=9;i>=0;i--) s2.push(i);
	s1.swap(s2);
	
	while(!s1.empty()){
		printf("%d ",s1.top());
		s1.pop();
	} //0 1 2 3 4 5 6 7 8 9
	return 0;
}
```
2. [emplace()](https://cplusplus.com/reference/queue/queue/emplace/)
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	queue<string> q;
	stack<string> s;
	
	q.emplace("Hello Hugo!");
	q.emplace("2022");
	s.emplace("Hello Hugo!");
	s.emplace("2022");
	
	while(!q.empty() && !s.empty()){
		cout<<q.front()<<" | "<<s.top()<<"\n";
		q.pop();
		s.pop();
	}
	// Hello Hugo! | 2022
	// 2022 | Hello Hugo!
	
	return 0;
}
```

### 5. Others
***
1. [boolalpha](https://cplusplus.com/reference/ios/boolalpha/)
	- boolalpha 可以將 `bool` 轉化為 `true`、`false`
	- noboolalpha 則與此相反
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	bool a = 0;
	bool b = 1;
	cout<< boolalpha <<a<<" "<<b<<"\n"; //false true
	cout<< noboolalpha <<a<<" "<<b; //0 1
	return 0;
}
```

### 資料來源
[CSDN C++ String 的erase、remove和pop_back删除方法](https://reurl.cc/9pOXLO)  
[How Do I Add Characters to Strings in C++ The Right Way?](https://reurl.cc/NRp6Ee)  
[C++ Reference String](https://cplusplus.com/reference/string/string/erase/)  