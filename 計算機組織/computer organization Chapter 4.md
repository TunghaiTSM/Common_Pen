###### tags: `computer organization` `note` `thu`
{%hackmd theme-dark %}

#  computer organization Chapter 4

## 需要的components
1.Program counter
2.Sign Extension Unit
3.Adder
4.Register
5.ALU
6.Data memory
7.Instruction memory

## Datapath
## ***1. R-type***
![](https://i.imgur.com/M1hyAtL.png)

RegDst=1，有rd。
RegWrite=1，有寫入暫存器。
ALUSrc=1，有做運算。
PCsrc=0，沒有跳躍。
MemRead=1，有讀取記憶體。
MemWrite=0，沒有寫入記憶體。
MemtoReg=0，沒有從記憶體寫入暫存器。
ALUOp=10，R-type專用。
ALU control=xxxx，根據指令。

## ***2. I-type***
- ### load 
![](https://i.imgur.com/AwQ0ELJ.png)

RegDst=0，無rd。
RegWrite=1，有寫入暫存器。
ALUSrc=1，有經過有號運算。
PCsrc=0，沒有跳躍。
MemRead=1，有讀取記憶體。
MemWrite=0，有寫入記憶體。
MemtoReg=1，有從記憶體寫入暫存器。
ALUOp=00，I-type專用。
ALU control=0010，I-type專用。

- ### store
![](https://i.imgur.com/K5QRYhQ.png)
RegDst=x，無rd。
RegWrite=0，沒有寫入暫存器。
ALUSrc=1，有經過有號擴充。
PCsrc=0，沒有跳躍。
MemRead=0，沒有讀取記憶體。
MemWrite=1，有寫入記憶體。
MemtoReg=x，沒有從記憶體寫入暫存器。
ALUOp=00，I-type專用。
ALU control=0010，I-type專用。

- ### branch on equal
![](https://i.imgur.com/WPMQ76y.png)
RegDst=x，無rd。
RegWrite=0，沒有寫入暫存器。
ALUSrc=0，有經過有號擴充。
PCsrc=1，if Zero=1，有跳躍。
MemRead=0，沒有讀取記憶體。
MemWrite=0，沒有寫入記憶體。
MemtoReg=x，沒有從記憶體寫入暫存器。
ALUOp=01，I-type專用。
ALU control=0010，I-type專用。


## ***3. J-type***
![](https://i.imgur.com/aJcNKOf.png)

## MIPS Pipeline stages

### IF：指令擷取

### ID：指令解碼

### EX：執行

### MEM：記憶體存取

### WB：寫回暫存器

## performance issue

### 公式：$$ ( Instruction\ count + ( Pipeline\ stage -1 ) ) \cdot colck\ cycle\ time $$ 

若IC有無限個，和無管線化比較快了( Pipeline stage )倍。

## Hazards

### Structure Hazard
硬體資源不足(只有一個memory)，導致兩個指令同時對同一個記憶體進行存取。
解決方式：
stall，導致管線出現bubble。

### Data Hazard
某一指令需要用到前面指令尚未產生的結果。
解決方式：
#### 1.Forwarding(bypassing)：不等到第一個指令將結果寫回，直接在第一個指令完成 Execution 時將結果傳送給第二個指令的 Execution Input 。
#### 2.Code Scheduling to Avoid Stalls：重排指令順序以避免stall。
若遇到load-use則不能使用Forwarding。

### Control Hazard
分支指令尚未決定是要否要跳躍至其他指令時，後面的指令已經進入管線。
解決方式：需提早決定是否要跳躍(在ID stage增加硬體)。








