---
title: "Selenium 隨筆紀錄 "
date: 2022-08-20T21:05:13+08:00
draft: false
menu:
  sidebar:
    name: Selenium 隨筆紀錄
    identifier: selenium-debug
    weight: 10
    parent: selenium
tags: ["Basic", "Multi-lingual"]
categories: ["Basic"]
---

### 設置超時限制器
```Python
browser.set_page_load_timeout(20)
browser.set_script_timeout(20)
```

### 隱藏瀏覽器日誌

```Python
edge_options = webdriver.EdgeOptions()
edge_options.add_argument('-disable-gpu')
edge_options.add_argument('log-level=3')
browser = webdriver.Edge("python/msedgedriver.exe", options=edge_options)
```

### 瀏覽器頁面加載偵測
```Python
from selenium.webdriver.common.by import By
from selenium.webdriver.support.wait import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
WebDriverWait(browser, 30).until(EC.presence_of_element_located((By.CLASS_NAME, 'image')))
```

### 破解反爬蟲網頁
我們可以先用正常手段進入後，查詢該 user agent 資訊，並將該資訊用於爬蟲的使用者資訊，以這個 user agent 資訊破解反爬蟲檢驗
```Python
user_agent = 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36 Edg/108.0.1462.42'
opt = webdriver.EdgeOptions()
opt.add_argument('--user-agent=%s' % user_agent)
browser = webdriver.Edge(executable_path="msedgedriver.exe", options=opt)
```

### 資料來源