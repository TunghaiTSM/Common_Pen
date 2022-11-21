###### tags: `database` `note` `thu`

# The Relational Algebra and Relational Calculus
## Relational Algebra Operation from Set Theory

交集，若有兩個Table `R(A1, A2, ... , An)`和`S(B1, B2, ... , Bn)`
包含 UNION、INTERSECTION、SET DIFFERENCE(也叫MINUS或EXCEPT)，皆為二元運算。  
- Relatioally Complete: 包含基本集合運算、select、projection。



## Relational Algebra Operations
### 0. ***Select***: $\ \sigma_{select\ condition}(R)$
- SQL CODE
```sql
select * from foobar where C1 and C2; #C1, C2為兩相異條件
```
- 選擇後的Column數量不變，Row數量改變。($deg不變$，但$card$改變。)
### 1. ***Projection***: $\ \pi_{attribute\ list}(R)$
- SQL CODE
```sql
select A, B, C from foobar; # A, B, C為三相異attribute
```
- 限制
    1. A, B, C需為`foobar`內所包含的attribute (column)。
    2. $deg\searrow$，但$card$不變。
### 2. ***基本集合運算***: (需Union compatible)
![](https://i.imgur.com/CGdiyHY.png)

#### a. ***Union***: $\ R_1\cup R_2$
- 限制
    1. Attribute的數量要對上 $\Longrightarrow deg(A) = deg(B)$
    2. 兩對應attribute的domain限制應該要相同, 
    i.e. $$V \in A\ and\  W \in B \Longrightarrow dom(V) = dom(W)$$
    3. $deg$不變，但$card\nearrow$。
    
#### b. ***Intersection***: $\ R_1 \cap R_2$
- 限制
    1. $C = A \cap B \Longrightarrow \forall t \in C,\ t\in A\ and\ t\in B$
    2. Attribute的限制也要對上。
    3. $deg$不變，但$card\searrow$。
 
#### c. ***Set difference***: $\ R_1 - R_2$

- 限制
    1. 需滿足Attribute的限制
    2. $deg$不變，但$card\searrow$。
- 解釋
Given $C = A - B$, 

    | A        | B        |  ->       |  C   |
    | -------- | -------- | ----------| ---- |
    |    X     |    X     |     ->    |   X  |
    |    X     |    O     |     ->    |   X  |
    |    O     |    X     |     ->    |   O  |
    |    O     |    O     |     ->    |   X  |


### 5. ***Cross product***: $A \times B$
卡氏積(只兩資料相乘)
deg(A x B)=deg(A)+deg(B)
card(A x B)=card(A)*card(B)

### 總體對照表(Join的種類) ###
![](https://i.imgur.com/1kXZOST.png)


### 6. ***Join***: $A \bowtie B$
deg(A ⋈ B)=deg(A)+deg(B)
0<=card(A ⋈ B)<=card(A)*card(B) 

是指將兩關聯表A與B依合併條件合併成一個新的關聯表R ，假設C為合併條件，以A⋈BC表示此合併運算。(有參與的放一起或沒參與的放一起，看題目要求)。

![](https://i.imgur.com/ZfEm1UN.png)

### 7. ***Outer join(s)***: $⟗, ⟕, ⟖$
join的相反，看6.反推
E⟗D(非ED條件的R)
outer join = join + 保留不符和
![](https://i.imgur.com/92rxUB1.jpg)

E⟕D(非E是D條件的R)
left join = join + 保留左不符合
![](https://i.imgur.com/rWhqvar.jpg)

E⟖D(是E非D條件的R)
right join = join + 保留右不符合
![](https://i.imgur.com/sqSorgR.jpg)

### 8. ***Division***: $A \div B$
R÷S 以第一個表格當被除數，以第二個表格當除數。 第一個關聯表格當作是「被除表」，第二個關聯表格當作是「除表」。此運算是在關聯表格 R中找出包含關聯表格S 中屬性值 的值組。
![](https://i.imgur.com/DmVyWrh.png)

### 9. ***Outer union(s)***:
把兩個完全不Union compatible的表格硬聯集在一起:
1. 取相異的attributes合成一個新表格。
2. 在原本沒有的屬性上補null。
