---
title: "5 C++ STL Containers"
date: 2022-08-07T21:05:13+08:00
draft: false
menu:
  sidebar:
    name: C++ 5 STL containers
    identifier: other-C++-container
    parent: other
    weight: 10
tags: ["Basic", "Multi-lingual"]
categories: ["Basic"]
---

以下為作者在練 C++ 時，較常使用到的容器以及其函數，整理成這份文章幫助作者我統整大腦中這部分的資料。
其他如 Deque, List, Array 等詳細使用，可至網路上搜尋或於 C++ Reference 閱讀，皆有相關豐富資料，給各位作參考。

### STL Container 前言
***
- 主要分類為三大塊，`容器配接器(Adaptor)`、`順序容器(Sequence)`、`關聯容器(Associative)`
- 關聯容器又可細分 `multi`、`unorder`。

![Container](https://miro.medium.com/max/1400/1*KeKGfCHNpEExsyQ6XPq2tg.png)
### 1. Vector
***
##### 何謂 Vector Container ?
- `Vector` 為一種自動可變容量的陣列
- 於尾端操作資料較快
- 可儲存任何變數，如 `int`、`string`、`自訂 vector`
- 優點：可以**快速儲存多個數值**（隨機存取），佔用空間小
- 缺點：搜索特定元素效率慢，於中間操作元素效率差

##### 更改元素方式
> 版本提醒：emplace_back()、emplace() 皆於 C++ 11 加入

1. 於陣列最後項新增：[push_back()](https://cplusplus.com/reference/vector/vector/push_back/) & [emplace_back()](https://cplusplus.com/reference/vector/vector/emplace_back/) 
> emplace_back() 與 push_back() 差異
> - push_back() 過程： 創建、拷貝至容器  
emplace_back() 過程： 直接於容器創建

{{< alert type="info" >}} 結論: 使用 `emplace_back()` 效率較高，但若顧慮版本，使用 `push_back()` 更安全 {{< /alert >}}
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

2. 新增元素插入：[insert()](https://cplusplus.com/reference/vector/vector/insert/) & [emplace()](https://cplusplus.com/reference/vector/vector/emplace/)
> insert() 與 emplace() 差異
> 1. insert() 可以插入多個元素；emplace() 只能插入一個元素 
> 2. insert() 過程： 創建、拷貝至容器  
>	 emplace() 過程： 直接於容器創建  

{{< alert type="info" >}} 結論： 使用 `emplace()` 效率較高，但若顧慮版本，或者需要插入多個元素，則使用 `insert()` 更好 {{< /alert >}}

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
3. 刪除某元素：[erase()](https://cplusplus.com/reference/vector/vector/erase/)
	- 方法一：erase(iterator)
	- 方法二：erase(iterator first, iterator last)
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	vector<int> v1 = {0,1,2,3,4,5,6,7,8,9};

	//方法一
	v1.erase(v1.begin()+5);
	for(int i:v1) cout<<i<<" "; //0 1 2 3 4 6 7 8 9
	cout<<"\n"; 
	
	//方法二
	vector<int> v2 = {0,1,2,3,4,5,6,7,8,9};
	v2.erase(v2.begin(),v2.begin()+2); 
	for(int i:v2) cout<<i<<" "; //2 3 4 5 6 7 8 9
	
	return 0;
}
```
4. 於陣列最後項刪除該元素：[pop_back()](https://cplusplus.com/reference/vector/vector/pop_back/)
	- 不需任何參數
	- 如同字面意思，功用為排出最後一個元素(無法一次排出多個元素)

### Map 與 Set 前言
***
- 容器種類：`Map` 與 `Set` 屬於關聯容器，為**自動排序**的容器
- 內部實現：紅黑樹
- 時間複雜度：O(log n)
- 相關翻譯：字典(Map)、集合(Set)
> 關聯容器補充：通常其儲存的元素結構為一對鍵值對 `(pair<type,type>)` , 前者稱為 `key`, 作為排序的參考；後者為 `val`, 為該元素主要儲存值

- `Map` 特性：`key`、`val` 不可相同且元素不可重複，透過調用 `key` 來獲得所需 `val`
- `Set` 特性： 主要儲存 `val` 來當作其 `key`，兼具 `key`、`val` 的功能，且元素不可重複
- `Map` 使用時機：需要有序訪問，且`val`須**經常更新**時
- `Set` 使用時機：需要有序訪問，且須**頻繁搜索**特定數值時
- 優點：元素能自動排序
- 缺點：創建時效率較慢

> `multi`：為一種關聯容器樣式，用於存取多個同樣 `key`、`val` 的資料，如 `multimap`、`multiset`  
`unorder`： 為一種關聯容器樣式，其排序規則依照其特定 `hash function` 而定

### 2. Map
***
> map 容器基本型態：`map<key type, val type>`

##### 更改元素方式

1. 操作符：[operator](https://cplusplus.com/reference/map/map/operator=/)
	- 可以透過 `＝`、`[]` 為 map 容器增加元素
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

2. 新增元素插入：[insert](https://cplusplus.com/reference/map/map/insert/)
	- 方法一：insert(pair<key,val>)
	- 方法二：insert(iterator position, pair<key,val>)
	- 方法三：insert(iterator first, iterator last)
```C++
#include <bits/stdc++.h>
#define ll long long
using namespace std;

int main(){
	map<string, int> mp = {{"abc",1},{"def",23}};
	map<string, int> mp2 = {{"ccc",1},{"kk",3},{"wsxy",77}};
	
	mp.insert({"hoo",45});//方法一
	mp.insert(mp.begin(),{"aa",111});//方法二
	mp.insert(mp2.begin(), mp2.find("kk"));//方法三
	
	for(auto el:mp) cout<<el.first<<" "<<el.second<<"\n";
	// aa 111
	// abc 1
	// ccc 1
	// def 23
	// hoo 45
	return 0;
}
```

3. 刪除某元素：[erase()](https://cplusplus.com/reference/map/map/erase/)
	- 方法一：erase(key)
	- 方法二：erase(iterator position)
	- 方法三：erase(iterator first, iterator last)
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	map<string,int> mp = {{"abc",123},{"ccc",456},{"xyz",789},{"hgj",0}};
	mp.erase("abc"); //方法一
	mp.erase(mp.begin()); //刪除"ccc" 方法二
	
	for(auto x:mp) cout<<x.first<<" "<<x.second<<"\n";
	//hgj 0
	//xyz 789
	return 0;
}
```
> map 會根據 `key` 自動排列

##### 查找元素方式

1. 查找某元素位置：[find()](https://cplusplus.com/reference/map/map/find/)
	- find(key)
	- 回傳 `iterator` 型態, 若沒有找到, 則回傳 `map::end()`
	{{< vs 1>}}
2. 計算某元素數量：[count()](https://cplusplus.com/reference/map/map/count/)
	- cout(key)
	- 通常回傳 1 或 0，因為 `key` 值不可重複
	{{< vs 1>}}
3. 查找某元素的下限／上限：[lower_bound()](https://cplusplus.com/reference/map/map/lower_bound/) & [upper_bound()](https://cplusplus.com/reference/map/map/upper_bound/)
	- lower_bound(key)，尋找此 `key` 以下的第一個元素
	- upper_bound(key)，尋找此 `key` 之上的第一個元素
	- 皆回傳 `iterator` 型態
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


### 3. Set
***
> set 容器基本型態：`set<val type>`  

##### 更改元素方式
1. 操作符：[operator](https://cplusplus.com/reference/set/set/operator=/)
	- 透過 `=` 方式增加元素
```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	vector<int> v = {0, 1, 2, 3, 4, 5, 6, 7};
	set<int> set1(v.begin(),v.end()); // 括弧內為增加指定容器特定範圍內的元素。
	set<int> set2(v.begin()+2,v.begin()+4);
	
	set1 = set2; //可以透過 = 更新容器內容
	// set1[2] = 3; 由於 set 沒有提供 [] 類型的 operation，因此會無法成功編譯
	for(auto el:set1) cout<<el<<" "; //2 3
	return 0;
}
``` 

2. 新增某元素插入：[insert()](https://cplusplus.com/reference/set/set/insert/)
	- 方法一：insert(val)
	- 方法二：insert(iterator position, val)
	- 方法三：insert(iterator first, iterator last)

```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	
	//使用方法一
	set<int> set_1;
	for(int i=1;i<=5;i++) set_1.insert(i*10);
	for(auto el:set_1) cout<<el<<" "; //10 20 30 40 50
	cout<<"\n";

	//使用方法二
	set_1.insert(set_1.begin(),5); 
	set_1.insert(set_1.begin(),100); //於開頭插入，但 set 會自動排序，因此移動至最後
	for(auto el:set_1) cout<<el<<" "; //5 10 20 30 40 50 100
	cout<<"\n";
	
	//使用方法三
	set<int> set_2;
	set_2.insert(set_1.begin(),set_1.end());
	for(auto el:set_2) cout<<el<<" "; //5 10 20 30 40 50 100
	
	return 0;
}
```

3. 刪除某元素：[erase()](https://cplusplus.com/reference/set/set/erase/)  
	- 方法一：erase(iterator position)
	- 方法二：erase(val)
	- 方法三：erase(iterator first, iterator last)

```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	
	set<int> set_1;
	for(int i=1;i<=5;i++) set_1.insert(i*10);
	
	//方法一
	set_1.erase(set_1.begin());
	for(int el:set_1) cout<<el<<" "; //20 30 40 50
	cout<<"\n";
	
	//方法二
	set_1.erase(40);
	for(int el:set_1) cout<<el<<" ";//20 30 50
	cout<<"\n";
	
	//方法三
	auto it = set_1.begin(); //iterator it 指向 20
	it++; // 指向 30
	set_1.erase(it, set_1.end());
	for(int el:set_1) cout<<el<<" ";//20
	cout<<"\n";
	
	return 0;
}
```

##### 查找元素方式
1. 計算某元素的數量：[cout()](https://cplusplus.com/reference/set/set/count/)
	- cout(val)
	- 通常回傳 1 或 0，因為 `val` 值不可重複
	{{< vs 1>}}
2. 查找某元素位置：[find()](https://cplusplus.com/reference/set/set/find/)
	- find(val)
	- 回傳 `iterator`, 若沒有找到則回傳 `set::end()`  
	{{< vs 1>}}
3. 查找某元素的下限／上限：[lower_bound()](https://cplusplus.com/reference/set/set/lower_bound/) & [upper_bound()](https://cplusplus.com/reference/set/set/upper_bound/)
	- lower_bound(val)
	- upper_bound(val) 
	- 皆回傳 `iterator` 型態
```C++
#include <bits/stdc++.h>
using namespace std;
int main(){
	
	set<int> set_1;
	for(int i=1;i<=5;i++) set_1.insert(i*10);
	
	auto it1 = set_1.lower_bound(20);//回傳 20 以下的第一個 iterator
	auto it2 = set_1.upper_bound(40);//回傳大於 40 的第一個 iterator
	cout<<*it1<<" "<<*it2;//20 50
	
	return 0;
}
```

### Unordered 無序容器 前言
***
- 容器種類：`Unordered` 開頭的容器屬於關聯性容器，但其內部為**無序**，即不會自動排列
- 內部實現：`HashTable`
- 時間複雜度：O(1)
- 優點：搜索特定元素時效率快
- 缺點：創建時效率慢，佔用空間大

### 4. Unordered_Map
***
##### 更改元素方式
1. 新增某元素插入：[insert()](https://cplusplus.com/reference/unordered_map/unordered_map/insert/)
	- 方法一：insert(pair<key,val>)
	- 方法二：insert(iterator first, iterator last)
	- 方法三：insert(list)
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	unordered_map<string, int> um = {{"ab",1},{"cc",2}};
	unordered_map<string, int> um2 = {{"le",1},{"kl",2}};
	
	um.insert({"sdf",100});//方法一
	um.insert (um2.begin(),um2.end());//方法二
	um.insert({{"ks",15},{"zz",33}});//方法三
	
	for(auto el:um) cout<<el.first<<" "<<el.second<<"\n";
	//zz 33
	//ks 15
	//sdf 100
	//kl 2
	//le 1
	//cc 2
	//ab 1
	return 0;
}
```
2. 刪除某元素：[erase()](https://cplusplus.com/reference/unordered_map/unordered_map/erase/)
	- 方法一：erase(key)
	- 方法二：erase(iterator position)
	- 方法三：erase(iterator first, iterator last)

```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	unordered_map<string, int> um = {{"ab",1},{"cc",2},{"sdf",100},{"ks",15},{"zz",33}};
	
	um.erase("ab");//方法一
	um.erase(um.begin());//方法二
	um.erase(um.find("sdf"),um.end());//方法三
	
	for(auto el:um) cout<<el.first<<" "<<el.second<<"\n";
	//ks 15
	return 0;
}
```
##### 查找元素方式
1. 計算某元素數量：[count()](https://cplusplus.com/reference/unordered_map/unordered_map/count/)
	- count(key)
	- 通常回傳 1 或 0，因為 `key` 值不可重複
	{{< vs 1>}}
2. 查找某元素位置：[find()](https://cplusplus.com/reference/unordered_map/unordered_map/find/)
	- find(key)
	- 回傳 `iterator`, 若沒有找到則回傳 `unordered_map::end()`

### 5. Unordered_Set
***
##### 更改元素方式
1. 新增某元素插入：[insert()](https://cplusplus.com/reference/unordered_set/unordered_set/insert/)
	- 方法一：insert(val)
	- 方法二：insert(iterator first, iterator last)
	- 方法三：insert(list)
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	unordered_set<int> us = {1,2,3,4,5};
	unordered_set<int> us2 = {-1,-2,-3};
	
	us.insert(100);//方法一
	us.insert(us2.begin(),us2.end());//方法二
	us.insert({200,300});//方法三
	
	for(auto el:us) cout<<el<<" ";
	//100 1 200 -3 2 300 -2 3 -1 4 5
	return 0;
}
```
2. 刪除某元素：[erase()](https://cplusplus.com/reference/unordered_set/unordered_set/erase/)
	- 方法一：erase(val)
	- 方法二：erase(iterator position)
	- 方法三：erase(iterator first, iterator last)
	
```C++
#include <bits/stdc++.h>
using namespace std;

int main(){
	unordered_set<int> us = {1,2,3,4,5};
	
	us.erase(2);//方法一
	us.erase(us.begin());//方法二
	us.erase(us.find(3),us.end());//方法三
	
	for(auto el:us) cout<<el<<" ";//4
	return 0;
}
```

##### 查找元素方式
1. 計算某元素數量：[count()](https://cplusplus.com/reference/unordered_set/unordered_set/count/)
	- count(val)
	- 通常回傳 1 或 0，因為 `val` 值不可重複
	{{< vs 1>}}
2. 查找某元素位置：[find()](https://cplusplus.com/reference/unordered_set/unordered_set/find/)
	- find(val)
	- 回傳 `iterator`, 若沒有找到則回傳 `unordered_set::end()`

### 補充 Queue & Stack
***
##### 何謂 Queue 與 Stack ?
- 容器種類： 兩者皆屬於容器配接器，由原先存在的容器、方法改造、結合而成
- `Queue` 譯為佇列，`Stack` 譯為堆疊。 
- `Queue` 的規則是先進先出(FIFO)，`Stack` 的規則則是先進後出(FILO)。  
- `Queue` 常用於 `BFS` (廣度優先搜索)，`Stack` 則用於 `DFS` (深度優先搜索)。  

##### 基本元素操作
- 推入容器／推出容器：[push()](https://cplusplus.com/reference/queue/queue/push/) & [pop()](https://cplusplus.com/reference/queue/queue/pop/)
- queue
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
- stack
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
### 總結 
***
1. 搜索資料的時間複雜度
	- Vector O(n)
	- Map/Set O(log n)
	- Unordered_map/Unordered_set O(1)
	{{< vs 1>}}
2. 佔用空間
	- Unordered_map/Unordered_set > Map/Set > Vector
	{{< vs 1>}}
3. **鍵值對**的容器使用參考
	1. `vector<pair<type, type>`
		- 當維護成本低 (於中間操作元素的機會小) 時，可以考慮使用
		- 當數據量過大，記憶體不足而無法以 `unordered_map` 進行儲存時，可以考慮使用 
	2. `map`
		- 當數據量不大，且 `key` 的類型 無法以 `hash function` 計算時，可以考慮使用
		- 當數據量不大，且需要有序的訪問 `key` 時，可以考慮使用
	3. `unordered_map`
		- 在記憶體允許情況下，並且不需有序的訪問所有元素時，應盡量使用
	{{< vs 1>}}
4. 容器內部方法提醒
	- vector 內部沒有 `find()` 、 `count()`
	- map 內部沒有 `operator +`
	- set 內部沒有 `operator +、[]`
	- unordered_map 內部沒有 `operator +`
	- unordered_set 內部沒有 `operator +、[]`
	{{< vs 1>}}
5. 其他參考意見
	- 需快速隨機存取 -> `vector`
	- 需有序訪問元素 -> `map`
	- 需查找某元素是否在某集合中 -> `set`
	- 需快速訪問特定元素 -> `unordered_map`
	> 如果你需要大量的插入和刪除，而不關心隨機存取 -> `list`  
	> 如果你需要隨機存取，而且關心兩端數據的插入和刪除 -> `deque`

### 資料來源
***
[C++ Reference](https://cplusplus.com/reference/stl/)  
[Medium C++ Container](https://wither23265.medium.com/stl-container%E7%89%B9%E6%80%A7-cc28fd8bc246)  
[CSDN Container Compare](https://blog.csdn.net/qq_44918090/article/details/120739010)