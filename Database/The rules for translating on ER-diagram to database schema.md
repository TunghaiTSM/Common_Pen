###### tags: `database` `note` `thu`

# The rules for translating on ER-diagram to database schema

---
### Rule 1 : ***entity type -> relation schema***
### (regular entity type)
#### 1. Entity name (E1) -> Relation name (E'1)
#### 2. Ai of E1 ->Ai of E'1
#### 3. Composite attribute -> simple attribute
#### 4. Candidate key of E1 -> candidatekey of E'1
---
### Rule 2: ***weak entity type***
#### 1.Entity type name(WE1) -> relation name (WE'1)
#### 2.Attribute of WE1 ->atrribute of WE'1
#### 3.Composite attribute -> simple attribute
#### 4.Candidate key of WE1 -> candidate key of WE'1
#### 5.Identifying owner's primary key of WE'1 partical key -> WE'1 primary key

### 3. ***1:1***
#### case1:
#### 1.Choose one side, e.g. E1 as the base realtion
#### 2.Copy E2's primary key, e.g. x to E1 (base) as aforeign key
#### 3.Attribute of R to E1
#### 4.Composite attribute -> simple attributes
#### case2:
#### 1.Choose total=participation side, e.g. E1 as a foreign key
#### 2.Copy E2's primary key to E1 as a foreign key
#### 3.More attribute of R to E1
#### 4.Composite attribute -> simple attributes
#### case3:
#### 1.Choose the side with less tuples (in the future), e.g. E2 as the base
#### 2.Copy E1's primary key to E2 as a foreign key
#### 3.Move R's atttribute, e.g. r to E2 (base)
#### 4.Composite attribute -> simple attribute

### 4. ***1:N***
### Binary Relationship on 1:N
#### 1.choose N-side as the base E2
#### 2.copy E1's pk to E2
#### 3.attribute of R are worked to E2
#### 4.composite attribute -> simple attributes

### 5. ***binary relationship on M:N***
#### 1.Choose N-side as the base, e.g. E2
#### 2.Copy E1's primary key to E2
#### 3.Attribute of R are moved to E2
#### 4.composite attribute -> simple attributes

### 6. and 7. ***n-ary relationship n>=3***
#### 1.create a relationship relation R'
#### 2.從i到n的聯集Ei's primary key -> R as R's
#### 3.R's attribute -> R'
#### 4.composite attribute -> simple attributes
##
### 8. ***Specialization / Generalization*** 的處理方式
|   o    | u   |     d      |
|:------:| --- |:----------:|
| 8A、8D |     | 8A、8B、8C |
#### 8A (多表格: 適用於Superclass and subclasses):
#### 1.成立各個表格
#### 2.把屬性都歸過去(到各個subclasses裡)
#### 3.把 Primary key 拷貝過去
#### 4.Composite attribute -> single attribute (打散)
#### Example
![](https://i.imgur.com/ZicTeEl.png)
變成了
![](https://i.imgur.com/ppX6Rlx.png)

##
#### 8B (多表格: 適用於subclass relations only):
#### 1.為每個 subclass 成立表格
#### 2.把屬性歸到 subclass 去
#### 3.把 superclass 表格放進 subclass 表格
#### 4.Composite attribute -> single attribute (打散)
#### 5.Subclass pk = superclass pk
![](https://i.imgur.com/9igdwtW.png)
變成了
![](https://i.imgur.com/z1sqliN.png)

##
#### 8C (Single relation with one type attribute):
#### 1.成立一個大表格
#### 2.把所有 subclass , superclass attribute 移動到大表格
#### 3.Composite attribute -> simple attribute (打散)
#### 4.Superclass pk 移動到大表格
#### 5.最後加 attribute (subclass type)
#### Example
![](https://i.imgur.com/NQOUsky.png)
變成了
![](https://i.imgur.com/qWQ69Ux.png)

##
#### 8D (Single relation with multiple type attributes):
#### 1.成立大表格
#### 2.把所有 subclass , superclass attributes 移動到大表格
#### 3.Composite attribute -> single attribute (打散)
#### 4.Superclass primary key 移到大表格
#### 5.多加 E1 ~ En的表格
#### Example
![](https://i.imgur.com/DjojNKs.png)
變成了
![](https://i.imgur.com/hWG5dVm.png)

##
### 9. ***(U, Union type)***
#### 1.成立大表格
#### 2.把 entity name ->relation name
#### 3.把 attribute 放進 E1
#### 4.Composite attribute -> single attribute (打散)
#### 5.Check to see whether all superclass have the same primary key
- a. Yes : primary is X , move X to subclass as a pk 
- b. No : create a dummy primary key (surrogate key) , say Y => copy to all superclass as a dummy foreign key

#### Example
![](https://i.imgur.com/urplPkH.png)
變成了
![](https://i.imgur.com/wrvNLHp.png)
