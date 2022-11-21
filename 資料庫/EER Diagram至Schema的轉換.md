###### tags: `database` `note` `thu`
{%hackmd theme-dark %}

# EER Diagram至Schema的轉換
本頁將會聚焦在將EER Diagram轉換至Schema的演算法。
詳細請參見課本Ch9。


## 簡介
這裡只會講大概的方向，詳細步驟請見[老師筆記](/GK34a_FiRhSZHvJPx3m4ag)。

## 1. Subclasses / Superclasses 的處理方式:

### a. 把泛化後抽象出來的資料分開放，其它的用Foreign key連結
![](https://i.imgur.com/BDgxRAy.png)


### b. 退化回泛化前
![](https://i.imgur.com/uIAVWD0.png)

### c. 全部瞎雞巴合成一個表格 (那當初為什麼還要泛化？!)

#### Example 1 (原c)
![](https://i.imgur.com/NQOUsky.png)
![](https://i.imgur.com/3FZDAYI.png)

#### Example 2 (原d)
![](https://i.imgur.com/DjojNKs.png)
![](https://i.imgur.com/hWG5dVm.png)


## 2. Union Type 的處理方式：
### Note: 該處relationship採取Relationship relation的處理方式。
### a. 各個Superclass各開一個表格
### b. 有共同的key就用，沒有就生出一個來(Surrogate key, dummy primary key)
### c. 把該primary key用foreign key 連起來。
![](https://i.imgur.com/urplPkH.png)
![](https://i.imgur.com/wrvNLHp.png)



# 考古
![](https://i.imgur.com/SexYVOk.jpg)
