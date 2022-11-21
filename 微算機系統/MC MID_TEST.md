# MC MID_TEST

###### tags: `microcomputer` `note` `thu`
{%hackmd theme-dark %}

## Range
Chapter 2, 3, 4~BCD (不含)

## 特殊用途暫存器 (Program Status Word register)
![](https://i.imgur.com/RH43n3z.png)
MCS-51最大能一次能處理的資料是8bit，所以我猜每個暫存器應該也都是8 bit吧...?

### 1. Register Bank Select: `RS0`, `RS1`
用於指定暫存器庫：
![](https://i.imgur.com/S9IdWeb.png)

### 2. Carry flag : `CY`
`CY = 1` $\Rightarrow$ MSB有進位輸出或借位輸入。 
`CY = 0` $\Rightarrow$ 其它狀況。

### 3. Parity flag : `P`
數累積器內的數字有幾個bit為1:
`P = 1` $\Rightarrow$ 有奇數個。
`P = 0` $\Rightarrow$ 有偶數個。


### 4. Overflow flag : `OV`
`OV = 1` $\Rightarrow$ 進位輸入和進位輸出不相等時(跑到sign bit外去了)
`OV = 0` $\Rightarrow$ 進位都在數字的表示範圍之中(沒有溢位)

### 5. Auxiliary Carry flag : `AC`
`AC = 1` $\Rightarrow$ 從LSB(第0位)數過來第3位的bit到第4位的bit有進位的情形發生。
`AC = 0` $\Rightarrow$ 反之第3個bit就沒有進位。
這個flag主要被用在BCD的運算上。

### 6. Flag 0 : `F0`
主要是給使用者自行定義用的。

### Example 1
![](https://i.imgur.com/K5nACwA.png)
`CY`: 因為靠左的部份沒有進位，所以`CY = 0`。 
`P`: 因為有偶數個1，所以`P = 0`。
`AC`: 因為D3到D4有進位的情形，所以`AC = 1`。
`OV`: 因為Sign bit沒有發生進位的情形，因此`OV = 0`。

### Example 2
![](https://i.imgur.com/2nYJzgV.png)
`CY`: 因為靠左的部份沒有進位，所以`CY = 0`。 
`P`: 因為有奇數個1，所以`P = 1`。
`AC`: 因為D3到D4有進位的情形，所以`AC = 1`。
`OV`: 因為Sign bit沒有發生進位的情形，因此`OV = 0`。

## 指令格式和定址模式
![](https://i.imgur.com/J6s0TeK.png)
基本上就是opcode(運算碼) + 運算元，
然後依指令性質而變，運算元所需的數量也會改變。
 
而定址模式就是指令取得運算元的手段。
### 0. 隱含定址 ***Implied Addressing***
```assembly
RLA;
SWAPA;
```
這種的定址方式通常只會在特定的暫存器上做特定的運算，
因此也不需要再特地指定走址了。
### 1. 立即資料定址 ***Immediate Addressing***
```assembly
ADD A, #56H;
```
![](https://i.imgur.com/TZQraDb.png)
簡單來說就是直接把資料塞進本來應該放位址的位置。

### 2. 暫存器定址 ***Register Addressing***
```assembly
ADD A, R0;
```
![](https://i.imgur.com/JZpCsna.png)
這個是單運算元的暫存器定址，因為他的暫存器只用了3bit，只有辦法定址到8個暫存器。

### 3. 直接定址 ***Direct Addressing***
```assembly
ADD A, 34H;
```
![](https://i.imgur.com/aWf2rxN.png)
於opcode後的空間直接放位址的常數進去。
只是這個方法只能存取內部ram，而無法存取外部ram。





### 4. 絕對定址 ***Absolute Addressing***
```assembly
ACALL Label; // Label表示某個副程式的位置
```
![](https://i.imgur.com/2xqcN0K.png)

這個只會用在`ACALL`(Absolute Call)跟`AJMP`(Absolute Jump)上。
都是2 Byte的指令。

### 5. 長程定址 ***Long Addressing***
```assembly
LCALL SUB1; // SUB1表示某個副程式的位置
```
![](https://i.imgur.com/njfrOuH.png)

只會用在`LCALL`, `LJMP`上。這兩個都是3 Byte的指令。

### 6. (暫存器)間接定址 ***(Register)Indirect Addressing***
```assembly
ADD A, @R0;
```

![](https://i.imgur.com/7G8HToN.png)
把`R0`的資料取出來，當做地址來解讀，並到對應的位置取出資料。

### 7. (PC)相對定址 ***(PC-)Relative Addressing***
```assembly
JC CY_SET;
JNZ NOT_EQUAL; // 雙位元組指令
```
```assembly
CJNE A, #69H, NOT_EQ;
CJNE A, 32H, NOT_EQ; // 三位元組指令
```
![](https://i.imgur.com/DKrVXpn.png)
簡單來說就是:
1. 把位移量符號擴展(前面補8個1)。
2. 加上PC。
3. 得到新的PC該執行的位置。
![](https://i.imgur.com/kxYxDWG.png)
而三位元組的指令有兩個運算元，其中一個是由直接定址取得。
所以三位元組的版本其實算是直接定址+PC相對定址組合的產物。

### 8. 指標定址 ***Indexed Addressing***
```assembly
JMP @A + DPTR;
MOVC A, @A + PC;
```
![](https://i.imgur.com/hEktXaQ.png)

只有`JMP`跟`MOVC`可用。 
為合成定址的一種。Index由累積器A提供，Base則由PC或DPTR提供。
**Note**:
如果單純指合成定址的話，Index可由其它暫存器提供或是直接給定常數。Base則可由位址暫存器提供。


## 資料轉移、運算指令
### 內部資料轉移: `MOV`
![](https://i.imgur.com/du8r7XJ.png)
```assembly
MOV dst, src;
```
來源跟目的地可較隨意。
可使用直接定址、間接定址。
### 外部ram資料轉移: `MOVX` (X = external) 
![](https://i.imgur.com/wcZeCNP.png)

```assembly
MOVX A, @Ri; // 讀取
MOVX @Ri, A; // Ri = R0, R1
```
來源跟目的地只能經由累積器`A`來進行。
只能使用間接定址。(`Ri`可用`DPTR`代替以存取256byte以外的資料)
### 程式記憶器資料轉移: `MOVC`
![](https://i.imgur.com/OvoFVUg.png)
```assembly
MOVC A, @A + PC;
MOVC A, @A + DPTR;
``` 
只能讀取不能寫入。使用指標定址。
    
### 運算指令
![](https://i.imgur.com/tj7xDmJ.png)
- 精確制
  ![](https://i.imgur.com/u1q3s7t.png)
- 連結進位
        此為當要算雙精確度以上的資料時，需分成兩次算。 
        而中間的進位需要由CY來一起加進去，就是連結進位。
        e.g. `ADDC dst, src`，dst = dst + src + c，c為c_in(或是上一組運算的c_out)
- 單運算元指令
        e.g. `INC`、`DEC`、`CPL`(取1補數)。
![](https://i.imgur.com/cbflXvw.png)

* 乘法、除法
此處的乘法為無號數的乘法，
![](https://i.imgur.com/TbRcdd5.png)
![](https://i.imgur.com/JPa5bW3.png)
除法也是無號數的除法。
![](https://i.imgur.com/BesLQms.png)

### 清除
``` assembly
CLR C    ; 隱含定址
CLR A    ; 隱含定址

CLR ACC  ; 直接定址
CLR CY   ; 直接定址
```
計數一個位元組中，含有”1”位元的個數
![](https://i.imgur.com/8xk25zL.png)

程式例(利用副程式的方式計算一個位元組中含有1位元的個數)
![](https://i.imgur.com/ArTL0a2.png)
![](https://i.imgur.com/8ikdkt3.png)
巢路副程式
![](https://i.imgur.com/75a0FNK.png)
![](https://i.imgur.com/dzYtOBn.png)
![](https://i.imgur.com/4VIEoFp.png)

![](https://i.imgur.com/so3xtQ3.png)






## References
https://www.keil.com/support/man/docs/is51/is51_acall.htm