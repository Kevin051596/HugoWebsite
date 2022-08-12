---
title: "Graph Traversal"
date: 2022-08-05T22:44:03+08:00
menu:
  sidebar:
    name: graph traversal
    identifier: algorithm-note-graph-algorithm-traversal
    parent: algorithm-note-graph-algorithm
    weight: 11
tags: ["Basic", "Multi-lingual"]
categories: ["Basic"]
draft: false
---

Graph traversal 基本上有兩種演算法：BFS、DFS。  
BFS 主要使用 STL 中的 queue 來遍歷圖資料。
DFS 主要使用 STL 中的 stack 來遍歷圖資料。

BFS 與 DFS 搜尋圖的方式如下
![DFS&BFS-Traversal](https://blog-c7ff.kxcdn.com/blog/wp-content/uploads/2015/05/dfsbfs_animation_final.gif)

### Breadth-Fist-Search
***
- 時間複雜度 O(n)
- 空間複雜度 O(n)
> 若存儲資料為 adjacency matrix 則複雜度為 O(n^2)。  
  若存儲資料為 adjacency lists 則複雜度為 O(n+e)，n為點數，e為邊數。

程式碼解析：
1. 「初始化」所有點的遍歷結果為未遍歷
2. 將遍歷的點放入 queue 中，並更新其遍歷結果
3. 彈出已遍歷的點，並重複 2、3 步驟直到跑完全圖

```C++
bool adj[9][9];
bool visited[9];

void BFS(){
    queue<int> q;
    //初始化
    for (int i=0; i<9; i++) visit[i] = false; 
    //BFS 主程式
    for (int k=0; k<9; k++){
        if (!visit[k]){
            q.push(k);
            visited[k] = true;
            while (!q.empty()){
                int i = q.front(); q.pop();
                for (int j=0; j<9; j++)
                    if (adj[i][j] && !visit[j]){
                        q.push(j);
                        visit[j] = true;
                    }
            }
        }
    }
}
```
***

### Depth-First-Search
***
- 時間複雜度 O(n)
- 空間複雜度 O(n)
> 若存儲資料為 adjacency matrix 則複雜度為 O(n^2)。  
  若存儲資料為 adjacency lists 則複雜度為 O(n+e)，n為點數，e為邊數。

只使用遞迴方法：
程式碼解析：
1. 「初始化」所有點的遍歷結果為未遍歷
2. 為其遍歷的點更新結果
3. 尋找遍歷的點下面的點，並重複 2、3 步驟直到無法往下尋找
4. 尋找最靠近起始點且未遍歷的點，並重複 2、3、4 步驟直到跑完全圖
> stack 也是採用遞迴方式編寫出來的資料結構

```C++
bool adj[9][9];
bool visit[9];

void traversal(){
    //初始化
    for (int i=0; i<9; i++) visit[i] = false;
    //DFS 主程式
    for (int i=0; i<9; i++)
        if (!visit[i]){
            visit[i] = true;
            DFS(i);
        }
}

void DFS(int i){
    for (int j=0; j<9; j++){
        if (adj[i][j] && !visit[j]){
            visit[j] = true;
            DFS(j);
        }
    }
}
```
***

### 題型紀錄
[Leetcode934 Shortest Bridge](https://leetcode.com/problems/shortest-bridge/)
(`DFS & BFS`)  
[Leetcode797 All Paths From Source to Target](https://leetcode.com/problems/all-paths-from-source-to-target/)
(`DFS`)  

### 資料來源
[Graph-Traversal](https://web.ntnu.edu.tw/~algo/Graph.html#5)  
[Graph-Algorithms-Explained](https://www.freecodecamp.org/news/graph-algorithms-explained/#:~:text=Graph%20algorithms%20are%20a%20set%20of%20instructions%20that,which%20can%20be%20used%20to%20model%20various%20problems.)