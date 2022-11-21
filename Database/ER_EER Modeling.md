###### tags: `database` `note` `thu`


# ER/EER Modeling

回到首頁： [DB-Note](/GbetBojTSMCOFmpVUFB_TQ)
## 簡介
我們的目標就是，在針對生活中的資訊建立資料庫時， 
如何有結構的，並最大程度的避免資料庫裡的兩大禁忌：
1. ***不得*** 有 ***空欄位*** (null value)
2. ***不得*** 有 ***重複的資料*** (否則要更新資料的時候就要多個一起更新)

因此我們發展出了ER/EER Diagram。
它可以幫助我們釐清資料和資料之間的關係，以及我們如何去存放他們在schema裡。

本頁會主要聚焦於如何將資料轉換成ER/EER Diagram。

## 原則
ER-Model將一切的資料都拆解成三個部份 (類似物件導向的概念)：
### 1. ***Entity*** / 實體
![](https://i.imgur.com/Z4Y8cWc.png)
    資料的形成勢必和某些物件或實體(*Entity*)有關。
    其中還又有分:
- ***Weak Entity***
![](https://i.imgur.com/NVk0pTN.png)
這種實體只能依存於其它的實體而存在。
他的Primary Key只能在他自己的表格有用，出了他自己就不再是Candidate Key了。
往往會跟Identifying Relationship一起出現。

    
### 2. ***Relationship*** / 關係
![](https://i.imgur.com/7wkFoVd.png)
    實體和實體之間的關係(*Relationship*)往往也會產生許多相關的資料。
    其中也有分:
- ***Identifying Relationship***
![](https://i.imgur.com/vsSFWqh.png)
當一個實體因另一個實體而存在於這個Database裡時(e.g. 員工的家屬、學校的電腦)，就會形成Identifying Relationship。
而主要的實體(e.g. 員工)的Primary Key往往會以Foreign Key的形式被加入次要的實體(e.g. 家屬)的表格裡。

而我們也因為想瞭解實體和實體之間的關係的細節，所以衍生了下列的符號：
- ***Partial / Total Particapation***
![](https://i.imgur.com/FXZhZAT.png)
表示是否每個實體都有"***參加該關係***"。
單線為Partial，雙線為Total。

- ***Cardinality Ratio***
![](https://i.imgur.com/neOB5Am.png)
數字表示如果"***雙方都有實體參加該關係的前提下***"，那雙方實體的數量比為何。
如果可能為1對多，則是1:N。
如果雙方數量不定，則為M:N。
有時會以下面的符號來表示：
![](https://i.imgur.com/9tGtGQC.png)
  

### 3. ***Attribute*** / 屬性
![](https://i.imgur.com/nlm7bnC.png)
    實體(*Entity*)、實體和實體之間的關係(*Relationship*)往往也都會產出衍生的屬性(*Attribute*)資料。
這些又分成以下幾種：
- ***Key Attribute***
![](https://i.imgur.com/tNmn3sG.png)
通常為該實體/關係的Primary Key。

- ***Multivalued Attribute***
![](https://i.imgur.com/jxzpq8n.png)
同一個㯗位有時也會有許多同性質的資料。(e.g. 台灣的城市、老師的外號...etc)

- ***Composite Attribute***
![](https://i.imgur.com/FIcKseB.png)
像是名字、地址之類可以分很多段的資料。
在形成DB Schema時，通常會被打散然後直接分開寫入DB。


- ***Derived Attribute***
![](https://i.imgur.com/ctFTMBO.png)
當該屬性可以從同一個資料庫中得到線索並算出時，就被稱為Derived Attribute。
e.g. 資料庫內已經有所有部門的清單了。那此時"部門數量"的欄位就是Derived Attribute。






## Example
### ER-Diagram
![](https://i.imgur.com/Imz7Poe.png)

### DB Schema
![](https://i.imgur.com/ULlBx8p.png)

### SQL Code
![](https://i.imgur.com/V6ehxdb.png)



## Symbols
![](https://i.imgur.com/Z0aKA7m.png)
