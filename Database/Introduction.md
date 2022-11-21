###### tags: `database` `note` `thu`

# Introduction

## 名詞定義
* **Data** &rarr; known facts
* **Relation** &rarr; a table that hosts many entries of data
* **Database** &rarr; a collection of ***related*** data
* **DBMS** &rarr; a collection of software to create and maintain DBs
Note: DBMS = (D)ata(b)ase (M)anagement (S)ystem

## Data models
結構就是：Data Structure + Operators
e.g. Linked list + Insert/Delete
### 實際存在的DB model
#### 1.  Relational
- Tables + SQL (4th Generation Language)
#### 2.  Network
- Circular Linked List + (Find first...)
#### 3. Hierarchical
- Tree + tree iterator
#### 4. Object-oriented
- Relational + 繼承
    
    
## Keys 種類
### 1. *Candidate*
- 不會重複的
### 2. *Primary*
- 常用的candidate key
### 3. *Super keys* (candidate的superset)
- e.g. {ID}, {ID, Email}都是Super keys(合起來可唯一決定key)
### 4. *Foreign keys*
- 來自別的table的Primary key (可連結表格, ER-model)

## Constraint 種類
### 1. ***Key***
- Candidate key不可重複
### 2. *Entity*
- Prime attribute (candidate key的attribute)非空
### 3. *Domain*
- 該㯗位的性質規定 (dtype, value range, format)
### 4. *No null*
- 非空//FIXME
### 5. *Referential integrity*
- 外來的Foreign key不可以隨便消失
    
## 比起傳統的檔案的好處
### 1. *Compact*
- 數位資料沒有體積
### 2. *Speed*
- 電腦比人快
### 3. *Automation*
- 可用程式自動化某些流程
### 4. *Concurrency*
- 內容是即時更新的
    
    
    
