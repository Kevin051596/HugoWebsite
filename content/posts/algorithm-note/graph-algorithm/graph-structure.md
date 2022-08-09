---
title: "Graph Structure"
date: 2022-08-05T22:42:14+08:00
hero: /images/posts/writing-posts/graph.jpg
menu:
  sidebar:
    name: graph structure
    identifier: algorithm-note-graph-algorithm-structure
    parent: algorithm-note-graph-algorithm
    weight: 10
tags: ["Basic", "Multi-lingual"]
categories: ["Basic"]
draft: false
---

Graph 中譯為圖，為一種用來記錄關係的方法  
一張圖的資訊通常包含點（vertex）、邊（edge），有些會替點、邊增加權重以詳訴其關係。  
一張圖的繪製不受點、線的外觀、位置影響。

### 常見的圖樣
***

#### 同構圖 Isomorphism / Isomorphic  
   
當兩張圖的連接方式一樣時，稱為「同構圖」  
  
![同構圖一](https://web.ntnu.edu.tw/~algo/Graph5.png)

圖上的點任意移動，只要兩點的關係不變，也屬同構圖

![同構圖二](https://web.ntnu.edu.tw/~algo/Graph6.png)

同構圖能夠傳遞同樣的資訊，因此繪製圖時只需在意能否表達清楚。
***

#### 有向圖/無向圖 Directed Graph （Digraph）/ Undirected graph

簡單來說，有向圖的邊具有方向性，用以表示其單向關係。  
另外，無向圖的邊，為雙向關係。

![有向圖](https://web.ntnu.edu.tw/~algo/Graph7.png)
![無向邊](https://web.ntnu.edu.tw/~algo/Graph4.png)
***

### 圖的資料結構常見方式
***
圖在程式語言中可以採用下列三種方式儲存其資料：　　
- Edge List
- Adjacency Matrix
- Adjacency Lists

#### Edge List
Edge List 主要使用陣列來紀錄每個點之間的邊  
![Edge_List](https://web.ntnu.edu.tw/~algo/GraphDS1.png)  
- 優點：直觀簡單，節省空間
- 缺點：不易計算，效率較低  
```C++
struct Edge{ int a,b; };
Edge edge[4];
void edge_list(){ 
    for(int i=0;i<4;i++){
        cin>>edge[i].a>>edge[i].b;
    }
}
```
***

#### Adjacency Matrix
Adjacency Matrix 主要使用方陣來記錄其連接資料。  
> 讀法 (欄，列)  

例如：第二張圖的元素 (0,4) 表示點 0 到點 4 之間有兩條線連結。  
![Adjacency_Matrix](https://web.ntnu.edu.tw/~algo/GraphDS2.png)
![Adjacency_Matrix2](https://web.ntnu.edu.tw/~algo/GraphDS4.png)
- 優點：資料詳細，可儲存多種資料，如：邊數、權重
```C++
int graph[5][5];
void adjacency_matrix(){
    for (int i=0; i<5; ++i){
        for (int j=0; j<5; ++j){
            graph[i][j] = 0;
        }
    }
    int a, b, w;
    while (cin >> a >> b >> w) graph[a][b] = w;
}
```
***

#### Adjacency Lists
Adjacency Lists 主要使用陣列或者鏈表來記錄所有相鄰的點資料
![Adjacency_Lists](https://web.ntnu.edu.tw/~algo/GraphDS6.png)

1. 採用陣列方式
```C++
int list[5][100];
int size[5];
void adjacency_lists(){
    for (int i=0; i<5; ++i) size[i] = 0;
    int a, b;
    while (cin >> a >> b) list[a][size[a]++] = b;
}
```  
2. 採用鏈表方式
```C++
struct Element{
    int b;
    Element* next;
};
Element* list[5];

void add_edge(int a, int b){
    Element* e = new Element();
    e->b = b;
    e->next = list[a];
    list[a] = e;
}
void adjacency_lists(){
    for (int i=0; i<5; ++i) list[i] = 0;
    int a, b;
    while (cin >> a >> b) add_edge(a, b);
}
```  
3. 使用 STL 的 vector、list
```C++
vector<int> list[5];
void adjacency_lists(){
    for (int i=0; i<5; ++i) list[i].clear();
    int a, b;
    while (cin >> a >> b) list[a].push_back(b);
}
```  
***

### 資料來源
[Graph](https://web.ntnu.edu.tw/~algo/Graph.html#1)