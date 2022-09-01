---
title: "Selenium 基礎"
date: 2022-08-20T21:05:13+08:00
draft: false
menu:
  sidebar:
    name: Selenium 基礎
    identifier: data-processing-selenium-base
    weight: 10
    parent: data-processing
tags: ["Basic", "Multi-lingual"]
categories: ["Basic"]
mermaid: true
---

### 介紹
***
- `Selenium` 介紹：  
Selenium 是一個自動化工具，主要透過程式自動控制瀏覽器進行任何操作，如搜尋、點擊、滾動等。其腳本是由 Python、Java、C# 等語言撰寫，可適用於所有瀏覽器、主流操作系統等。

### Selenium 環境配置
***
1. `Selenium` 函式庫安裝
    > pip install Selenium
2. `Webdriver` 下載  
    - [Chrome](https://sites.google.com/a/chromium.org/chromedriver/downloads)
    - [Edge](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/)
    - [Firefox](https://github.com/mozilla/geckodriver/releases)
    - [Safari](https://webkit.org/blog/6900/webdriver-support-in-safari-10/)  
{{< alert type="info" >}} 記得檢查目前的瀏覽器版本，再下載對應的 `Webdriver` ，並要適時更新版本 
[<如何查詢瀏覽器版本>](https://www.ozchamp.com/professionals-d922-n1.html) {{< /alert >}}
  - 解壓縮檔案後，可以將 .exe 檔放於與 `Python` 一起的同個資料夾中，又或者使用者自己特定位置

3. `bs4` 函式庫安裝：
    > pip install bs4  
    
    - 什麼是 `bs4`：一個解析、遍歷、維護 `DOM` 的功能庫，協助使用者讀取網頁原始碼

### Selenium 基本操作
***
##### 開啟瀏覽器、前往特定網頁
（以下以 `Edge` 實作）
```Python
# 載入需要的套件
from selenium import webdriver
# 開啟瀏覽器視窗
# 方法一：執行前需開啟chromedriver.exe且與執行檔在同一個工作目錄
browser = webdriver.Edge()
# 方法二：或是直接指定exe檔案路徑
browser = webdriver.Edhe("桌面\msedgedriver")
browser.get("http://www.google.com") # 更改網址以前往不同網頁
browser.close() # 關閉瀏覽器視窗
```
> 若為其他瀏覽器，則只要改變瀏覽器名稱就好
```Python
browser = webdriver.Firefox()
browser = webdriver.Safari()
```
##### 調整視窗大小
```Python
browser.maximize_window() # 最大視窗
browser.minimize_window() # 最小視窗
```
##### 輸入及點擊
```Python
element = driver.find_element_by_class_name("你的搜尋框 Class Name") # 定位搜尋框
element.send_keys("Selenium Python") # 傳入字串
element.clear() # 清除

button = driver.find_element_by_class_name("你的搜尋按鈕 Class Name")  # 定位搜尋按鈕
button.click() # 點擊
```
> 如何快速尋找原始碼網頁元素  

![快速尋找網頁元素](快速尋找網頁元素_.gif)
##### 模擬鍵盤打字
```Python
from selenium.webdriver.common.keys import Keys
element.send_keys(Keys.CONTROL, "c") # 模擬 Ctrl+C
element.send_keys(Keys.CONTROL, "v") # 模擬 Ctrl+V
```
##### 瀏覽紀錄
```Python
browser.forward() # 前往下一筆瀏覽紀錄/下一頁
browser.back() # 前往上一筆瀏覽紀錄/上一頁
```

### 資料來源
<!-- [CSDN Python combine Vue](https://blog.csdn.net/m0_38051293/article/details/101382493)   -->
[Medium 動態網頁爬蟲第一道鎖 — Selenium教學：如何使用Webdriver、send_keys（附Python 程式碼）](https://reurl.cc/ERoZOR)  
[Medium 動態網頁爬蟲第二道鎖 — Selenium教學：如何使用find_element(s)取得任何網頁上能看到的內容(附Python 程式碼)](https://reurl.cc/4po323)  
[CSDN 內嵌 div 滾動](https://blog.csdn.net/LYX_WIN/article/details/119972741)  
[Geeksforgeeks Selenium-tutorial](https://www.geeksforgeeks.org/selenium-python-tutorial/)