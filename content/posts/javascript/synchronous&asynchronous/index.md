---
title: "JavaScript 的同步、非同步技巧"
date: 2022-12-20T23:18:28+08:00
description: 關於 JavaScipt 實現同步、非同步的方式
draft: false
menu:
  sidebar:
    name: 同步、非同步實現方式
    identifier: javascript-sync_asyn
    parent: javascript
    weight: 10
tags: ["Front-end", "JavaScript", "Multi-lingual"]
categories: ["Front-end", "JavaScript"]
---

本篇主要說明為什麼 JavaScript 可以做到同步處理、非同步處理，以及如何代碼實現。

### 前言
***
`JavaScript` 屬於**單線程**的瀏覽器行程。意思是同時間只做一段代碼，也就是只能一件一件事逐步完成。
好處是架構簡單，環境單純。但壞處就是，當其中一件事時間複雜度過高，會拖累整體程式效率，使得後續程式幾乎無法執行。

因此為了解決這個問題，`JavaScript` 將事件拆為**同步**與**非同步**兩種，來改善單線程的缺點。

### 同步 (Synchronous)
***
與字面上意思剛好相反，同步在 `JavaScript` 中代表一次只能執行一段程式，執行結束在執行下一段。
{{< split 5 7>}}
```javascript
console.log(1);
console.log(2);
console.log(3);
```
---
輸出結果：  
1  
2  
3  
{{< /split >}}

### 非同步/異步 (Asynchronous)
***
與同步相反，同時間可以執行多段程式碼，每段的程式碼執行完成後繼續執行該段之後的程式碼，彼此之間不會影響。  
{{< split 7 5>}}
```javascript
let xhs = 3
setTimeout(() => {
    xhs = xhs + 5
    console.log(xhs)
}, 1000)
xhs = xhs + 4
console.log(xhs)
```
---
輸出結果：  
7  
12
{{< /split >}}
此段程式解釋：
1. 宣告一個變數 `xhs` 為 3
2. 邊等待一秒的時候，執行 `xhs = xhs + 4` 以下的程式，因此現在 `xhs = 7`，並且將其打印
3. 一秒過後執行 `xhs = xhs + 5`，並且將其打印

### 任務佇列和事件迴圈
***
Javascript 執行時，通常在主線程執行程式，此外還提供一個任務佇列(Task Queue)，負責儲存當前程式要處理的非同步程式(實際上，根據異步任務的類型，存在多個任務佇列)。  

因此整個程式的流程可以簡單理解成，Javascript 先執行完所有主線程內的程式後，接著查看任務佇列內有沒有程式，有就將其丟入主線程繼續執行直到任務佇列中沒有程式須被執行。  

而 Javascript 一遍又一遍檢查任務佇列中有沒有異步程式須被處理的過程，就叫做事件迴圈(Event Loop)

### Promise
***
**說明**：`Promise` 是用來改善 `JavaScript` 的非同步語法結構。本身是一個建構函數，需要使用 `new` 來建立新物件，而這個新物件可以
使用其中的原型方法(如：`catch`、`then`、`finally`)。

**結構**：`Promise` 建構函式建立同時，必須傳入一個函式作為參數（executor function），此函式的參數包含 `resolve`, `reject`，這兩個方法分別代表成功與失敗的回傳結果，特別注意這兩個僅能回傳其中之一，回傳後表示此 `Promise` 事件結束
```javascript
new Promise(function(resolve, reject) { 
	resolve(); // 正確完成的回傳方法
	reject();  // 失敗的回傳方法
});
```
{{< vs 1>}}
**狀態**：`Promise` 的關鍵在處理非同步的事件，而非同步的過程中也包含著不同的進度狀態，如下：  
- pending：事件已經運行中，尚未取得結果
- resolved：事件已經執行完畢且成功操作，回傳 `resolve` 的結果
- rejected：事件已經執行完畢但操作失敗，回傳 `rejected` 的結果
![Promise 狀態流程](https://firebasestorage.googleapis.com/v0/b/casper-de5d5.appspot.com/o/images%2Fblog%2F202002%2Fimg-promise-pending.png?alt=media&token=f5a5607b-4436-44e6-ab1f-0d8dd4bf59b3)  
{{< vs 1>}}
進入新狀態後不可回溯，同時會調用接下來的 `then`、`catch` 方法  
{{< vs 1>}}

**寫法**：接下來要說明與 `Promise` 相關的幾種常見寫法  
{{< vs 1>}}
與 `return` 搭配使用，可以回傳任何表達式 
- 如果是回傳 `Promise` 函式，則會繼續遵循 `then` 及 `catch` 的運作  
- 如果不是，在下一個 `then` 則可以取得結果  

{{< split 7 5>}}
```javascript
function promise(num) {
  return new Promise((resolve, reject) => {
    num ? resolve(`${num}, 成功`) : reject('失敗');
  });
}
const test = num => num;

promise(1)
  .then(success => {
    console.log(success);
    return promise(2);
  })
  .then(success => {
    console.log(success);
    return test(0);
  })
  .then(success => { 
    console.log(success);
    return promise(3);
  })
  .then(success => { 
    console.log(success);
    return promise(0);
  })
  .then(success => { 
    console.log(success);
    return promise(3);
  })
  .catch(fail => {
    console.log(fail);
  })
```
---
輸出結果：  
1,  成功  
2,  成功  
0  
3, 成功  
失敗  
{{< /split >}}
{{< vs 1>}}
程式碼說明：  
1. 第一個 Promise 回傳成功結果，所以執行第一個 `then`，之後回傳新的 `Promise`   
2. 第二個 Promise 回傳成功結果，所以執行第二個 `then`，之後回傳一個非 `Promise` 的表達式
3. 非 Promise 的表達式回傳結果，因為沒有錯誤的選擇，所以直接執行第三個 `then`，之後回傳新的 `Promise`
4. 第三個 Promise 回傳失敗結果，直接跳到最後的 `catch` 並結束   
{{< vs 1>}}

只用 then 取出成功或失敗結果
{{< split 7 5>}}
```javascript
function promise() {
  return new Promise((resolve, reject) => {
    const num = Math.random() > 0.5 ? 1 : 0;
    if (num) resolve('成功');
    reject('失敗')
  });
}

promise()
  .then((success) => {
    console.log(success);
  }, (fail) => {
    console.log(fail);
  })
  .then((success) => {
    console.log(success);
  }, (fail) => {
    console.log(fail);
  })
```
---
輸出結果：  
成功  
undefind
{{< /split >}}
{{< vs 1>}}
程式碼說明：  
1. 執行 `Promise`，回傳成功結果，執行 `then` 中的 `resolved` 函式
2. 沒有回傳函式，所以默認回傳成功結果，但因為沒有賦值，輸出 `undefind`
{{< vs 1>}}

使用 finally 終止
{{< split 7 5>}}
```javascript
promise(1)
  .then(success => {
    console.log(success);
  }).finally(() => {
    console.log('done');
  })
```
---
輸出結果：  
1  
done  
{{< /split >}}
{{< vs 1>}}
程式碼說明：  
程式碼結束可以使用 `finally` 方法來結束程式

**最後介紹 Promsie 的一些方法**
- `all` -> 多個 `Promise` 行為同時執行，全部完成後統一回傳。
- `race` -> 多個 `Promise` 同時執行，但僅回傳第一個完成的。
- `Promise.reject`, `Promise.resolve` -> 定義 `Fulfilled` 或 `Rejected` 的 `Promise` 物件  
{{< vs 1>}}

**Promise.all**  
透過陣列的形式傳入多個 promise 函式，在全部執行完成後回傳陣列結果
{{< vs 1>}}
{{< split 7 5>}}
```javascript
var p1 = Promise.resolve(3);
var p2 = 1337;
var p3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'foo');
});

Promise.all([p1, p2, p3]).then(values => {
  console.log(values);
});
```
---
輸出結果：  
[3, 1337, "foo"]  
{{< /split >}}

**Promise.race**  
透過陣列的形式傳入多個 promise 函式，在全部執行完成後回傳單一結果，結果為第一個運行完成的  
{{< split 7 5>}}
```javascript
var resolvedPromisesArray = [Promise.resolve(33), Promise.resolve(44)];

var p = Promise.race(resolvedPromisesArray);
// immediately logging the value of p
console.log(p);

// using setTimeout we can execute code after the stack is empty
setTimeout(function(){
    console.log('the stack is now empty');
    console.log(p);
});
```
---
輸出結果：  
Promise { <state>: "pending" }  
the stack is now empty  
Promise { <state>: "fulfilled", <value>: 33 }  
{{< /split >}}

**Promise.resolved, Promise.reject**  
這兩個方法是直接定義 `Promise` 物件已經完成的狀態`（resolve, reject）`，與 `new Promise` 一樣會產生一個新的 `Promise` 物件，**但其結果是已經確定的**
{{< split 7 5>}}
```javascript
var result = Promise.resolve('result');
result.then(res => {
  console.log('resolved', res); // 成功部分可以正確接收結果
}, res => {
  console.log('rejected', res); // 失敗部分不會取得結果
});
```
---
輸出結果：  
resolved, result  
{{< /split >}}
{{< split 7 5>}}
```javascript
var result = Promise.reject('result');
result.then(res => {
  console.log("resolved", res);
}, res => {
  console.log("rejected", res); // 只有此段會出現結果
});
```
---
輸出結果：  
rejected, result  
{{< /split >}}
### Async/await
***
說明：為 `ES7` 加入 `JavaScript` 的 `Promise` 語法糖。主要將非同步程式（如 `setTimeout`, `setInterval`, `fetch` )更改為同步程式執行。  
注意：async 一定要搭配 await 使用  
{{< vs 1>}}
沒有用 async/await 執行
{{< split 7 5>}}
```javascript
const count = (t,s) => {
  let a = 0;
  let timer = setInterval(() => {
    console.log(`${t}${a}`);
    a = a + 1;
    if(a>5){
      clearInterval(timer);
    }
  },s);
};

console.log(1); 
count('test', 100);
console.log(2);
```
---
執行結果：  
1  
2  
test 0  
test 1  
test 2  
test 3  
test 4  
test 5  
{{< /split >}}
{{< vs 1>}}
有用 async/await 執行
{{< split 7 5>}}
```javascript
~async function(){  
  const count = (t,s) => {
      return new Promise(resolve => {
        let a = 0;
        let timer = setInterval(() => {
          console.log(`${t}${a}`);
          a = a + 1;
          if(a>5){
            clearInterval(timer);
            resolve();  // 表示完成
          }
        },s);
      });
    };

  console.log(1); 
  await count('test', 100);
  console.log(2);
}();
```
---
輸出結果：  
1  
test 0  
test 1  
test 2  
test 3  
test 4  
test 5  
2
{{< /split >}}
此段程式說明：  
雖然 count 是個非同步程式，但是因為 await 語法，所以我們必需等待 count 結束後才能值星後面的程式，所以整體程式運行變成同步處理的效果。

### 資料來源
[Blog - Promise](https://www.casper.tw/development/2020/02/16/all-new-promise/)  
[MDN Web Doc - Promise](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Promise)
