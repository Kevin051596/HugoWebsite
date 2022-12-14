---
title: "Firebase DBD illustrated book - Storage"
date: 2022-12-10T23:40:13+08:00
draft: false
menu:
  sidebar:
    name: firebase/storage 
    identifier: firebase-storage
    weight: 10
    parent: firebase
tags: ["Basic", "Multi-lingual"]
categories: ["Basic"]
---
此篇主要說明我是如何從 Firebase 的 storage 中上傳檔案與下載檔案

### 預先操作

1. 引入 firebase 、 getFirestore 、 collection 等函示庫
2. 設定 firebaseConfig ，用來提供 firebase 設定的資訊
3. 初始化 firebase 功能
```Javascript
import firebase from "firebase/compat/app"
import { collection } from "firebase/firestore"
import { getStorage } from "firebase/storage"

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

### 如何上傳檔案

首先要設定檔案儲存端來源
```Javascript
var storage = getStorage(firebaseApp)
```
{{< vs 1>}}
- 藉由 JavaScript File API 、 Blob API 和 `uploadBytes` 下載  
接著設定將檔案儲存於何處，並藉由`uploadBytes`將位置與上傳的檔案綁在一起
這樣就能成功上傳了
```Javascript
import { ref as r, uploadBytes } from "firebase/storage"
const storageRef = r(storage, "在檔案儲存端的路徑")

uploadBytes(storageRef, /*上傳的檔案*/).then((snapshot) => {
  console.log("Uploaded a blob or file!", snapshot)
})
```

### 如何下載檔案

- 藉由 URL 下載  
一樣要先設定檔案儲存端
接著輸入「在檔案儲存端的路徑」`pathReference`
可以用一個「陣列」 `list` 去接下載下來的檔案
這樣就成功下載完成了
```Javascript
import { getStorage, getDownloadURL  } from "firebase/storage"
var storage = getStorage(firebaseApp)

const download = (pathReference, list) => {
  getDownloadURL(pathReference)
  .then((url) => {
    list.push(url)
  })
  .catch((error) => {
    console.log(error)
  })
}
```