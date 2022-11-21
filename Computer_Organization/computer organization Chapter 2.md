###### tags: `computer organization` `note` `thu`


# computer organization Chapter 2



## R-Type
![](https://i.imgur.com/XGbngkg.png)
### Addressing mode: ***Register addressing***
* 使用5 bit的資料來指定放資料的register (共三組)
* `shamt`: shift amount
* `funct`: function code (op code的延伸)
### 數值運算類
1. `add`, `addu` (unsigned) 
2. `sub`, `subu` (unsigned)
3. `mul` (沒有overflow), `mult`, `multu` (unsigned)
4. `div`, `divu` (unsigned)
### 邏輯/位元運算類
1. `and`, `or`, `nor`, `xor`
2. `sll`, `srl` (左移/右移)
3. `sllv`, `srlv` (使用register內的偏移量左移/右移)

### 流程控制類
1. `jr` (跳至register內的地址)
2. `slt` (把比大小的結果存起來) 

## I-Type
![](https://i.imgur.com/f0M5AgA.png)
### Addressing mode: ***Base addressing***
* `rs`裡的 base address + `constant or address`裡的offset
1. 資料存取類
    a. `sb`, `lb`, `lbu` (unsigned)
    b. `sh`, `lh`, `lhu` (unsigned)
    c. `sw`, `lw`, `lwu` (unsigned)

### Addressing mode: ***Immediate addressing***
* `constant or address` 直接放資料
1. 運算類
    a. `addi`, `addiu` (unsigned)
    b. `andi`, `ori`, `xori`,  
2. 資料存取類
    a. `lui` (載入upper 16 bit 的 immediate value) 

### Addressing mode: ***PC-relative addressing***
* `PC`(program counter) + `constant or address`
1. 流程控制類 (branch on...)
    a. `beq`, `bne` ($=$ / $\neq$)
    b. `bgtz`, `bgez` ($>0$ / $\geq 0$)
    c. `bltz`, `blez` ($<0$ / $\leq 0$)
    

## J-Type
![](https://i.imgur.com/c2xSoqS.png)
### Addressing mode: ***Pseudodirect addressing***
* (幾乎)直接存取address內的address
* 因為MIPS的架構下，記憶體為32bit
* 但26bit是不夠拿來直接定址的
* 因此我們使用PC裡比較高的4bit加上最後的兩個0
* 就可以進行直接定址了(因為MIPS的指令都為4byte)

1. 流程控制類
    a. `j`, `jal`


## Pseudo Instruction
* 無此指令，但可用別的指令組合而成
1. 流程控制類 (branch on...)
    a. `bgt`, `bge` ($>$ / $\geq$)
    b. `blt`, `ble` ($<$ / $\leq$)
2. 資料移動
    a. `move $t0, $t1` -> `add $t0, $zero, $t1`








## Register 對應的編號
![](https://i.imgur.com/IFuWfBA.png)

## 參考資料
https://www.d.umn.edu/~gshute/mips/rtype.xhtml
https://www.d.umn.edu/~gshute/mips/itype.xhtml
https://www.dsi.unive.it/~gasparetto/materials/MIPS_Instruction_Set.pdf
https://rmd.ac.in/dept/ece/Supporting_Online_%20Materials/5/CAO/unit2.pdf
https://phoenix.goucher.edu/~kelliher/f2009/cs220/mipsir.html
