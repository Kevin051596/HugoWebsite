---
title: "Selenium 基礎語法"
date: 2022-08-20T21:05:13+08:00
draft: false
menu:
  sidebar:
    name: Selenium 基礎語法
    identifier: selenium-base
    weight: 10
    parent: selenium
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

### Selenium 基本操作
***
##### **開啟瀏覽器、前往特定網頁**
（以下以 `Edge` 實作）
載入需要的套件
```Python
from selenium import webdriver
```
{{< vs 1>}}
開啟瀏覽器視窗  
- 方法一：執行前需開啟 chromedriver.exe 且與執行檔在同一個工作目錄  
- (推薦)方法二：或是直接指定 exe 檔案路徑
```Python
browser = webdriver.Edge()
browser = webdriver.Edhe("桌面\msedgedriver")
```
{{< vs 1>}}
最後設定讓網只要前往的網頁。爬蟲結束後，記得關閉瀏覽器視窗
```Python
browser.get("http://www.google.com") # 更改網址以前往不同網頁
browser.close() # 關閉瀏覽器視窗
```
{{< vs 1>}}
> 若為其他瀏覽器，則只要改變瀏覽器名稱就好
```Python
browser = webdriver.Firefox()
browser = webdriver.Safari()
```
{{< vs 2>}}
***
##### **調整視窗大小**
調整為最大視窗，調整為最小視窗  
通常會放在前往網址之前
```Python
browser.maximize_window()
browser.minimize_window()
```
{{< vs 2>}}
***
##### **定位 WEB 元素**
主要有兩種寫法(此處以 `class name` 為依據定位)，我推薦第二種方法
- `find_element_by_class_name(...)`
- `find_element(By.CLASS_NAME, ...)`
```Python
element = driver.find_element_by_class_name("你的 Web 元素的 Class Name")

from selenium.webdriver.common.by import By
element = driver.find_element(By.CLASS_NAME, "你的 Web 元素的 Class Name")
```
{{< vs 1>}}
如果需要定位多個元素，在後面加上 `s` 就可以了
- `find_elements_by_class_name(...)`
- `find_elements(By.CLASS_NAME, ...)`
```Python
element = driver.find_elements_by_class_name("你的 Web 元素的 Class Name")

from selenium.webdriver.common.by import By
element = driver.find_elements(By.CLASS_NAME, "你的 Web 元素的 Class Name")
```
{{< vs 1>}}
其他的定位依據
- `By.CSS_SELECTOR` 依照 CSS 選擇器
- `By.ID`           依照 id
- `By.TAG_NAME`    依照 DOM element 的 Tag
- `By.XPATH`        依照自訂規則
- `By.NAME`         依照 name
- `By.LINK_TEXT`    依照連結文字
- `By.PARTIAL_LINK_TEXT`    依照部分連結文字
{{< vs 1>}}

By.XPATH 如何自訂規則
```Python
element = driver.find_element(By.XPATH, "//tag name[@special tag='...']")
```
{{< vs 1>}}
- 例子一：定位 data-sizing 為 px 的 div
```Python
element = driver.find_element(By.XPATH, "//div[@data-sizing='px']")
```
{{< vs 1>}}
- 例子二：定位 placeholder 為 Your Name 的 input
```Python
element = driver.find_element(By.XPATH, "//input[@placeholder='Your Name']")
```
{{< vs 2>}}
***
##### **輸入及點擊**
- `send_keys(...)`：可以用來輸入文字，也可以用來上傳檔案( 前提是該 DOM 元素為 input )  
- `click()`：用來點擊
```Python
element = driver.find_element(By.CLASS_NAME, "你的搜尋框 Class Name") # 定位搜尋框
element.send_keys("Selenium Python") # 傳入字串
element.clear() # 清除

button = driver.find_element(By.CLASS_NAME, "你的搜尋按鈕 Class Name")  # 定位搜尋按鈕
button.click() # 點擊
```
{{< vs 1>}}
上傳一個檔案：將檔案的絕對路徑放入就可以了
```Python
element = driver.find_element(By.CLASS_NAME, "你的搜尋框 Class Name")
element.send_keys("檔案的絕對路徑")
```
{{< vs 1>}}
上傳多個檔案：將全部檔案的絕對路徑用 `\n` 串起來後，再放入就可以了
```Python
element = driver.find_element(By.CLASS_NAME, "你的搜尋框 Class Name")
element.send_keys("第一個檔案的絕對路徑\n第二個檔案的絕對路徑\n...")
```
{{< vs 2>}}
***
##### **模擬鍵盤打字**
此外 `send_keys` 也可以用於模擬鍵盤打字，甚至是快捷鍵功能
```Python
from selenium.webdriver.common.keys import Keys
element.send_keys(Keys.CONTROL, "c") # 模擬 Ctrl+C
element.send_keys(Keys.CONTROL, "v") # 模擬 Ctrl+V
```
{{< vs 2>}}
***
##### **瀏覽紀錄**
對瀏覽紀錄模擬跳轉
```Python
browser.forward() # 前往下一筆瀏覽紀錄/下一頁
browser.back() # 前往上一筆瀏覽紀錄/上一頁
```
{{< vs 2>}}
***

##### **滾動頁面**
`selenium` 沒有滾動的語法，但我們可以透過執行 `Javascript` 程式來達到滾動效果  
接下來會比較各種 `Javascript` 的滾動語法  
- 滾動到距離頁面頂部 500px 的位置
```Python
pos = 500
js = 'window.scrollTo({top: %d, behavior: "smooth"})' % pos
browser.execute_script(js)
```
{{< vs 1>}}
- 這裡是處理「內嵌滾動」的方法
  1. 首先你要定位該滾條元素的位置(通常為該元素的 div 或其他容器 tag)
  2. 滾動到距離此特定元素頂部 500px 的位置  
```Python
pos = 500
js = 'document.querySelector("{0}").scrollTop={1}'.format(element, pos)
browser.execute_script(js)
```
{{< vs 1>}}
- 滾動至該元素出現
```Python
js = 'document.querySelector("%s").scrollIntoView(false)' % element
browser.execute_script(js)
```
{{< vs 2>}}
***
### 資料來源
<!-- [CSDN Python combine Vue](https://blog.csdn.net/m0_38051293/article/details/101382493)   -->
[Medium 動態網頁爬蟲第一道鎖 — Selenium教學：如何使用Webdriver、send_keys（附Python 程式碼）](https://reurl.cc/ERoZOR)  
[Medium 動態網頁爬蟲第二道鎖 — Selenium教學：如何使用find_element(s)取得任何網頁上能看到的內容(附Python 程式碼)](https://reurl.cc/4po323)  
[Geeksforgeeks Selenium-tutorial](https://www.geeksforgeeks.org/selenium-python-tutorial/)