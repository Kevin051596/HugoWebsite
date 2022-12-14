---
title: "C++ String Operation"
date: 2022-08-07T21:05:13+08:00
draft: false
menu:
  sidebar:
    name: C++ string operation
    identifier: other-5-C++-common-skills
    parent: other
    weight: 10
tags: ["Basic", "Multi-lingual"]
categories: ["Basic"]
---

### String
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

### 資料來源
[CSDN C++ String 的erase、remove和pop_back删除方法](https://reurl.cc/9pOXLO)  
[How Do I Add Characters to Strings in C++ The Right Way?](https://reurl.cc/NRp6Ee)  
[C++ Reference String](https://cplusplus.com/reference/string/string/erase/)