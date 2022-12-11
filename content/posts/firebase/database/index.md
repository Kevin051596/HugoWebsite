---
title: "Firebase DBD illustrated book - Database"
date: 2022-12-07T21:05:13+08:00
draft: false
menu:
  sidebar:
    name: firebase/database 
    identifier: firebase-database
    weight: 10
    parent: firebase
tags: ["Basic", "Multi-lingual"]
categories: ["Basic"]
---
此篇主要說明我是如何從 Firebase 的 database、realtime database 中獲取資料、修改資料、刪除資料、增加資料等操作

### 預先操作

1. 引入 firebase 、 getFirestore 、 collection 等函示庫
2. 設定 firebaseConfig ，用來提供 firebase 設定的資訊
3. 初始化 firebase 功能

```Javascript
import firebase from "firebase/compat/app"
import { getFirestore, collection } from "firebase/firestore"

const firebaseConfig = {
  apiKey: ...,
  authDomain: ...,
  projectId: ...,
  storageBucket: ...,
  messagingSenderId: ...,
  appId: ...,
  measurementId: ...
}

const firebaseApp = firebase.initializeApp(firebaseConfig)
```

### 如何找到資料位置

首先要設定資料庫來源
```Javascript
var db = getFirestore(firebaseApp)
```

- collection 查詢
  - 集合級別的定位
  - 語法：`collection(db, "集合名")`
- collection 查詢，定位特殊文件
  - 可以透過 `where` 定位特殊資料
  - 語法：`collection(db, "cities"), where("state", "==", "CA")`
- doc 查詢　
  - 更為準確的定位
  - 語法：`doc(db, "集合名", "文件名")`

### 獲取資料和即時資料更新

- 獲取即時多筆資料
```Javascript
import { onSnapshot } from "firebase/firestore"
const catchData = onSnapshot(/*資料位置*/, (querySnapshot) => {
  querySnapshot.forEach((doc) => {
    console.log(doc.id, " => ", doc.data());
  })
})
```

- 只是獲取多筆資料（不一定為最新）
```Javascript
import { getDocs } from "firebase/firestore"
const catchData = await getDocs(/*資料位置*/).forEach((doc) => {
  console.log(doc.id, " => ", doc.data());
})
```

### 增加資料、修改資料

- 增加資料：`setDoc`
  - 此處的資料位置須自己設定，至少需到達文件層級
```Javascript
import { setDoc } from "firebase/firestore"; 
await setDoc(/*資料位置*/, data);
```
- 增加資料：`addDoc`
```Javascript
import { addDoc } from "firebase/firestore"; 
const addNewDocumnet = /*新增的資料*/ => {
  addDoc(/*資料位置*/, { /*新增的資料*/ })
}
```

- 更改資料
```Javascript
import { updateDoc } from "firebase/firestore"; 
const updateDocument = /*更新的資料*/ => {
  updateDoc(/*資料位置*/, { /*更新的資料*/ })
}
```

### 刪除資料
```Javascript
import { deleteDoc } from "firebase/firestore"; 
const deleteDocument = await deleteDoc(/*資料位置*/)
```
