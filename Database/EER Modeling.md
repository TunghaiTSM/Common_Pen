###### tags: `database` `note` `thu`


# EER Modeling

回到首頁： [DB-Note](/GbetBojTSMCOFmpVUFB_TQ)
## 簡介
如果你仔細的看了前面的ER-Diagram的介紹應該就不難發現Entity跟Entity之間的關係都隔著一個Relationship。
可是當Entity跟Entity之間有關聯，但是又沒有適當的Relationship可以把他們關聯起來該怎麼辦呢？
- e.g. Employee有很多種(打字、掃地、管理...etc)，但我們只能把他們全部不加分類的歸在同一個Entity嗎？這也是為什麼前面會出現這麼不直覺的奇怪圖形的原因之一：
![](https://i.imgur.com/he7jwJn.png)
自己監督自己?!社會突然理想了起來有木有？！

### 這個頁面主要會聚焦在EER比ER Diagram為此所多出的概念:
- ***Subclasses*** 跟 ***Super classes***
- ***Specialization*** 跟 ***Generalization***
- ***Category type*** 跟 ***union type***
- ***Aggregation*** 跟 ***Association***

## 我們先快速的對名詞有個概念
### 1. ***Subclasses*** 跟 ***Super classes***
![](https://i.imgur.com/dYMjm8L.png)
- TRIANGLE、SQUARE、CIRCLE都是一種Shape $\Longrightarrow$ 為SHAPE的***Subclasses***
- SHAPE有的TRIANGLE、SQUARE、CIRCLE都有 $\Longrightarrow$ 為三種形狀的***Super class***

### 2. ***Specialization*** 跟 ***Generalization***
- ***Specialization***: 長出Subclasses的過程。
- ***Generalization***: 長出Super classes的過程。

## 施工中
### 3. ***Category*** 跟 ***union type*** 
### 4. ***Aggregation*** 跟 ***Association***
##



## Notations
### U (Union)
![](https://i.imgur.com/c6KojVx.png)
![](https://i.imgur.com/XMjHbaw.png)


### O (Overlapped)
![](https://i.imgur.com/KlPJIkX.png)
![](https://i.imgur.com/qNTEKMX.png)

### D (Disjoint)
![](https://i.imgur.com/3h79f3n.png)
![](https://i.imgur.com/pZtzmw7.png)
