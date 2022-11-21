###### tags: `Algorithm` `test` `thu`
# CH6(施工中)


## Exercise
 
### 6.1-1
### What are the minimum and maximum numbers of elements in a heap of height h?

minimum = $$ 2^h $$
maximum = $$ 2\cdot 2^h -1 $$

### 6.1-2
### Show that an n-element heap has height $\lfloor lgn \rfloor$.

設$n=2^m-1+k$，m+1為heap高度，k為額外可能有的leaf。root到leaf的最長的simple path，也要等於m，所以可得 $m=\lfloor lgn \rfloor$

https://math.stackexchange.com/questions/874170/show-that-the-height-of-the-heap-is-lfloor-lg-n-rfloor

假設高度height=k

n最小的情況為$$ 2^k  $$n最大的情況為$$ 2\cdot 2^k -1 $$
因此
$$ 2^k \le n \le 2\cdot2^k-1<2\cdot2^k   $$
$$ 2^k \le n <2\cdot2^k   $$
$$k \le lgn < k+1 $$
$$lgn = k+a $$
$$0\le a <1 $$
$$ k = \lfloor lgn \rfloor$$
### 6.1-3
### Show that in any subtree of a max-heap, the root of the subtree contains the largest value occurring anywhere in that subtree.

若有一個子樹的最大元素不在root，且他的parent在子樹內，那他的最大元樹會大於parent，違反的heap的定理。

### 6.1-4
### Where in a max-heap might the smallest element reside, assuming that all elements are distinct?

最小的元素會出現在leaf。若x是最小元素但不是leaf，y是x的child，根據heap的性質，y會小於x或等於x，違反了前提。

### 6.1-6
### Is an array that is in sorted order a min-heap?

是的。

### 6.1-7
### Is the array with values `23, 17, 14, 6, 13, 10, 1, 5, 7, 12` a max-heap?

不是。
![](https://i.imgur.com/gguK4AO.png)
第9個元素大於第四個，不符合max-heap之性質。

### 6.1-8
### Show that, with the array representation for storing an n-element heap, the leaves are the nodes indexed by $\lfloor n/2 \rfloor + 1$，$\lfloor n/2 \rfloor + 2$， ... ， n.

若有一個元素i在leaf裡，而i有兩個child，$2\cdot i$和$2\cdot i +1$，他們會大於$2\cdot\lfloor n/2 \rfloor + 2$且不在上面的數列裡。所以我們應該假設i沒有child，$2\cdot i$和$2\cdot i +1$皆大於n，i大於$n/2$，i就會屬於這個數列。

最後一個不是leaf的node會出現在哪裡,在$\lfloor n/2 \rfloor$
所以$\lfloor n/2 \rfloor$+1 ~n都是leaf

### 6.2-1
### Using Figure 6.2 as a model, illustrate the operation of MAX-HEAPIFY(A, 3) on the array A = {27, 17, 3, 16, 13, 10, 1, 5, 7, 12, 4, 8, 9, 0}


| 27 | 17 | 3  | 16 | 13 | 10 | 1  | 5  | 7  | 12  | 4  | 8  | 9  | 0  |
|----|----|----|----|----|----|----|----|----|-----|----|----|----|----|
| 27 | 17 | 10 | 16 | 13 | 3  | 1  | 5  | 7  | 12  | 4  | 8  | 9  | 0  |
| 27 | 17 | 10 | 16 | 13 | 9  | 1  | 5  | 7  | 12  | 4  | 8  | 3  | 0  |

### 6.2-2
### Starting with the procedure MAX-HEAPIFY, write pseudocode for the procedure MIN-HEAPIFY(A, i), which performs the corresponding manipulation on a min-heap.How does the running time of MIN-HEAPIFY compare to that of MAX-HEAPIFY?
```cpp=
void min_heapify(vector<int> &vec, int i){
    int l = left(i);
    int r = right(i);
    int smallest = 0;
    if(l < vec.size() && vec[l] < vec[i]){
        smallest = l;
    }
    else{
        smallest = i;
    }
    if(r < vec.size() && vec[r] < vec[smallest]){
        smallest = r;
    }
    if(smallest != i){
        int tmp = vec[i];
        vec[i] = vec[smallest];
        vec[smallest] = tmp;
        max_heapify(vec, smallest);
    }
}
```
有bug求救
There is no difference in running time between MAX-HEAPIFY and MIN-HEAPIFY.

### 6.2-4
### What is the effect of calling MAX-HEAPIFY(A, i)when the element A[i] is larger than its children?
不會變動。

### 6.2-5
### What is the effect of calling MAX-HEAPIFY(A, i) for$i > A.heap-size/2$ ?
i不會有child，演算法不會有動作。

### 6.2-6
### The code for MAX-HEAPIFY is quite efficient in terms of constant factors, except possibly for the recursive call in line 10, which might cause some compilers to produce in efficient code. Write an efficient MAX-HEAPIFY that uses an iterative control construct (a loop) instead of recursion.
```cpp=
void max_heapify2(vector<int> &vec, int i){
    while(i <= vec.size()){
        int l = left(i);
        int r = right(i);
        int largest = 0;
        if(l <= vec.size() && vec[l] > vec[i]){
            largest = l;
        }
        else{
            largest = i;
        }
        if(r <= vec.size() && vec[r] > vec[largest]){
            largest = r;
        }
        if(largest != i){
            int tmp = vec[i];
            vec[i] = vec[largest];
            vec[largest] = tmp;
            i = largest;
        }
        else{
            break;
        }
    }
}
```


### 6.2-7
### Show that the worst-case running time of MAX-HEAPIFY on a heap of size n is $\Omega(lgn)$. (Hint: For a heap with n nodes, give node values that cause MAX-HEAPIFY to be called recursively at every node on a simple path from the root down to a leaf.)
最小的元素出現在root時。他一路換到leaf需要移動$\lfloor lgn \rfloor$(heap的高度)次，所以$\Omega(lgn)$就是MAX-HEAPIFY的worst-case。

### 6.3-1
### Using Figure 6.4 as a model,illustrate the operation of BUILD-MAX-HEAP on the array A = {5,3,17,10,84,19,6,22,9}.
| 5 | 3 | 17 | 10 | 84 | 19 | 6 | 22 | 9 |
|---|---|----|----|----|----|---|----|---|
| 5 | 3 | 17 | 22 | 84 | 19 | 6 | 10 | 9 |
| 5 | 3 | 19 | 22 | 84 | 17 | 6 | 10 | 9 |
| 5 | 84 | 19 | 22 | 3 | 17 | 6 | 10 | 9 |
| 84 | 5 | 19 | 22 | 3 | 17 | 6 | 10 | 9 |
| 84 | 22 | 19 | 5 | 3 | 17 | 6 | 10 | 9 |
| 84 | 22 | 19 | 10 | 3 | 17 | 6 | 5 | 9 |

### 6.3-2
### Show that $\lceil n/2\cdot2^h\rceil \ge1/2$ for $0\le h \le \lfloor lgn \rfloor$
$proof.$
- 我不會
$$h = \lfloor lgn \rfloor$$
$$2\cdot2^h = 2 \cdot 2^ (lgn) = 2 \cdot n$$
$$\lceil n/2\cdot2^h\rceil = \lceil n/2n\rceil = \lceil1/2 \rceil = 1$$
### 6.3-3
### Why does the loop index i in line 2 of BUILD-MAX-HEAP decrease from $\lfloor n/2 \rfloor$ to 1 rather than increase from 1 to $\lfloor n/2 \rfloor$
increase from 1 to $\lfloor n/2 \rfloor$ 如果最大值在leaf可能到不了root

### 6.3-4
### Show that there are at most $\lceil n/(2\cdot2^h )\rceil$ nodes of height $h$ in any n-element heap.
![](https://i.imgur.com/hjedsMv.jpg)

### 6.4-1
### Using Figure 6.4 as a model,illustrate the operation of HEAPSORT on the array A = {5,13,2,25,7,17,20,8,4}
![](https://i.imgur.com/HCEh4cU.png)


### 6.4-2
### Argue the correctness of HEAPSORT using the following loop invariant:
### At the start of each iteration of the for loop of lines 2–5, the subarray $A[1\ldots i]$ is a max-heap containing the i smallest elements of $A[1 \ldots n]$, and the subarray $A[i+1 \ldots n]$ contains the $n-i$ largest elements of A[1...n],sorted.



### 6.4-3
### 

### 6.4-4
###

### 6.4-5
###

### 參考資料:
https://sites.math.rutgers.edu/~ajl213/CLRS/CLRS.html




