---
title: "Python 商家資料抓取"
date: 2022-08-20T21:05:13+08:00
draft: true
menu:
  sidebar:
    name: Python 商家資料抓取
    identifier: selenium-project
    weight: 10
    parent: selenium
tags: ["Basic", "Multi-lingual"]
categories: ["Basic"]
---

### Selenium 實作
***
```Python
import time
from datetime import datetime
from selenium import webdriver
from bs4 import BeautifulSoup as Soup
from selenium.webdriver.common.by import By
from selenium.webdriver.support.wait import WebDriverWait
from selenium.webdriver.common.action_chains import ActionChains
from selenium.webdriver.support import expected_conditions as EC


if __name__ == '__main__':

    browser = webdriver.Edge()
    url = "https://reurl.cc/KQ0xNj"
    browser.set_page_load_timeout(10)
    browser.set_script_timeout(10)

    try:
        browser.get(url)
    except:
        browser.execute_script("window.stop()")

    browser.maximize_window()
    soup = Soup(browser.page_source,"lxml")

    data_index = 4 
    sort_index = 2
    WebDriverWait(browser, 30).until(EC.presence_of_element_located((By.CLASS_NAME, 'S9kvJb')))
    category_click = browser.find_elements(By.CLASS_NAME,'S9kvJb')
    print(category_click[data_index].text, "pass")
    time.sleep(1)
    category_click[data_index].click()
    time.sleep(1)
    category_click = browser.find_elements(By.CLASS_NAME,'fxNQSd')
    print(category_click[sort_index].text, "pass")
    time.sleep(1)
    category_click[sort_index].click()


    time.sleep(1)
    js = 'document.getElementsByClassName("m6QErb DxyBCb kA9KIf dS8AEf")[0].scrollTop=1000000'
    browser.execute_script(js)

    time.sleep(1)
    soup = Soup(browser.page_source,"lxml")
    all_reviews = soup.find_all(class_ = 'jftiEf fontBodyMedium')
    print("pass")
    for ar in all_reviews:
        name = ar.find(class_ = "d4r55").text
        star_review = str(ar.find(class_ = "kvMYJc").get('aria-label'))
        date_review = ar.find(class_ = "rsqaWe").text
        text_review = ar.find(class_ = "wiI7pd").text
        print(name,"\n",star_review,"\n",date_review,"\n",text_review,"\n")
```

### 錯誤處理
***
USB: usb_device_handle_win.cc:1048 Failed to read descriptor from node connection: 連結到系統的某個裝置失去作用。 (0x1F)

### 資料來源
[Medium Google Map Review 動態爬蟲：如何獲取店家評論內容、圖片以及篩選評論（附Python程式碼）](https://reurl.cc/W1GXpD)  
[Medium Google Map Review 動態爬蟲：如何解決評論動態加載的問題以及在不同視窗間跳轉、滑動（附Python程式碼）](https://reurl.cc/YXejZa)
