# 04
## 1. 了解ajax加载
*分析
-加载一个html的话是可以分为加载其中某个块（div）和加载整个页面，而不管加载其中任何一种都是需要本页面的一个块（div）来进行加载展示。加载的方法可以是$(ajax{}) 方法也可以是 $('#div').load() 方法。
## 2. 通过chrome的开发者工具，监控网络请求，并分析
## 3. 用selenium完成爬虫
## 4. 具体流程如下：
<br>用selenium爬取https://news.qq.com/ 的热点精选


```
import time
from  selenium import webdriver
from bs4 import BeautifulSoup

driver=webdriver.Chrome()
driver.get("https://news.qq.com")

#了解ajax加载
for i in range(1,100):
    time.sleep(2)
    driver.execute_script("window.scrollTo(window.scrollX, %d);"%(i*200))



html=driver.page_source
bsObj=BeautifulSoup(html,"lxml")


jxtits=bsObj.find_all("div",{"class":"jx-tit"})[0].find_next_sibling().find_all("li")



print("index",",","title",",","url")
for i,jxtit in enumerate(jxtits):
 
    
   try:
        text=jxtit.find_all("img")[0]["alt"]
    except:
        text=jxtit.find_all("div",{"class":"lazyload-placeholder"})[0].text
   try:
       url=jxtit.find_all("a")[0]["href"]
    except:
        print(jxtit)
    print(i+1,",",text,",",url)
```
