#	c++内存管理（侯捷）

----从平地到万丈高楼

##第一讲：primitives（基础工具）

### 1.OverLook

###2.**内存分配的每一层面**

![image-20230102145842326](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230102145842326.png)

最下面的一层是针对某个特定操作系统的一些有关内存调用的API

![image-20230102150558680](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230102150558680.png)

先来说一些在malloc之上的调用接口，

- malloc

- new
- operator new（）
- allocator<T>:: allocate()  //分配器

### 3.四个层面的用法

malloc的用法：

malloc向系统申请分配size字节的内存空间，返回类型为void*类型；

```cpp
void *p=malloc(512);
free(p);

int* p;
p = (int*)malloc(sizeof(int));
free(p);//释放内存
```

new:

```cpp
complex<int> *p2=new complex<int>;
delete p2;

int *q = new int(5); //开辟大小为sizeof(int)的空间，并初始化为5。
//二维
int (*a)[6] = new int[5][6];
```

::operator new

其实这个的底层就是调用malloc和free

```cpp
void *p3=::operator new(512);
::operator delete(p3);
```

分配器：

在不同的编译器下调用的接口有所不同，所以要声明版本

![image-20230102153459541](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230102153459541.png)

重要的就是allocate和deallocate 

使用分配器带来的困扰就是，归还的时候一定要归还和原本一样大的空间。所以一般只会和容器搭配使用。 

###4-6.**基本构件之一newdelete expression**

new一般做两件事，1分配内存，2调用构造函数。

![image-20230102155505223](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230102155505223.png)

operator new的源代码

![image-20230102155728366](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230102155728366.png)

内部不断调用malloc，如果成功就返回，如果分配不了就进入while内部发callnewh函数去释放一些系统内存，从而下一次有足够内存被分配。



那么delete也对应如此：

先析构函数，然后释放内存

![image-20230102161625055](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230102161625055.png)



所以总结：

- new调用了operator new，而operator new又调用了malloc
- delete调用了operator delete，而这个又调用了free



是否可以通过指针直接调用Ctor和Dtor（构造函数和析构函数），大部分的编译器是不允许的、

###7. Array new

一次性建造一个array

```cpp
Complex* pca=new Complex[3];//调用了三次构造函数
delete[] pca;//同样调用了三次析构
```

如果少了[]，那么只会调用一次析构函数。会导致内存泄漏，会之析构掉一块。

会有一个cookie记录new出来东西的长度：![image-20230102165544170](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230102165544170.png)

相当于底层的placement new

```cpp
A* tmp=buf;
for(int i=0;i<size;i++){
    new(tmp++) A(i);
}
```

构造和析构的顺序是相反：

构造如果是从上到下，那么析构就是从下到上。

在VC中，申请一块内存会被自动填加到16的倍数，同时还包含上cookie和下cookie![image-20230102182526016](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230102182526016.png)

###8. **Replacement new**（定点的new）

placement new允许我们将object建构于已经分配好的内存之中。

```cpp
char *buf=new char[sizeof(Complex)*3];
Complex* pc=new(buf)Complex(1,2);//new括号内部是已经分配好内存的
delete[] buf;
```

相当于原本的new就不需要再分配内存了。

本质就是内部并不分配内存

### 9.重载

重载operator new这样的操作，使得有机会可以改变内存分配的机制

![image-20230103152345536](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230103152345536.png)

最终还是要回到::operator new(size_t)和::operator delete(void*)  然后用malloc 



- 重载全局的operator new和delete（基本不会使用）

![image-20230103153622218](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230103153622218.png)

这里只是示范了如何重载这个接口。

- 在类内部使用重载的operator new和delete

![image-20230103153958347](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230103153958347.png)

你在类的内部重载operator new和delete之后，就会在你new一个类对象和delete一个类对象的时候调用

```cpp
Foo* p=new Foo;
delete p;
```

###10-11重载实例

重载new()和delete()，正常里面是放一个指针，这个指针已经分配好内存了。

也就是上面说的placement new，这本来就是对new的一种特殊形式

![image-20230103160405456](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230103160405456.png)

第一个参数一定要是size_t，后面的参数可以自己定义。

delete只有在异常出现的时候才会调用。

在标准库中有一个模板叫：basic_string，我们所使用的string就是它的一个typedef

![image-20230103161547226](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230103161547226.png)



###12.**Per-class allocator**

为了减少每次需要空间，每次就要malloc的这样一个工作，使用者想到了是否可以先挖一大块内存，需要的时候直接调用。而且除此之外，每次malloc都会得到前后两个cookie，也会占用较大的内存。内存池的分配，内存池一般减少用链表来管理：

![image-20230103164837231](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230103164837231.png)

在回收的时候，**这个内存也会回收到单向链表的头。**

###13.Per-class allocator2

![image-20230103170703460](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230103170703460.png)

在后续的内存管理中，特别喜欢用union这个操作，把一个对象看成一个指针：![image-20230103170935891](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230103170935891.png)

###14.**Static allocator**

把上述的每次分配一大块，然后把每一小块切割之后用链表串在一起这一系列动作能不能集中起来？变成一个类：

![image-20230103193641346](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230103193641346.png)

在后续使用的时候只需要：

```cpp
class Foo{
  	static allocator myAlloc;
    myAlloc.allocate(size);
    myAlloc.deallocate(p,size);
};
```

![image-20230103194134724](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230103194134724.png)

只是每一块内部是连续的地址，块与块之间不一定是连续的。

###15.**Macro for static allocator**

也就是把上面浅黄色的部分定义成一个宏，然后每次调用这个宏就可以

![image-20230103200550690](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230103200550690.png)

最下面的括号要加上类的名称

```cpp
IMPLEMENT_POOL_ALLOC(Foo);
```

这就是标准库中allocator一步一步的来源：

进化到现在，allocator已经有16条free-lists，可以应付16种不同的大小。而且不再以static呈现，而是一个global allocator。

###16. new handler

在operator new没有能力为你申请的变量分配内存的时候，会抛出异常或者返回一个0指针。而在抛出异常之前会先调用一个可以由我们自己指定的hanndler函数：

![image-20230103201848779](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230103201848779.png)

- 会去尝试释放一些内存，从而得到更多可以分配的内存
- 或者直接退出/杀手程序

比如以下形式：

```cpp
void noMoreMemory(){
    cerr<<"out of memory";
    abort();
}

void main(){
    set_new_handler(noMoreMemory);
}
```



而且对于operator new[]和operator delete[]来说是有默认的=default和=delete版本的。

## 第二讲：std::allocator

直接来看标准库的allocator

###17.**VC6 malloc()**

==malloc申请下来的区块是带着cookie的，cookie是记录区块的大小的，要想保证可以正确去除cookie就必须保证每个区块等大==

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230105200229421.png" alt="image-20230105200229421" style="zoom:67%;" />

同时会填补成16的倍数。

###**18.VC6标准分配器之实现**

其实就是一个allocator的模板类，里面最重要的就是调用了：

- allocate
- deallocate

这两个函数，底层又是对operator new的调用。

经典的各类容器的<>第二个参数默认就是一个allocator<>对应类型。

### 19.BC5标准分配器之实现

也是调用operator new和delete。就是让malloc和free工作。

###20. G2.9标准分配器的实现

也有一个allocator，但是2.9版本并没有被加入到任何容器种，原因是还在使用operator new，因此还提供了一个std::alloc。

**但是只有allocator被称为标准分配器**

###21 **2.9std_allocVSG4.9__pull_alloc**

2.9版本的std::alloc已经在4.9变成了__pull_alloc,本质没什么区别。

![image-20230105203225966](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230105203225966.png)

### 22.pull alloc的用例

__pull_alloc的好处就是去除了cookie

### 23.std alloc

alloc实质上是负责16条链表，每条链表负责不同字节（大小）的内存，如果需要的内存不是8的倍数会被自动调整至8的倍数。

每个链表会挖多少块呢？20块，没什么原因，就是20块。而且一般是20*2，也就是40，但是还有另外一半一样的大的是没有被切割放在那边待命的，后续还有容器需要分配的时候直接用这半块就好了。

![image-20230105210555568](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230105210555568.png)

归还内存也就是deallocate的时候就是：把回收的操作对应成链表的操作，指针变化。

如果高于了16条链表的最大可以放的大小，就会调用malloc，这个时候的malloc就带cookie了。

![image-20230105211342025](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230105211342025.png)

使用嵌入式指针的方法，用4个字节的一个指针指向自己。

### 24-26.std alloc的运行过程

分配器对应的客户应该是容器

每次分配的指针一般都先给到分配池内部，需要的时候再去分配池挖。

怎么看选择哪个链表，把需要的内存/8 -1，就是哪个链表，比如48，那么就是48/8-1=5，就是5号链表。

![image-20230106190708440](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230106190708440.png)

这一整个大块还是malloc来的，带cookie

而且从pool种切割出来准备挂到free list区域后面的块的数目应该永远小于20，即使切割完大于了20也要这么做，切成20然后剩下 继续到pool中去。而且pool内部的那一块也是不带cookie的 

追加量=累积量/16 然后向8整位。

如何定位战备池呢？从图中也可以看出来，是使用`start_free`和`end_free`两个起始和终止指针来定位战备池。

如果不同类型的容器但是大小是相等的话，也会共用一条链表。

如果内存池的大小不够分配下一次需要的一个块的大小，那么会先找到和目前内存池相同大小的链表先挂上去，然后重新分配一块内存来供新的东西

![image-20230106190414298](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230106190414298.png)



当系统的内存不够用的时候会发生什么呢？

因为之前分割的很多20个的那种块可能没被分配完，它内部还有很多的空间，所以如果系统的heap无法提供更多的内存，alloc操作就会从手中资源最接近需要分配内存大小的那块回填到pool中，一般就是从右边找。这边回填的内存不用切20块，正常系统需要多少给多少就可以。



就是看能不能满足20个，满足不了20个就看能不能满足一个，一个都满足不了就是碎片，就去找一个链表挂起。

### 27-29 std_alloc源码剖析

G4.9**就会删除第一级**

总共分为两级分配器，第一级主要做的事情是new handle也就是内存不够不断找内存的那个工作。

第二级就是上述所讲的16条链表的工作。

第一级分配器的名称：`class __default_alloc_template`



这是一个把字节对齐的函数：比如13会取整到16

![image-20230106193059286](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230106193059286.png)

用指针的指针来指向具体哪一条链表内的哪个头元素，比如第一个指针指向第8条链表，二重指针指向第八条链表的头元素。

![image-20230106194959404](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230106194959404.png)

**refill 重新填装函数**，相当于重新分配。

![image-20230106201454075](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230106201454075.png)

利用chunk_alloc这个函数拿到一大块内存。

![image-20230106201807680](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230106201807680.png)

obj就是转型成之前那个指向自身指针的union那个类型。先转为字节类型，加上n指向下一块之后再转成union类型那个指针。



**chunk_alloc**函数

![image-20230106203043717](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230106203043717.png)

如果不是1个或者20个，碎片的话，就重新分配空间。

![image-20230106203601618](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230106203601618.png)

![image-20230106203756865](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230106203756865.png)

内存的补充永远是补充到战备池里面的。

- 先检查战备池，够的话先用
- 不够检查是否有碎片
- 然后重新分配内存到战备池

![image-20230106205209286](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230106205209286.png)

###30.std__alloc观念大整理

![image-20230106210254728](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230106210254728.png)

第一种通过临时对象申请的，不带cookie，申请再栈区。

第二种动态分配的，是需要cookie的。 在容器push_back的过程中会copy一份，copy的那份是不带cookie的。

### 31pool allocator运行观察

写一个程序看看cookie是不是真的减少了

 ![image-20230106211024989](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230106211024989.png)

2会被调用

![image-20230106212741838](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230106212741838.png)



## 第三讲 malloc/free

==这一讲说的都是malloc，并非allocator==

### 32.VC6和VC10的malloc比较

==内存都是向windows中那块特殊的内存CRT里面来的==

**VC6**

![image-20230107215451283](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230107215451283.png)

_heap_alloc_base(...)函数做的就是判断要拿的内存是否比`__sbh__threshold`这个门槛小，门槛的大小为//3F8,i.e.1016

这是为一个小区域服务的。

sbh是 small block heap小区块。

**VC10**

![image-20230107215809534](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230107215809534.png)

不论大小，==都直接调用操作系统的HeapAlloc这个函数==。

HeapCreate和HeapAlloc这些都是windows操作系统的一些api接口，windows维护了海量的内存。

![image-20230107220202053](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230107220202053.png)

`_heap_init`函数做的就是分配好16个HEADER，只是分配了16个头

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230107220202155.png" alt="image-20230107220202155" style="zoom:67%;" />



HEADER 的结构：

消耗一个数据结构来管理1mega的内存

### 33-37 VC6内存分配

2. **_ioinit()函数**

第一次内存分配：

![image-20230107220931333](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230107220931333.png)

如果定义了宏DEBUG，就会调用_malloc_dbg()函数

而这个函数先分配256个字节的内存，转化到二进制就是100

3. **_heap_alloc_dbg()**函数

在debug模式下会附加一块crtmemmenblockheader

![image-20230107221522897](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230107221522897.png)

**正真需要的内存就是浅绿色那块，可以在标号5看到它多大，但是这个并不是总内存的大小，总内存是看cookie里面的标记。**

![image-20230107221603490](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230107221603490.png)



这一块就是分配的内存，附加一些东西。上面的8格小内存没格都有自己的含义，在紫色那个函数中对应了。

同时还有pFirstBlock和pLastBlock两个链表链接起来。

4. **_heap_alloc_base()函数**

![image-20230107222403495](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230107222403495.png)

上面定义好的总内存和门槛比较，门槛是1016，为什么不是1024，因为加完cookie（8个字节），刚好就是一个cookie的大小。

5. **__sbh_alloc_block() 函数**

![image-20230107222548144](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230107222548144.png)

![image-20230107222554809](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230107222554809.png)

加上两端的cookie并规整到16的倍数。



**接下来就是内存的分配，前面都只是在计算区块的大小：**

6. **__sbhalloc_new_region()函数**

![image-20230107223418987](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230107223418987.png)

调用了Windows下的VirtualAlloc这个api申请1M的内存，1个HEADER管理1M内存

HEADER一共有两个指针，一个指向真正的内存1M

而HEADER另外有一个指针指向下图所示的数据结构用来管理内存：

![image-20230107223538935](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230107223538935.png)

BITVEC是一个unsigned int 占64个字节，所以相当于32个64个字节。

还有32个Group负责管理每个区块是否有出现过，每个Group是64个指针变成双向链表。

而这个数据结构的大小大概有16k左右。



7.**__sbhalloc_new_group()函数**

这个函数的目的就是希望用刚刚的32个group来管理1M的内存，相当于想成把1M内存分为32块（**1个HEADER分32块，每块32k**）。（1024/32=32k），每一个32k又细分成8个块。4K就是一个page。 

![image-20230107225545196](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230107225545196.png)



切割内存动作：

![image-20230107225847713](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230107225847713.png)

切割实质上是cookie的调整，并改变起始指针的位置。



### 38-41 SBH行为分析-分配（small block heap）

略，感觉太过底层，我不太需要



###42.VC6的内存管理free

free的时候应该落在哪一个Header，Header里面的哪个group，group里面的哪一个free-list

只要看指向那个内存的__sbh_pHearderList具体夹在哪个Header之间就能找到他所在哪个Header。哪个Header又有32段，也是减去头除以单位长度即可。

如何找到自己在哪个链表呢，把指针向上找到cookie，然后得知自己有多大，转化成10进制/16 -1就知道在哪条链表。

### 43-44 VC内存管理总结

**1M（1个Header）---32个group（每个32k，这个是由windows操作系统的virtualalloc函数来申请的真正的内存）---64条链表（32对双向链表）**

层层递进的内存管理方式，分段管理：

优点？

==为了更好地把内存回收！！==

如何判断是否全回收呢？

==在每个group最上面有个counter，只要malloc就-++，free就--，如果这个值是0，就说明全回收。==



同时当内存全部回收之后不会马上还给操作系统，而是会进行一个defer操作，也就是延迟。

![image-20230109212451196](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230109212451196.png)



**allocator和malloc的关系**：

allocator管理16条链表，每次内存不够都会使用malloc申请

## 第四讲 loki::allocator

略

## 第五讲 other issues

介绍GCC和G++平台下其他的分配器，与第二讲不同，这一讲的操作开头都是

```cpp
__gnu_cxx::new_allocator
    
__gnu_cxx::malloc_allocator
```



###50 **GNU C++对7个allocators的描述**

GNU C++的STL存在\include\c++\bits文件夹之下

分配器存在：\include\c++\ext之下

![image-20230109214754004](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230109214754004.png)

- 这种方法就是需要内存就new，释放内存就直接delete

gnu一般用的分配器都是： `new_allocator`

```cpp
__gnu_cxx::new_allocator
    
__gnu_cxx::malloc_allocator
```

这二者的区别在于第一个使用了全局::operator new和delete

而第二个使用了malloc和free



- 第二种做法，使用cache（缓存）

![image-20230109215353918](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230109215353918.png)

![image-20230109220902922](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230109220902922.png)

只有`__gnu_cxx::array_allocator`底部使用静态的数组来分配内存，别的都是动态内存分配。

一共有7个allocator

==最大的优势其实是内存占用小了，不再需要那么多的cookie==



而且从GNU4.9可以看出

![image-20230109220548073](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230109220548073.png)

我们用的分配器都是子类分配器，无需面对父类分配器

![image-20230109220724601](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230109220724601.png)

### 51.VS2013标准分配器与new_allocator

只要涉及到分配器，大部分都应该包含memory头文件，而在vs底下，memory又包含了xmemory

###52G4.9 array_allocator

array是C++11的一个新的容器，内部是一个数组

![image-20230110203222786](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230110203222786.png)

指向一块数组，静态的，不需要释放。

所以只有allocate函数，deallocate也有这个接口，但是什么事情都不做。

![image-20230110203405942](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230110203405942.png) 

###53 debug_allocator

相当于包覆在一个别的分配器上，本身没什么用

### 54-55bitmap——allocator

private继承自free_list

![image-20230110204722726](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230110204722726.png)

只为调用一个的客户服务，相当于只为容器服务。

一开始分配64个block，这些block后续会成倍增长，每次*2，在这些block的前头加上bitmap（2个，一个bitmap32位，所以有两个），就称之为super-blocks

![image-20230110205130475](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230110205130475.png)

两个指针组成一个单元，指向block的第一个和第二个单元，表示vector内的一个元素，然后一个单元代表了一个super-block。

同时内部自己写了一个和vector几乎一样的mini-vector

![image-20230110210154023](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230110210154023.png)



如何回收呢？

全回收之后会用另外一个vector指向头部，把原本那个vector的指针打断掉。专门全回收用的，这个容器最多放64个super-block，超过64个会把最大的那个还给OS。

### 56 Const

const放在函数的后面：**意图是修饰成员函数**，成员不能改变参数的值

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230113214721088.png" alt="image-20230113214721088" style="zoom:80%;" />

常量对象是不允许调用非常量函数的，比如：

```cpp
const String str("hello world");
str print();
//错误调用
```

当成员函数的const和non-const版本同时存在的时候，常量对象只会调用const成员函数

非常量对象只会调用非常量成员函数。

### 57new和delete

...

