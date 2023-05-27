#数据结构（C语言版）----浙江大学

![image-20220918152504610](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220918152504610.png)

空间如何分配？类别分多细。

常见的数据结构：

- 线性表，还可细分为顺序表、链表、栈和队列；
- 树结构，包括普通树，二叉树，线索二叉树等；
- 图存储结构

### 1.1.2空间的使用

写一个PrintN函数，顺序输出正整数1-N。递归实现（不如循环好，占用内存太大）

```c
viod PrintN( int N )
{ if (N)
	{
	PrintN(N-1);
    printf("%d\n",N);
	}
 	return;
}
```

### 1.1.3关于算法效率

![image-20220918154748973](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220918154748973.png)

```cpp
double f(int n, double a[], double x)
{
    int i;
    double p = a[n];
    for (i=n;i>0;i--)
        p = a[i-1]+x*p;
    return p; 
}
```

调用时钟打点函数：

```c
#include<stdio.h>
clock_t start,stop;//相当于一个数据类型
double duration;
int main()
{
    start = clock();
    MyFunction();
    stop = clock();
    duration = ((double)(stop-start))/CLK_TCK;
    return 0;
}

```

### 1.1.4抽象数据类型

**数据**：能够用计算机程序处理的符合：声音，图像

**数据元素**：是数据的基本单位，数据元素可以由多个数据项组成，数据项是最小的单元。（书-数据元素，书本中的书名-数据项）

**数据对象**：性质相同的数据元素的集合 

**数据结构**：数据对象在计算机中的组织方式（是互相之间存在一种或多种特定关系的数据元素的集合）

- 逻辑结构（数据元素之间的逻辑关系）—— 线性、树
- 物理存储结构

数据对象必定与一系列加在其上的操作相关联

完成这些操作所用的方法就是算法

**数据之间的关系：结构**：四种结构：

- 集合
- 线性结构
- 树形结构
- 图状结构（网状结构）

![image-20220918165421583](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220918165421583.png)

矩阵（Matrix），对于矩阵M*N的描述用<a,i,j>。

**数据类型**：出现在高级语言中，用于刻画操作对象的特性

- 非结构的**原子类型**：不可分解，类似于实型、整型、指针型、空型。
- **结构类型**：
- **抽象数据类型**：
- 

### 1.2.1算法的定义

 **算法**（Algorithm）：是对于特定问题求解步骤的一种描述，一个有限指令集，接受一些输入（有些情况下不需要输入），产生输出，在有限步骤后种植，

5个特性：

![image-20220919145607036](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220919145607036.png)

 

### 1.2.2什么是好的算法

算法好坏的定义：

空间复杂度S（n）——根据算法写成的程序再执行时占用存储单元的长度。这个长度与输入数据的规模有关。	

时间复杂度T（n）：——根据算法写成的程序在执行时耗费时间的长度



递归时占用的内存（10000）就占用了10000块空间。

机器做乘除法的时间比较久，所以算法要尽量减少乘除法。

![image-20220919152028353](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220919152028353.png)

==一般分析最坏情况复杂度：T ~worst~==

### 1.2.3复杂度的渐进表示法

![image-20220919152747043](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220919152747043.png)

T（n）=O（f（n）），表示T（n）有一个上界（找最小上界）

T（n）=Ω（g（n）），表示T（n）有一个下界（找最大下界）

T（n）=Θ（g（n）），表示T（n）同时有一个上下界



不同计算的复杂度情况

![image-20220919153307814](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220919153307814.png)

两个算法的的复杂度：

若两个算法相加，则复杂度为两者复杂度中的大者。若两个算法相乘，则复杂度为两个算法复杂度乘积。

![image-20220919153606469](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220919153606469.png)

==for循环程序是相乘，if-else程序是选最大（相加）==

### 1.3.1应用实例，算法1和2

 暴力求解法：三重循环，把每个子序列都加出来之后比较大小

![image-20220919160331899](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220919160331899.png)

 

算法2：在每次累加后面加一个A[j]减少了一次复杂度

![image-20220919160422133](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220919160422133.png)



***一般编写一个程序时，复杂度若为O（n²），会下意识的把其复杂度改为O（nlog（n））***

### 1.3.2算法3

分而治之的算法：

一直对半分，对半分，然后左右相加。

 ![image-20220919163226540](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220919163226540.png)

### 1.3.3算法4（在线处理最优算法）

![image-20220919163800728](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220919163800728.png)

N/A：Not Available OR Not Applicable. 直译是无从得知或不适 用。

![image-20220919170752444](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220919170752444.png)



### 2.1.1引子：多项式表示

线性机构，线性表。

利用顺序存储结构表示非零项：

非零项a~i~x^i^表示的是系数和指数，可以将应该多项式看成一个（a~i~,^i^）的组合 。

![image-20220922135806077](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220922135806077.png)

指数大小有序存储，两项相加看对应项的指数级别项进行相加。



方法3：链表结构存储非零项：

![image-20220922140636586](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220922140636586.png)

```c
typedef struct PolyNode *Polynominal;
struct PolyNode{
    int coef;//定义系数
    intexpon;//定义指数
    Polynominal link;//定义指针
}
```



### 2.1.2线性表及其顺序存储

==同一个问题可以有不同的（存储）方法==

- 数组存储
- 链表存储

**线性表（List）：**是由同类数组元素构成的有序序列的线性结构。

线性表L∈List，元素X∈ElemenType（elemen元素）

```c
List MakeEmpty(): //初始化一个空线性表
ElementType FindKth(int K,List L)://根据位序K，返回相应元素
int Find(ElementType X,List L)://在线性表L中查找X的第一次出现位置
```

![image-20220922142718215](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220922142718215.png)

以及更多见书本19页。

线性表的顺序存储实现：

![image-20220922143309514](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220922143309514.png)

初始化建立空的顺序表：

```c
List MakeEmpty()
{
    List Ptrl;
    Ptrl = (List)malloc(sizeof(struct LNode));
    PtrL->Last = -1;
    return Ptrl;
}
```

C语言中malloc是动态内存分配函数，C++中使用new关键字

如果分配成功则返回指向被[分配内存](https://www.baidu.com/s?wd=分配内存&tn=44039180_cpr&fenlei=mv6quAkxTZn0IZRqIHckPjm4nH00T1Y3nhmsm103mHbLm1Fbnh7W0ZwV5Hcvrjm3rH6sPfKWUMw85HfYnjn4nH6sgvPsT6KdThsqpZwYTjCEQLGCpyw9Uz4Bmy-bIi4WUvYETgN-TLwGUv3En1c1Pj0LnjT1)的指针(此存储区中的初始值不确定)，否则返回空指针NULL。

```c
#include<stdio.h>  
#include<malloc.h>  
int main()  
{  
    char *p;  
   
    p=(char *)malloc(100);  
    if(p)  
        printf("Memory Allocated at: %x/n",p);  
    else  
        printf("Not Enough Memory!/n");  
    free(p);  
    return 0;  
}  
```

malloc和new的不同：

　从函数声明上可以看出。malloc 和 new 至少有两个不同: ***new 返回指定类型的指针，并且可以自动计算所需要大小。***比如：

   int *p;

　　p = new int; //返回类型为int* 类型(整数型指针)，分配大小为 sizeof(int);

　　或：

　　int* parr;

　　parr = new int [100]; //返回类型为 int* 类型(整数型指针)，分配大小为 sizeof(int) * 100;

　

　  ***而 malloc 则必须由我们计算要字节数，并且在返回后强行转换为实际类型的指针。***

  　int* p;

　　p = (int *) malloc (sizeof(int));

malloc需要强制转换类型，自己指定大小。

### 2.1.3顺序存储的插入和删除

插入：在第：i（1<i<n+1）个位置上插入一个值为X的新元素。

那么这个新元素要插入在i-1和i之间。

那么首先需要**先移动再插入**：防止数据覆盖

插入操作具体实现：

p->Next，代表的是p那个结点的指针域

![image-20220922150746345](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220922150746345.png)

删除：

![image-20220922151000550](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220922151000550.png)****

### 2.1.4 链式存储及查找

 线性表的链式存储实现：

求表长：

```c
int Length(List PtrL)
{
    List p=PtrL;//目前p指向表的第一个结点
    int j = 0;
    while(p){
        p = p->Next;
        j++;
    }
    return j;
}
```

查找Find：

![image-20220922153602713](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220922153602713.png)

### 2.1.5链式存储的插入和删除

![image-20220922154119579](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220922154119579.png)

顺序不能交换：先指下一个，再值前一个

```c
s->Next = p->Next;
p->Next = s;
```

插入操作的具体实现L:

```c
List Insert(ElementTyper X,int i,List Ptrl)
{
    List p,s;
    if(i == 1)
    {
        s= (List)malloc(sizeof(struct LNode));
        s->Data = X;
        s->Next = PtrL;/*申请新结点插入在表头*/
        return s;
    }
    p = FindKth(i-1,PtrL);
    if (p ==NULL){
        printf("参数错误");
        return NULL;
    }
    else{
        s= (List)malloc(sizeof(struct LNode));
        s->Data = X;
        S->Next = p->Next;
        p->Next = s;
        return PtrL;
    }
}
```

删除结点：

删除结点之前要把删除结点那块内存free（）掉。

![image-20220922155928642](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220922155928642.png)

要记得释放s

### 2.1.6广义表和多重链表

![image-20220922161734808](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220922161734808.png)

广义表是线性表的推广。

对于线性表而言，n个元素基本都是单元素

但是对于广义表来说：这些元素不仅仅是单元素，也可以是另外一个广义表。

![image-20220922162017665](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220922162017665.png)

通过Tag来判断下面的位置是Data还是SubList



多重链表：链表中的节点可能同时隶属于多个链

结点的指针域会有多个。

但是**包含两个指针域的链表并不一定是多重链表**，比如双向链表就不是多重链表。



十字链表：（多重链表来表示稀疏矩阵）

![image-20220922163531490](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220922163531490.png)

![image-20220922163811566](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220922163811566.png)

利用一个union来将Term和Head两种结构何在一起。

### 2.2.1什么是堆栈

堆栈也是一种顺序结构，特殊的顺序表。

有关后缀表达式：

![image-20220924133721500](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924133721500.png)

举个例子：6 2 / 3 - 4 2 * + = ？

先6 2 ，然后除，变3，然后 3 3，遇到-，变成3-3，0，然后0 4 2×，变成0 8， 然后0 8 +，相当于最后变成8。

**最近两个数的两个数进行运算**

先放进去的后拿出来，后放进去的先拿出来，这样的数据存储结构称为**堆栈**。

**堆栈（stack）：**具有一定操作约束的线性表

只在一端（栈顶，Top）做插入和删除

- 插入数据：入栈（Push）
- 删除数据：出栈（Pop）
- 后入先出：Last In First Out（LIFO）

操作集：长为MaxSize的堆栈S∈Stack，堆栈元素item∈ElementType

最常用的堆栈基础操作：

1. void Push（Stack S，ElementType item）：//将数据item压入堆栈中
2. ElementType Pop(Stack S): //删除并返回栈顶元素

![image-20220924135851602](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924135851602.png)

进去ABC，出来CBA，可以利用交替push和pop来改变顺序 

有一个公式可以计算顺序入堆栈后出栈的情况：叫卡塔兰数：

![image-20220924140754110](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924140754110.png)

所以当n=4时，有14种出栈形式。

### 2.2.2堆栈的顺序存储实现

用C语言描述栈类型Stack如下：

```c
#define Maxsize
typedef struct SNode *Stack;
struct SNode{
    ElementType Data[Maxsize];
    int Top;
}
```



当Top指向-1时，表示空栈；Top指向Maxsize-1时表示满栈。最下面是0，最上面是Maxsize。

入栈操作：

![image-20220924142128028](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924142128028.png)



当两个堆栈一起的时候，可以项中间生长：

![image-20220924142702895](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924142702895.png)

当两个堆栈Top指针相遇时，表示两个栈都满了。最大地利用了数组空间。

双堆栈的结构比标准堆栈多了一个栈顶指针：

初始化两个堆栈Top指针时：Top1=-1，Top2=Maxsize。

![image-20220924142833925](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924142833925.png)

### 2.2.3堆栈的链式存储实现：

用链表实现堆栈： 栈的链式存储结构实际上是一个单链表，叫做链栈。插入和删除操作只能在链栈的栈顶进行。TOP指针

![image-20220924143704774](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924143704774.png)

  

![image-20220924143843052](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924143843052.png)

头指针里面是没有元素的，从头指针向后第一个结点内才有元素。

用数组插入数据的时候要判断满不满。但是用链表的时候是动态申请结点的，所以不需要考虑满不满，满了继续申请结点就可以。

![image-20220924145203026](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924145203026.png)

### 2.2.4堆栈的应用：表达式求值

将中缀转换为后缀表达式，之后进行求值：

![image-20220924150448209](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924150448209.png)

一个一个输入堆栈当中，遇到运算复杂度高的就要放进去，低的拿出来。

![image-20220924150744709](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924150744709.png)

整体流程：

![image-20220924150813864](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924150813864.png)

高进低拿，一拿拿所有。



堆栈的应用：

- 函数调用及递归实现
- 深度优先搜素
- 回溯算法

 

### 2.3.1队列及顺序存储实现

队列（Queue）：具有一定操作约束的线性表

插入和删除：只能在一端插入，而在另一端删除。 

先进先出（FIFO），入队列（AddQ），出队列（DeleteQ）

![image-20220924153350697](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924153350697.png)

顺序队列需要两个变量进行存储：front和rear（队尾）

 判断队列空满是根据Front和Rear的相对差值（n种情况）进行判别的。 

对于Rear和Front之间的差距最多只有n种情况，但是队列元素的个数总共有n+1种情况，没办法区分

**解决方法**：让n长的队列只排n-1个数



使用循环队列结构进行

![image-20220924154713600](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924154713600.png)

用求余操作来看队列是不是满了

### 2.3.2 对于列的链式存储实现

队列存储也可以用单链表来表示。但是==队列的头（Front）必须指向头节点（因为头要删除），队列的尾（Rear）要指向尾结点（尾巴删的话找不到前一个元素）==

###2.4多项式的加减运算实现

计算机中可以用单向链表来实现：两个值：系数和指数还有下一个结点的指针。

![image-20220924160820722](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924160820722.png)

如何相加：

 ![image-20220924161602969](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924161602969.png)

Attach函数的实现：

![image-20220924161822108](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924161822108.png)

读入多项式：

![image-20220924164521640](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220924164521640.png)

P24-26重新看一看，跟着写一遍。





### 3.1.1引子（顺序查找）-3.1.3（二分查找实现）

  分层次的管理具有更高的效率

数据管理基本操作：

**查找**：

- 静态查找：集合中记录是固定的，没有插入和删除操作，只有查找

顺序查找：通过建立哨兵，来判断是非到了数组的边缘，哨兵位于数组的0位置，K就是你要找的那个值。

```c
int SequentialSearch(List Tbl, ElementType K)//结构的指针，里面包含元素值和，数组的大小。
{
    int i;
    Tbl->Element[0] = K;
    for(i = Tbl->Length;Tbl->Element[i]!=K;i--)
    return i;
}
```

时间复杂度O(n)



二分查找：两个条件：==连续存放的数组==才可以进行二分查找

 ```c
 //二分法的算法：
 int BinarySearch(List Tbl,ElementType K)
 {
     int left,right,mid,NotFound=-1;
     left = 1;
     right = Tbl->Length;
     while(left<=right)
     {
         mid = (left+right)/2;
         if(K<Tbl->Element[mid])
             right = mid-1;
         else if(K>Tbl->Element[mid]) 
             left=mid+1;
         else
             return mid;
     }
     return NotFound;
     }
 }
 ```

时间复杂度O（LogN）

![image-20220925184330136](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220925184330136.png)

![image-20220925184429883](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220925184429883.png)

二分查找判断树：

判定树上每个结点需要查找次数刚好尾该结点层数

查找成功的次数不会超过判定树的深度

n个结点的判定树的深度为log~2~n+1,平均正确查找次数（ASL）=`(4*4+4*3+2*2+1)/11=3`

- 动态查找：集合中记录是动态变化的，除了查找还可以出现插入和删除

### 3.1.4树的定义和术语

![image-20220925185934557](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220925185934557.png)

树的特点：

- 子树是不相交的；

- 除了根节点之外，每个结点有且仅有一个父节点；

- 一棵N个结点的树有N-1条边

![image-20220925190616297](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220925190616297.png)

![image-20220925190758437](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220925190758437.png)

### 3.1.5树的表示

 ![image-20220925191431133](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220925191431133.png)

二叉树：

![image-20220925191512337](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220925191512337.png)

每个点只有两个指针域。

### 3.2.1二叉树的定义和性质

 二叉树T：一个有穷结点的集合，这个集合可以为空。

二叉树有左右之分。

5种形态：见书本P106。

 三种特殊的二叉树：

![image-20220926162115841](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220926162115841.png)

完美二叉树表示的是每个结点下面都有两个结点。

**完全二叉树：**有n个结点的二叉树，对树中结点按从上至下、从左到右的顺序进行编号，编号为i的结点必须和满二叉树中位置相同。

![image-20220926162416734](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220926162416734.png)

不是完全二叉树的例子：

![image-20220926162435062](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220926162435062.png)

显然，一棵完美二叉树必定是一棵完全二叉树。有N个结点的完全二叉树的深度为O（logN）。

二叉树的重要性质：

![image-20220926163414455](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220926163414455.png)

n0=n2+1，n0是没有下面分支的结点数，n1是有一个边，n2是两个边。

![image-20220926163554040](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220926163554040.png)

以上为遍历方法。

### 3.2.2二叉树的存储结构

1.顺序存储结构：

适用于完全二叉树：从上至下、从左到右顺序存储n个结点的完全二叉树的结点。（数组存储）

-  非根节点（序号i>1）的父节点的序号是不大于i/2的最大整数。
- 结点（i）的左孩结点的序号是2i，右孩结点的序号是2i+1（若2i<=n/2i+1<=n，则没有左/右孩子）

一般的二叉树也可以用这种数组的结构来存储，但是会造成空间的浪费，就是把别的结点补齐。

2.链表存储：

![image-20220926183757860](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220926183757860.png)

### 3.3.1先序中序后序遍历

1. 先序遍历：先访问根节点，先序遍历其左子树，先序遍历其右子树。

   统一都是先访问左子树，然后再访问右子树

```c
void PreOrderTraversal(BinTree BT)
{
    if(BT){
        printf("%d",BT->Data);
        PreOrderTraversal(BT->Left);
        PreOrderTraversal(BT->Right);
    }
}
```

![image-20220926185229238](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220926185229238.png)

2.中序遍历：中序遍历其左子树，中访问根节点，先序遍历其右子树。

```c
void PreOrderTraversal(BinTree BT)
{
    if(BT){
        PreOrderTraversal(BT-Left);
        printf("%d",BT->Data);
        PreOrderTraversal(BT-Right);
    }
}
```

![image-20220926185443915](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220926185443915.png)

都先左再中间再右。每一个小树的根节点都要最后访问。

3.后序遍历：后序遍历其左子树，后序遍历其右子树，先访问根节点。

 ![image-20220926190041060](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220926190041060.png)



先中后序的判断方法：

![image-20220926190225589](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220926190225589.png)

递归的实质还是使用了堆栈

### 3.3.2中序非递归遍历

 ![image-20220926191306707](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220926191306707.png)

```c
void InOrderTraversal(BinTree BT)
{
    BinTree T=BT;//指向根节点
    Stack S = CreatStack(MaxSize);//初始化堆栈S
    while(T || !IsEmpty(S))
    {
        while(T){
        	Push(S,T);
        	T = T->Left；
        }		}
    	if(!IsEmpty(S))
    	{ 
        	T = Pop(S);//结点弹出堆栈
        	printf("%5d",T->Data);//
        	T = T->Right;//转向右子树
    	}
}
```

先序非递归：

把下面`printf("%5d",T->Data);//`，挪到上面的push后面。



后序有点复杂，算了。

### 3.3.3层序遍历

![image-20220926193713020](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220926193713020.png)

抛出一个结点赋给T,把左右儿子都放到结点里去。

### 3.3.4遍历应用的例子

叶子结点：就是没有儿子的结点

算法就是在前序遍历前面加一个判断

```c
if(BT){
    if(!BT->Left && !BT->Right)
        printf("%d",BT->Data);
}
```

**求二叉树的高度**：

![image-20220926195353400](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220926195353400.png)

二元运算表达式树及其遍历：

![image-20220926195600079](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220926195600079.png)

由两种遍历序列确定二叉树：必须包含中序遍历才可以唯一确定。没有中序（仅前后序）不行。

### P41树的同构1：

 同构：给定两棵树T1和T2，如果T1可以通过若干次左右孩子互换就变成T2，则我们称两棵树是“同构”的

![image-20220927154451653](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220927154451653.png)

数组表示二叉树的方法就是把这棵树看成一个完全二叉树

结构数组表示二叉树：静态链表

```c
#define MaxTree 10
#define ElementType char
#define Tree int
#define Null -1//代表-1，与大写NULL区别
struct TreeNode
{
    ElementType Element;
    Tree Left;
    Tree Right;
}T1[MaxTree],T2[MaxTree];
```

链表就是有Left和Right两个指针。

### P42

创建二叉树代码：

第一个输入值是结点数，如何寻找到根结点的位置。

一开始设置一个数组check[]，将其初值都设为0，找到结点中每个位置，如果有人指向它则设成1，没有人指向设为Null（-1），最后会留下一个唯一一个0，因为没有人指向，所以这个点就是根结点。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220927160148545.png" alt="image-20220927160148545" style="zoom:50%;" />

 如何判断两个数是否同构：

 ### 4.1二叉搜素数及查找

查找问题分两种：

- 静态查找（按照二分查找）
- 动态查找

把数据直接放树当中，方便插入删除和动态存储

**二叉搜素树（Binary Search Tree，BST）也称二叉排序树或者二叉查找树：**

![image-20220929143437461](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220929143437461.png)

递归效率较低，使用循环来做，根据二叉搜素树的性质可以知道，最左端是最小值，最右端是最大值。

寻找最大元素的迭代函数：

```c
Position FindMax(BinTree BST)
{
    if(BST)//如果非空
        while(BST->Right) BST=BST->Right;
    return BST;
}
```

### 4.1.2二叉搜素树的插入

递归实现

```c
BinTree Insert(BinTree BST, ElementType X)
{
    if(!BST){
        BST = (BinTree)malloc(sizeof(struct TNode));
        BST->Data = X;
        BST->Left = BST->Right =NULL;
    }
    else{
        if(X<BST->Data)
            BST->Left = Insert(BST->Left,X);
        if(X>BST->Data)
            BST->Right = Insert(BST->RightX);
    }
    return BST;
}
```

### 4.1.3二叉搜素树的删除

有三种删除的情况，只说一种最复杂的。

删除的结点有左、右两棵子树：要用另外一个结点代替呗删除的结点：

- 取右子树中最小元素
- 或者取左子树中最大元素

### 4.2.1什么是平衡二叉树

搜索树结点不同插入次序，将导致不同的深度和平均查找长度ASL。

平衡因子（Balance  Factor，BF）：BF（T）=hL-hR（左树高度-右树高度）

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220929153457033.png" alt="image-20220929153457033" style="zoom:50%;" />

必须！每一个！结点的左右子树的平衡因子绝对值不超过1

节点数最小：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220929153812926.png" alt="image-20220929153812926" style="zoom:50%;" />

 最少结点数：n~h~=n~h-1~+n~h-2~+1，高度为h

==给定结点数为n的AVL数的最大高度为h=O（log~2~n）==

与斐波那契数列的关系为n~h~=F~h+2~-1

### 4.2.2平衡二叉树的调整

如果多个结点被破坏，考虑最下面那个就可以。

RR旋转（右单旋）：麻烦结点再发现者的右子树的右边。（逆时针转）

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220929161633998.png" alt="image-20220929161633998" style="zoom:50%;" />

 LL旋转：和上面同理相反（顺时针转 ）

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220929162038539.png" alt="image-20220929162038539" style="zoom:50%;" />

**LR旋转**：麻烦结点再左子树的右边

![image-20220929162739696](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220929162739696.png)

**RL旋转**

![image-20220929162942619](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220929162942619.png)

有点看不懂：[(4条消息) 平衡二叉树（树的旋转）_清塘荷韵_kathy的博客-CSDN博客_rl左右](https://blog.csdn.net/qq_24336773/article/details/81712866)

简单一点：

<img src="https://img-blog.csdn.net/20150818221513880" alt="img" style="zoom: 50%;" />

<img src="https://img-blog.csdn.net/20150818220942825" alt="img" style="zoom:50%;" />

LR调整：由于在A的左孩子(L)的右子树(R)上插入新结点，使原来平衡二叉树变得不平衡，此时A的平衡因子由1变为2

![img](https://img-blog.csdn.net/20150818224419149)

同理：

![img](https://img-blog.csdn.net/20150818230041580)

### 48-50判断是否同一棵树

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220929171209576.png" alt="image-20220929171209576" style="zoom:50%;" />

flag是用来判别一个序列是否被访问过。

 

1. 如何建立搜索树：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220929171647670.png" alt="image-20220929171647670" style="zoom:80%;" />

1. 如何判别

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220929184301962.png" alt="image-20220929184301962" style="zoom:67%;" />  

P48-50有点懵，有空重新看一看。

### 5.1.1什么是堆

不是堆栈，堆栈是先进后出那个。与队列也不同，队列是没有特权的，要先来的先处理。

**堆**：通常被称之为**优先队列**，是一种特殊的队列，取出元素的顺序是按照元素的优先权（关键字）的大小，而不是按照元素进入队列的先后顺序。

==主要要做的就是插入任何结点和删除最大最小值==



如何表示堆？

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006101845022.png" alt="image-20221006101845022" style="zoom:67%;" />

不管是用链表还是数组都有各自的缺点



用树来表示表示堆比较方便：

优先队列（堆）的完全二叉树表示：

堆有两个特性：

- 结构性：用数组表示的完全二叉树
- 有序性：任一结点的关键字是其子树所有结点的最大（最小）值
  - 最大堆：也称大顶堆：最大值
  - 最小堆：也称小顶堆：最小值

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006102638786.png" alt="image-20221006102638786" style="zoom:67%;" />

### 5.1.2堆的插入

```c
typedef struct HeapStruct *MaxHeap;
struct HeapStruct{
    ElementType *Elements;/*存储堆元素的数组*/
    int Size;/*堆当前元素的个数*/
    int Capacity;
}
```

![image-20221006104848572](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006104848572.png)



插入值的算法：

```c
void Insert(MaxHeap H, ElementType item)
{/*将元素item插入最大堆H，其中H->Element[0]定义为最大值，不占元素，定义为哨兵*/
    int i;
    if(IsFull(H)){"略"}；
    i = ++ H->Size;//取出当前元素的下一位
    for(;H->Elements[i/2]<item;i/=2)//i/2是i结点的父节点
        H->Elements[i] = H->Elements[i/2];
    H->Element[i] = item;
}
```

没有哨兵要再中间for中增加`&& i>1`,有哨兵的话可以不用加，哨兵很大

时间复杂度：T（N） = O（log N）

### 5.1.3堆的删除

对于最大堆/最小堆，删除肯定都是在头节点。删除最上面头节点之后，把最后一个结点放到头节点，然后一个一个往下摆，往下比较。

时间复杂度：O（log N）

如何判断是否有左右儿子：==`Parent*2<=H->Size`==

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006111845884.png" alt="image-20221006111845884" style="zoom: 67%;" />

### 5.1.4堆的建立

最大堆的建立： 从最小堆先调整，然后都调好了再和上一个结点调，然后一个一个调下来。

代码再课本P150页。复杂度是等于树的高度

### 5.2.1哈夫曼树哈夫曼编码

在做成绩转换问题的时候，发现学生成绩分布的频率不同，如果频率分布高的用简单一点的编码，就会大大降低程序的复杂度。

**带权路径长度（WPL）**：

![image-20221006141943236](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006141943236.png)

**哈夫曼树（最优二叉树）**：WPL最小的二叉树

### 5.2.2哈夫曼树的构造

要使得带权路径长度（WPL）最小，必须使权值越大的叶节点靠近跟结点，而权值越小的叶节点越远离根节点。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006143130174.png" alt="image-20221006143130174" style="zoom:67%;" />

代码生成过程：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006143348251.png" alt="image-20221006143348251" style="zoom:67%;" />

哈夫曼树的特点：

- 没有度为1的结点
- n个叶子结点的哈夫曼树共有2n-1个结点
- 哈夫曼树的任意非叶节点的左右子树交换后仍是哈夫曼树

### 5.2.3哈夫曼编码

不等长编码：一定要避免二义性。

为了避免二义性：可以使用***前缀码prefix code***：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006144843894.png" alt="image-20221006144843894" style="zoom: 67%;" />

只要编码在叶子结点上就不会出现二义性，，第二张图就是不等长编码的情况。

举个例子：

![image-20221006145229474](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006145229474.png)

### 5.3.1集合的表示及查找

集合的主要运算：交、并、补、差，判断元素是否属于某一集合。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006150316561.png" alt="image-20221006150316561" style="zoom:80%;" />

用数组来表示最方便：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006150826435.png" alt="image-20221006150826435" style="zoom:80%;" />

例如：2的parent指向的是0，0的位置data是1，parent是-1。-1代表已经到头了。

和链表不同的是：是由子节点指向父节点

### 5.3.2集合的并运算

 <img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006151605994.png" alt="image-20221006151605994" style="zoom:67%;" /><img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006151929803.png" alt="image-20221006151929803" style="zoom:67%;" />

问题在于，不断的union的情况下树会越来越高，降低了find的效率。

为了改善合并以后的查找性能，可以采用小的集合合并到相对大的集合中。把Parent的负数值都改成对应的负数的元素个数值，只要判断根节点谁的负数绝对值大，就可以判断谁的元素多。

### P60 堆中的路径

堆一般用数组来表示。

堆的创建和插入元素。

![image-20221006154854087](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006154854087.png)

![image-20221006155035286](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006155035286.png)

### P61--64 File Transfer

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006155538624.png" alt="image-20221006155538624" style="zoom:67%;" />

这个题就不看了



### P65-72 树习题选讲

P65-66

根据前序和中序遍历，得到后续遍历的算法

![image-20221007152824072](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221007152824072.png)

post最终是：342651

P67-69完全二叉搜索树：

二叉搜索树和完全二叉树的定义：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221007153954768.png" alt="image-20221007153954768" style="zoom:50%;" />

完全二叉搜索树形式：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221007154105681.png" alt="image-20221007154105681" style="zoom:50%;" /<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221007155933273.png" alt="image-20221007155933273" style="zoom:67%;" />

 ==一般完全二叉树用数组来表示是很划算的==：因为如果用数组来表示树的话带来的问题计算会浪费空间，但是完全二叉树本就每个结点都是满的所以不会浪费空间。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221007155222433.png" alt="image-20221007155222433" style="zoom:50%;" />

思路：首先要判断根节点是哪个，如何判断呢？已知一棵树的元素个数，由于他是完全二叉树，那么他的结构肯定是固定的，所以得出左子树有多少个元素，那么根节点是这一组树中从小到大排的第左子树元素+1个。

从而分开左右子树。

然后左右继续递归，和上面一样，继续每一个结点分分分。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221007160622645.png" alt="image-20221007160622645" style="zoom:80%;" />

直接利用自带的sort进行排序（在C++的容器部分有涉及，建议回去看看）

```cpp
std::sort(a, a + 10);//默认从小到大排序，数组开始的地方，结束的地方，排序方式。
```

如果想要降序排列，需要自己编写compare函数，作为sort函数的第三个参数传入。

```cpp
bool cmp(const int &a, const int &b)
{
    return a > b;
}
std::sort(a, a + 10, cmp);
```

如何计算左子树的规模：

  <img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221007162934616.png" alt="image-20221007162934616" style="zoom:67%;" />

X不怎么影响最后算出来H的结果，所以拿掉X向下取整就可以，答案是一样的。

左子树结点个数：L = 2^H-1^-1+x   (X最小0，最大2^H-1^ ),X = min{X,2^H-1^}

###==P70-72霍夫曼树的习题还没看==



### 6.1.1什么是图

​		一般多对多的关系常常用图来表示。它把线性表和树全部包含在内了

- 一组顶点：通常用V（Vertex）表示顶点集合

- 一组边：通常用E（Edge）表示边的集合
  - 边的实质就是顶点对：（v，w）∈E，其中v，w属于V，**圆括号表示的是两端双回路可以从v到w，也可以从w到v**
  - 有向边<v，w>表示的是从**v指向w的边（单行线）**
  
  **==圆括号表示的是双向回路，而尖括号表示的是单行线，从第一个到第二个。==**
  
  - 图里也不考虑重边和自回路

对于数据对象集：G（V,E）由一个非空的有限顶点集合V和一个有限边集合E组成，V不能为空，E可以为空。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221009195940427.png" alt="image-20221009195940427" style="zoom:50%;" />

### 6.1.2邻接矩阵表示法

邻接矩阵表示一个图( 本质上用了二维数组的方法)：`G[N][N]`,N个顶点，从0到N-1编号。

如果从`vi--->vj`有边的话则`G[i][j]`=1,否则为0；

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221009201341629.png" alt="image-20221009201341629" style="zoom:67%;" />

邻接矩阵的特点1：对角线全为0 2：对称

为了省空间，只存一半。（仅针对于无向图）

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221009201922598.png" alt="image-20221009201922598" style="zoom:67%;" />

邻接矩阵有什么**好处**：

- 方便检查任意一对顶点之间有没有边
- 方便找任一顶点的所有邻接点（有边直接相连的顶点），无向图直接横向扫描，有向图纵向扫描
- 方便计算任一顶点的“度”（度就是该顶点的所有的边），（该点发出的边数为“出度”，指向该点的边数为入度）
  - 无向图：对应行（或列）非0元素的个数
  - 有向图：对应行非0元素的个数是“出度”；对应列非0元素的个数是“入度”。

**坏处**

 <img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221009202906107.png" alt="image-20221009202906107" style="zoom:67%;" />

###6.1.3邻接表表示法

邻接表：G【N】为指针数组，对应矩阵每行一个列表，只存非0元素.一定要很稀疏才划算。

 <img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221009203833591.png" alt="image-20221009203833591" style="zoom:67%;" />

邻接表的表示并不唯一，因为不一定元素会怎么出现。

同时他也没有很省空间，原因在于说每条边都被存了两次。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221009204109676.png" alt="image-20221009204109676" style="zoom:67%;" />

把列也存在一串链表中才能实现。

同时邻接表也不方便检查任意一对顶点之间是否存在边。

### 6.2.1图的遍历-DFS

**DFS——深度优先搜索（Depth First Search）**

把图里面每一个顶点都访问一边，同时不重复。

特点，访问完一个结点附近的所有结点之后，一定要原路返回，才可以从出口出去。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221009205324734.png" alt="image-20221009205324734" style="zoom:67%;" />

和树的先序遍历很像。

![image-20221009205456097](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221009205456097.png)

### 6.2.2图的遍历-BFS

**BFS——广度优先搜索（Breadth First Search）**

相当于树中的层序遍历。 

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221009210410548.png" alt="image-20221009210410548" style="zoom:50%;" />

### 6.2.3为什么需要两种遍历

....

### 6.2.4图不连通怎么办

有孤立结点怎么办。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221009210829343.png" alt="image-20221009210829343" style="zoom:33%;" />

回路：起点=终点的路径

如果一条路径上有回路则这个路径就不是简单路径

**连通图：图中任意两顶点均连通的图称为连通图。**

 <img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221009211156001.png" alt="image-20221009211156001" style="zoom:50%;" />

对于有向图：有向图中顶点V和W之间存在双向路径，则称V和W是**强连通**的。

**弱连通**：把非强连通图中的方向全部抹除之后是连通图，则称为弱连通。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221009211520433.png" alt="image-20221009211520433" style="zoom:67%;" />

解决方法代码：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221009211823144.png" alt="image-20221009211823144" style="zoom:50%;" />

### 6.3应用实例：拯救007

![image-20221012211106501](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221012211106501.png)





![image-20221012211054567](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221012211054567.png)

### 6.4应用实例：六度空间

广度优先搜索BFS思路

对每个结点进行广度优先搜索，搜索过程中累计访问结点数， 需要记录层数，仅计算6层以内的结点数。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221013190359904.png" alt="image-20221013190359904" style="zoom:67%;" /> 

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221013190656733.png" alt="image-20221013190656733" style="zoom:67%;" />

### P81-87如何建立图

***1.利用邻接矩阵来表示图***

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221013191216908.png" alt="image-20221013191216908" style="zoom:67%;" />

一般就是直接用一个二维数组来表示`G[][]`

```cpp
int Nv;//顶点数
int Ne;//边数
int G[MaxVertexNum][MaxVertexNum];//最大顶点数
```

 

**建树具体代码**：V和E代表顶点和边，

```c
typedef struct GNode *PtrToGNode;//定义一个指向GNode的指针
struct GNode{
    int Nv;//顶点数
	int Ne;//边数
	int G[MaxVertexNum][MaxVertexNum];//最大顶点数
    DataType Data[MaxVertexNum];//存放顶点中的数据的，DataType后面再定义，这里只是抽象的。
}
typedef PtrToGNode MGraph;
```

**初始化**：初始化有VertrexNum个顶点，但是没有边的图

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221013193147858.png" alt="image-20221013193147858" style="zoom:80%;" />

双重循序，遍历整个Nv*Nv矩阵。

**向MGraph中插入边：**

每次都是一个理：创建边结点类型

```c
typedef struct ENode *PtrToENode;
struct ENode{
    Vertex V1,V2;//首先一条边由两个顶点构成
    int Weight;//定义权值，有权图才需要
};

void InsertEdge(MGraph Graph,Edge E)
{
    Graph->G[E->V1][E-V2] = E->Weight;
    //如果是无向图，还要插入边<V2,V1>
    //Graph->G[E->V2][E-V1] = E->Weight;
}

typedef PtrToENode Edge;
```

**完整建立一个邻接矩阵图：**

C语言代码：

![image-20221013194735649](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221013194735649.png)



不用那么麻烦版本：（手输入版本）

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221013194840077.png" alt="image-20221013194840077" style="zoom:67%;" />

***2.利用邻接表来表示图***

邻接表本质就是指针数组G[N],对应矩阵每行一个链表，只存非0元素。

![image-20221013195927665](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221013195927665.png)

```cpp
typedef struct GNode *PtrToGNode;
struct GNode{
    int Nv;
    int Ne;
    AdjList G;//创建邻接表
};
typedef PtrToGNode LGraph;

typedef struct Vnode{
    PtrToAdjVNode FirstEdge;//指向第一条边的指针。
    DataType Data;
}
AdjList [MaxVertexNum];//每个点都是一个链表形式

typedef struct AdjVNode *PtrToAdjVNode;
struct AdjVNode{
    Vertex AdjV; //邻接点的下标，上一个结点传过来的
    int Weight;//权值
    PtrToAdjVNode Next;//指向下一个结点的指针。  
}；
```



建立这个图：

初始化：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221013201337750.png" alt="image-20221013201337750" style="zoom:80%;" />

插入边：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221013201300547.png" alt="image-20221013201300547" style="zoom:80%;" />

### P88-103 最短路径问题概述。

最短路径问题：在网络中（带权的图），求两个不同顶点之间的所有路径中，边的权值之和最小的那一条路径。

- 按照递增顺序找出各个顶点的最短路：（BFS广度优先搜索）
  - 无权图的

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230319185111327.png" alt="image-20230319185111327" style="zoom: 67%;" />

![image-20230319185438362](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230319185438362.png)



​       有权图的：

有权图会出现的一个问题就是负值圈：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230319190547446.png" alt="image-20230319190547446" style="zoom:67%;" />

不考虑这种情况：

### 6.5.1 Dijkstra算法

==**Dijkstra算法**==专门解决这种问题（**无法解决负边的问题**），**求最小路径的问题。**

- 令S={源点S+已经确定了最短路径的顶点vi}
- 对任一未收录的顶点v，定义dist[v]为s到v的最短路径长度，但是该路径仅经过s中的顶点。即路径{s-》（vi∈s）-》v}的最小长度。
- 路径是按照递增顺序生成。

![image-20230319191449929](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230319191449929.png)

![image-20230319192350710](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230319192350710.png)



### 6.5.2Floyd算法

多源最短路的算法（）：

- 直接将单源最短路算法调用|V|次，每个顶点都算一遍就可以了
- 方法2：==Floyd算法==：时间复杂度：O（V^3^）

![image-20230319192813275](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230319192813275.png)

### 6.5.3Prim算法（最小生成树）

最小生成树问题：（Minimum Spanning Tree）

是一棵树

- 无回路，|V|个顶点一定有|V|-1条边。
- 生成树：包含全部顶点，|V|-1条边都在图里面，生成树中任加一条边就会形成回路
- 边的权重和最小

如果图联通---那么一定存在最小生成树，二者互为充要条件。



解决方法就是贪心算法：

![image-20230320134133319](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230320134133319.png)



Prim算法：从根节点开始，让一棵树不断长大

和Dijkstra算法有点像。

### 6.5.4Kruskal算法--将森林合并成树

边比较少，顶点比较多

回路也是不能收，大贪心，把所有的边收进来。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230320134953242.png" alt="image-20230320134953242" style="zoom:67%;" />

时间复杂度：O（|E|log|E|）



### 6.5.5拓扑排序

AOV（activity on vertex）网络图：

![image-20230320135249472](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230320135249472.png)

拓扑序：如果图中从V到W有一条有向路径，则V一定排在W之前。满足此条件的顶点序列称为一个拓扑序。获得一个拓扑序的过程就是拓扑排序。

AOV如果有合理的拓扑序，那么必定是**有向无环图**（DAG）。

![image-20230320135517386](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230320135517386.png)

为图中的每个结点设置入度，入度为0的结点就可以直接输出，然后每次拿到一个入度结点，就把这个结点相邻的边的结点的入度-1.

![image-20230320140010000](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230320140010000.png)

可以用队列来完成这样的容器。

![image-20230320140156242](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230320140156242.png)

### 6.5.6关键路径问题（拓扑排序的应用）

和上述的AOV不同又提出了一种新的网络结构：

AOE（Activity On Edge）网络：边代表的是项目活动。

![image-20230320140643390](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230320140643390.png)





### 7.1 简单排序

```c
//规范模板
void X_sort(ElementType A[],int N)
```

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221015213223234.png" alt="image-20221015213223234" style="zoom:50%;" />

### 7.1.1冒泡排序

```c++
void Bubble_Sort(int a[],int n)
{
    for(int i=0;i<n-1;i++){
        flag = 0;
        for(int j = 0;j<n-i-1;j++){
            if(a[j]>a[j+1]){
                int tem = a[j];
                a[j]=a[j+1];
                a[j+1]=tem;
                flag = 1;//判断是否完全有序
            }
        }
        if(flag==0) break;
    }
}
```

好处:

- 如果待排元素放在一个单向链表时就很好用!!
- 相等不做交换,保证了稳定性

时间复杂度：最坏情况下O(n^2^),在完全有序的情况下：O(n)。

### 7.1.2(直接)插入排序

类似摸牌插牌问题：

```cpp
void Insert_Sort(int a[],int n){
    for(int i=1;i<n;i++){
        int tem = a[i],int j=i;
        while(j>=1 && temp<a[j-1])
        {	a[j]=a[j-1];//相当于直接覆盖，不用像冒泡那样一步一步两两交换。
        	j--;}//用--向前推移
        a[j]=tem;
    }
}
```

时间复杂度：最好情况顺序：T=O(N)，最差情况逆序：T=O（N^2^）

相等不做交换,保证了稳定性。相当于直接覆盖，不用像冒泡那样一步一步两两交换。

### 7.1.3 时间复杂度下届

**逆序对**：对于下标i<j，如果A[i]>A[j]，则称（i，j）是一对逆序对。

每次交换一组相邻元素，就会正好消去一个逆序对。

对于插入排序来说：时间复杂度T（N,I）=O(N+I);  I代表的是逆序对的个数。



**定理1**：任意N个不同元素组成的序列平均具有N（N-1）/4个逆序对。

**定理2**：任何仅以交换相邻两元素来排序的算法，其时间复杂度为Ω（N^2^）.



### 7.2希尔排序（shell sort）

进化版的插入排序： 

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221017193106512.png" alt="image-20221017193106512" style="zoom: 50%;" />

自定义一个间隔排序，每次间隔排序不断变小直到变成1.每次间隔变小之后还能保证之前的间隔是有序的。 

**原始的希尔排序：**

增量序列为N/2，每次都变为原来的一半，但是不互质容易后面小的间隔序列不起作用。

```cpp
void Shell_sort(int a[],int n){
    for(D=N/2;D>0;D/=2){
        for(p=D;p<n;p++){
            tem=a[p];
            for(i=p;i>0 && a[i-D]>tem;i -=D){
                a[i]=a[i-D];
            A[i]=tem;
            }
        }
    }
}
```



以一个整数序列为例来说明{12,45,90,1,34,87,-3,822,23,-222,32}，该组序列包含N=11个数。不少已有的说明中通常举例10个数，这里说明一下，排序算法与序列元素个数无关！ 
首先声明一个参数：增量gap。gap初始值设置为N/2。缩小方式一般为gap=gap/2. 
第一步，gap=N/2=5，每间隔5个元素取一个数，组成一组，一共得到5组

![这里写图片描述](https://img-blog.csdn.net/20180706215839405?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzIxMTA3NDMz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70) 对每组使用[插入排序](https://so.csdn.net/so/search?q=插入排序&spm=1001.2101.3001.7020)算法，得到每组的有序数列： 
![这里写图片描述](https://img-blog.csdn.net/20180706215936608?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzIxMTA3NDMz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

了解一些别的排序：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221017194542346.png" alt="image-20221017194542346" style="zoom:50%;" />

### 7.3堆排序

选择排序：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221017195925670.png" alt="image-20221017195925670" style="zoom:67%;" />

最坏情况换N-1次。但是寻找最小元的过程中也要扫描一次元素，所以时间复杂度上也是O（n2）；



利用最小堆：最小堆的根结点肯定是最小的

![image-20221017201204348](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221017201204348.png)



### 7.4归并排序有序子列

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221017202930307.png" alt="image-20221017202930307" style="zoom:67%;" />

和合并两个有序链表那个题很像，利用三个指针，每次比较之后两个指针向后挪动，再重新比较。

```cpp
void Merge(int a[],int tema[],int L, int R,int RightEnd){
    LeftEnd = R-1;
    tmp=L;
    len=RightEnd-L+1;
    while(L<=LeftEnd && R<=RightEnd){
        if(a[L]<a[R]) tema[tmp++] = a[L++];
        else tema[tmp++] = a[R++];
    }
    while(L<=LeftEnd){
        tema[tem++]=a[L++];
    }
    while(R<=RightEnd){
        tema[tem++]=a[R++];
    }
    //输出
    for(int i=0;i<len;i++,RightEnd--){
        a[RightEnd]=tema[RightEnd];
    }
}
```

### 7.5归并算法

分而治之 ，分为左右半边，左半边先排好然后右半边也拍好，之后用上面的两个有序子列合并的方法把两个子列合并。

```cpp
void MSort(int A[],int tempA[],int L,int RightEnd){
    int center;
    if(L<RightEnd){
        center = (L+RightEnd)/2;
        MSort(A,tempA,L,center);
        MSort(A,tempA,center,RightEnd);
        Merge(A,tempA,L,center+1,RightEnd);
    }
}
```

复杂度为：O(NlogN)

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221018200517305.png" alt="image-20221018200517305" style="zoom:67%;" />

### 7.6非递归的归并算法

每次让相邻的两个子序列归并，归并好之后再两两归并：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221018201758351.png" alt="image-20221018201758351" style="zoom:67%;" />

只要开一个最大的临时数组来存数据就可以，空间复杂度为O（N）。

![image-20221018203021737](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221018203021737.png)

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221018203148135.png" alt="image-20221018203148135" style="zoom:67%;" />

缺点：要额外的空间。在外排序中非常有用。



### 8.1快速排序（重要！！！）

现实中排序最快的：

都采用了分而治之的方法

挑出一个元素做主元（pivot）： 分为两块，左边小于pivot，右边大于pivot，然后分块把两边排序好。总体的思想也是递归的。

==重点在于如何把主元选好，主元选的好算法会很快。==

**算法思想：**

![image-20221018203747178](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221018203747178.png)

快速排序算法最好情况，就是每次主元都中分，那么时间复杂度为：T(N)=O(NlogN)。

### 8.2如何选主元

如果选A[0]为主元，那么时间复杂度为O（N^2^）

 选择头、中、尾三个数之中的中位数作为主元：

![image-20221018210118177](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221018210118177.png)

输出之前做点操作，把主元值的位置换到Right-1处，这样就只需要比较，A[Left+1]-A[Right-2]之间的元素。

### 8.3子集的划分

快速排序之所以快的原因：主元被插入到元素中的某个位置之后，他就一定是那个位置，不会再移动了。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221018210931530.png" alt="image-20221018210931530" style="zoom:67%;" />

1.停下来交换，每次都交换，但是主元一般都在序列的中间，时间复杂度是O（n）=O（nlongn ）

2.不理他，避免了很多无意义的交换，但是主元都停在端点，时间复杂度N^2

但是快排本身用的递归，所以会占用空间，对于小规模的数据，可能还不如插入排序快。

解决方法：再程序中定义一个Cutoff阈值，当数据规模小于Cutoff之后就改尾插入排序。

### 8.4算法实现

```cpp
void Quicksort(int A[], int Left, int Right){
    if(Cutoff<=Right-Left){
    Pivot=Median(A, Left, Right);//返回中位数值，同时left变三个数中最小的，right变最大的，同时Pivot现在在A[Right-1]中
    i=Left;j=Right-1;
    for(;;){//无线循环
       	while(A[++i]<Pivot){}
    	while(A[++i]>Pivot){}
		if(i<j)
            swap(&A[i],&A[j]);
    	else break;
    }
    swap(&A[i],&A[Right-1]);
    Quicksort(A,Left,i-1);
    Quicksort(A,i+1,Right );
    }
    else
        Insertion_Sort(A+Left,Right-Left+1);//开始的位置是A[left]
}
```

调用接口

```cpp
void Quick_sort(int a[],int N){
    Quicksort(A,0,N-1);
}
```

快排注意点：

**当基准数选择最左边的数字时，那么就应该先从右边开始搜索；当基准数选择最右边的数字时，那么就应该先从左边开始搜索。不论是从小到大排序还是从大到小排序！**



标准快排代码：

```cpp
//快速排序（从小到大）
void quickSort(int left, int right, vector<int>& arr)
{
	if(left >= right)
		return;
	int i, j, base, temp;
	i = left, j = right;
	base = arr[left];  //取最左边的数为基准数
	while (i < j)
	{
		while (arr[j] >= base && i < j)
			j--;
		while (arr[i] <= base && i < j)
			i++;
		if(i < j)
		{
			temp = arr[i];
			arr[i] = arr[j];
			arr[j] = temp;
		}
	}
	//基准数归位
	arr[left] = arr[i];
	arr[i] = base;
	quickSort(left, i - 1, arr);//递归左边
	quickSort(i + 1, right, arr);//递归右边
}
```



###8.5表排序

适用于：每一个待排元素都不是整数，而是一个类似结构体之类的，每次移动都要移动很多东西。

特点：不需要移动本身，只需要改变指向他们的指针。

- 间接排序
  - 定义一个指针数组作为“表”

这里的指针不是C语言中那个指针，只是记录了每个数的下标而已。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221020192523851.png" alt="image-20221020192523851" style="zoom:50%;" />

如果不单单要输出，还要用一个物理排序的时候怎么办呢？

==N个数字的排序是由若干个独立的环组成的：每个环之间没有交集==，所以可以按照环之间进行处理， 

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221020193152209.png" alt="image-20221020193152209" style="zoom:50%;" />

先把环第一个拿出来，然后把中间都按序摆好之后，最后把环第一个元素放到最后一个那边，一个环就摆好了。

判断一个环结束与否：`if(table[i]==i)`

时间复杂度：

- 最好情况：初始即有序
- 最坏情况：
  - 需要N/2个环，每个环包含两个元素
  - 需要3*N/2次移动
- 时间复杂度为：T=O（mN），m是每个A元素的复制时间。



### 8.6基数排序

先说桶排序：

 N个数，每个数的范围为：0-M，则建立M+1个桶，把N个数每个数都放进去，然后输出。当M远大于N时不划算。

基数排序：

用到了次位优先的算法：LSD算法，先从最后一位建桶排序。

![image-20221020194811651](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221020194811651.png)

时间复杂度：T=O（P(N+B)）

MSD主位优先算法：

![image-20221020195156797](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221020195156797.png)

对于扑克牌来说肯定是LSD优于MSD

![image-20221020195240390](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221020195240390.png)



### 8.7排序算法的比较：

 

![image-20221020195521502](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221020195521502.png)

![image-20221020195541048](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221020195541048.png)

### 排序习题讲解：Insert of Merge

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221020200203586.png" alt="image-20221020200203586" style="zoom:80%;" />

判断插入排序：

1. 从左到右扫描，直到发现顺序不对，则跳出循环。
2. 从跳出点继续向右扫描，与原始序列对比发现不同则为“非”
3. 循环自然结束，则判断为“是”，返回跳出地点

如何判断归并段长度：





#查找问题：

### 11.1散列表

编译处理中对变量的管理：动态查找问题。

利用AVL查找树来进行查找，但是查找过程中字符串的比较效率远不如整数，所以想法就是：**能不能把字符串转化为整数之后再比较。**



目前已知的查找：

![image-20221020202442966](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221020202442966.png)

一些别的查找方法：

- 已知对象位置找位置
  - 有序安排对象：全序、半序
  - ==直接“算出”对象位置：称为散列==

![image-20221020203010957](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221020203010957.png)



###11.2==散列表（哈希表）==

类型：起始是一种符号表

数据对象集：==符号表是“名字-属性”对的一种集合==

主要的一些操作：

![image-20221022194408235](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221022194408235.png)

首先先构造一个散列函数，然后把数值依次放进去。

如果一个表里某个地址为空，那么这个数一定不在表中。

装填因子概念：设散列表空间大小为m，填入表中元素的个数是n，则α=n/m为散列表的装填因子。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221022195452672.png" alt="image-20221022195452672" style="zoom:67%;" />

散列的两个基本思想：

1. 以关键词key为自变量，通过一个确定的函数h（散列函数）计算出对应的函数值h（key），作为数据对象的存储地址。
2. 可能不同的关键字会映射到同一个散列地址上，就会引发冲突，需要某种冲突解决的策略。

### 11.2.1数字关键词的散列函数构造

 <img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221022195751541.png" alt="image-20221022195751541" style="zoom:67%;" />

数字关键词的散列函数构造：

1. 直接定值法：h（key）=a*key+b；
2. 除留余数法：h（key）=key % p（p一般是表的大小，p一般取素数）
3. 数字分析法： h（key）=atoi（key+7）//（char *key）
4. 折叠法：
5. .......

只要哈希值能被每一位数给影响就可以。

### 11.2.2字符串关键词的散列函数构造

![image-20221022201016010](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221022201016010.png)

把每个元素都看成是32进制的数。

例子：

![image-20221022201108685](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221022201108685.png)

如何计算：

```cpp
Index Hash(const char *Key,int TableSize){
    unsigned int h=0;//初始化散列函数值
    while(*Key != '\0')
        h = h*32+(*Key)++;
    return h%TableSize;
}
```

### 11.3 散列查找的冲突处理方法

- 换个位置：开放地址法：若发生了第i次冲突，试探的下一个地址将增加d~i~,基本公式是：`hi(key)=(h(key)+di) % TableSize`
  - 线性探测：d~i~=i（di是线性的，相当于一个一个找）
  - 平方探测：d~i~=±i^2^;
  - 双散列：d~i~=i*h~2~（key），设计两个散列函数。
- 统一位置的冲突对象组织在一起：链地址法

### 11.3.1线性探测法：

实质就是在原来序列上找下一个，再找下一个，一直找下一个的过程

带来的问题就是：由于在某个地方会冲突，那么在那个位置向后会一直冲突，从而造成聚集的现象。

**散列表的查找性能分析：**

- 成功平均查找长度（ASLs）
- 不成功平均查找长度（ASLu）

 	![image-20221022205146780](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221022205146780.png)

不成功就是插入的时候取后面找，找到空位存在，那么就可以说明它不再hash表里面。

### 11.3.2平方探测法（二次探测）

先正后负，然后再加一平方

优点：避免了聚集，而且平均查找次数要小

缺点：不一定有空间，有的时候二次探测不一定找得到

**定理：如果散列表长度TableSize是某个4k+3（k为正整数）形式的素数时，平方探测就可以探查到整个散列表的空间。**

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221022210500780.png" alt="image-20221022210500780" style="zoom:80%;" />

比较复杂，如果需要可以返回去看看P136

###11.3.3双散列探测法

定理表明设计成：h~2~（key）=p-（key % p）比较好

这里的p小于TableSize



**再散列（Rehashing）**

当散列表元素太多（装填因子α太大）时，查找效率会下降：

一般来说：实用的最大装填因子取：0.5-0.85.

重新装载的过程并不是把原本的元素照搬，而是要重新找。

### 11.4 分离链接法

将相应位置上冲突的所有关键词存储再同一个单链表中。

![image-20221022212419800](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221022212419800.png)

### 11.5散列表的性能分析

用平均查找长度（ASL）来衡量散列表的查找效率：成功、失败两种情况。

关键词的比较次数与冲突的多少有关，冲突的多少与：

1. 散列函数是否均匀
2. 处理冲突的方法
3. 散列表的装填因子α有关【0-1之间】

- 对于线性探测法：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221024203518552.png" alt="image-20221024203518552" style="zoom:80%;" />

只是反映一般情况下，不一定就是等于这个。

- 对于平方探测

![image-20221024203709797](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221024203709797.png) 

一般情况下最大装载因子不超过0.85

**总结：哈希查找（散列查找）**

散列法的查找效率期望是常数O（1），它和常用的树查找、二分法等查找log2n简单很多。==与关键字的空间的大小n无关，适合关键字比较计算量大的问题。==

常用于字符串的管理。

要以较小的阿尔法为前提，是以空间换时间为代价的，对关键字是随机的，不便于顺序查找关键字，也不适合范围查找和最大最小值查找。



两种方法：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221024204842264.png" alt="image-20221024204842264" style="zoom:67%;" />

![image-20221024204913836](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221024204913836.png)

### 11.6散列查找的应用：文件中单词词频的统计



### P140-143 小白专场：电话聊天狂人

 ![image-20221025193704979](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221025193704979.png)

用链表来实现哈希表：

```c
void ScanAndOutput(HashTable H){
    
    
    for(int i=0;i<H->TableSize;i++){
        Ptr = H->Heads[i].Next;
        
        
    }
}
```

![image-20221025194237181](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221025194237181.png)

模块的引用与裁剪：

![image-20221025194402627](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221025194402627.png)





### 12 KMP算法（串的模式匹配1-5）

什么是串：串是线性存储的一组数据（默认是字符）

比较有难度的：==匹配子串==

**串的模式匹配：**

给定一段文本：string=.......

给定一个模式：pattern=...........

求pattern在string中出现的位置？这就是问题所在。

```c
Position PatternMatch(char *string,char *pattern){
    
}
```

方法1：使用C语言的库函数strstr

```c
char *strstr(char *string,char *pattern)
```

![image-20221025200526204](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221025200526204.png)

匹配不上的情况：打印出NULL。

 strstr库函数的时间复杂度是T=O（n*m），n是字符串长度，m是模式的长度。



#### 对strstr方法的改进（KMP算法）

KMP算法：时间复杂度是T=O(n+m)

![image-20221025201744460](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221025201744460.png)



#### KMP算法的实现

主函数：

```cpp
#include<stdio.h>
#include<string.h>

typedef int Position;
#define NotFound -1

int main(){
    char string[]="this is a simple example";
    char pattern[]="simple";
    Position p = KMP(string,pattern);
    if(p==NotFound)printf("Not Found. \n");
    else printf("%s\n",string+p);
    return 0;
}
```

![image-20221025203034635](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221025203034635.png)

match[]记录的是匹配上的那个小子串的长度，【0，p-1】那段、也可以说是【0，p）那段。记录的最后一个匹配位置的下标。

#### BuildMatch的实现

要算j的match值，我们先看看他和j-1的match有啥关系。

经过反证法得到：match[j] = match[j-1]+1,最多最多match[j]=match[j-1]+1 ，前提是：`pattern[match[j-1]+1]==pattern[j]`

```c
void BuildMatch(char *pattern, int *match){
     int i,j;
    int m=strlen(pattern);
    match[0]=-1;
    for(j=1;j<m;j++){
        i=match[j-1];
        while((i>=0) && (pattern[i+1]!=pattern[j]))
            i=match[i];//缩短
        if(pattern[i+1]==pattern[j])
            match[j]=i+1;
        else match[j]=-1;
    }
}
```

####串匹配实现

1.暴力：

```cpp
int ViolentMatch(string text, string pattern)		//text是文本串,pattern是关键字
{
	int tLen = text.size();
	int pLen = pattern.size();
 
	int i = 0;
	int j = 0;
	while (i < tLen && j < pLen)
	{
		if (text[i] == pattern[j])
		{
			//如果当前字符匹配成功（即text[i] == pattern[j]）,匹配下一个字符
			i++;
			j++;
		}
		else					//如果当前字符匹配失败,pattern从头开始匹配
		{
			i = i - j + 1;
			j = 0;
		}
	}
	
	if (j == pLen)				//当pattern全部匹配成功,返回匹配位置
		return i - j;
	else
		return -1;
}
```





KMP:

``` cpp
#include <bits/stdc++.h>
using namespace std;

//在关键字中记录与前缀匹配的组合,记录在next数组
void make_next(string pattern, int *next)
{
    int q, k;               //q是匹配的位置,k是前缀开始的地方
    int m = pattern.size(); //关键字的长度

    next[0] = 0; //用于记录关键字中与前缀匹配的组合的位置
    for (q = 1, k = 0; q < m; q++)
    { //q是后面的数,k是前缀开始的地方
        while (k > 0 && pattern[q] != pattern[k])
        { //当后面的组合与前缀不同时,前缀数-1继续匹配
            k = next[k - 1];
        }

        if (pattern[q] == pattern[k])
        { // 如果前缀与后面有相同字符
            k++;
        }
        next[q] = k; //用于记录关键字中与前缀匹配的组合的位置
    }
}

//kmp算法
int kmp(string text, string pattern, int *next)
{
    int n = text.size();    //文本串的长度
    int m = pattern.size(); //关键字的长度

    make_next(pattern, next); //在关键字中记录与前缀匹配的组合,记录在next数组

    int i, q;
    for (i = 0, q = 0; i < n; i++)
    { //i --> text, q --> pattern
        while (q > 0 && pattern[q] != text[i])
        {                    //如果匹配失败,往前找与前缀相同组合的位置
            q = next[q - 1]; //只要next[q-1]不大于0,那么就是还没找到与前缀相同的组合
        }                    //继续在循环中找到与前缀相同的组合,直到next[q-1]等于0

        if (pattern[q] == text[i])
        { //如果匹配正确,关键字位置+1
            q++;
        }

        if (q == m)
        {                     //如果q的位置是关键字的长度,那么就是找到字符串了
            return i - q + 1; //返回字符串的位置
        }
    }
    return -1; //整个文本串找完都没有找到字符串,返回-1
}

int main()
{
    string text = "ABAABAABBABAAABAABBABAAB";
    string temp = "ABAABBABAAB";
    int len = temp.size();
    int arr[len+1];
    make_next(temp, arr);
    
    cout << kmp(text, temp, arr);

    return 0;
}

```

