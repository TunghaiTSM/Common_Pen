###### tags: `database` `note` `thu`

# ER Diagram至Schema的轉換
本頁將會聚焦在將ER Diagram轉換至Schema的演算法。
詳細請參見課本Ch9。

## 簡介(~~幹話~~)
我們既然在把資料轉換成Diagram的時候就已經把資料分類成三大類，
那我們就也把轉換成schema的步驟分成三大類: Entity、Relationship、Attributes。

## 1. ***Entity***
### a. 建一個table叫Employee。
### b. 把attribute們放進去當column的欄位(composite的打散)。
### c. 選一個key attribute當primary key。

### d. (Weak Entity) 把它依存的Regular Entity的Primary用"Foreign Key"的方式複制進來。

### Example 1 (Regular)
![](https://i.imgur.com/R2wZt9i.png)
#### 變成了
![](https://i.imgur.com/Q7ZpKyJ.png)

### Example 2 (Weak)
![](https://i.imgur.com/N4Z5pUd.png)
#### 變成了
![](https://i.imgur.com/EZD7W02.png)
- 這裡的ESSN為Employee的SSN(Foreign key)。



## 2. ***Relationship***

### a. Relationship relation
- 直接生出一個table來記錄誰參與了該relationship。
- 記錄時使用Foreign key。
- 而attribute們就照常放入。
### b. (Binary 1:N) Foreign key approach
- 在N side (數量比較多的那一邊)裡把1 side用Foreign key的形式記錄下來。

### c. (Binary 1:1 total) Just merge
- 當兩邊都是total participation時，就可以直接合併成同一個table。

### Note: 可以的話就用b，不能的話再用a。



### Example 1: SUPPLY (n-ary)
![](https://i.imgur.com/inicGwB.png)
#### 變成了
![](https://i.imgur.com/HouTNX4.png)

### Example 2: WORKS_ON (Binary M:N)
![](https://i.imgur.com/nggXKXC.png)
#### 變成了
![](https://i.imgur.com/82Lyrad.png)
- Essn指向Employee的Ssn
- Pno指向Project的Pnumber

### Example 3: WORKS_FOR (Binary 1:N)
![](https://i.imgur.com/rGs84vd.png)
#### 變成了
![](https://i.imgur.com/u977gOJ.jpg)

### Example 4: MANAGES (Binary 1:1)
![](https://i.imgur.com/dOpt3mL.png)
#### 變成了
![](https://i.imgur.com/z5dXAVe.jpg)





## 3. ***Attributes***
### a. Multivalued Attributes (多值屬性)
- 另外為該Attribute開一個table。
- 其中一個column對應到Entity的Primary key。
- 剩下的就把他原本的值也開一個column放入。
- (注意) 有的新版relational model會有array這種資料型態，就不要再傻傻的另開一個table了。 

### Example
![](https://i.imgur.com/G4bDQUa.png)
#### 變成了
![](https://i.imgur.com/6EdMXT9.png)
- 這裡的Dnumber為來自Department的Foreign key。


