# 数据结构C++复现

## 1最大子列和问题

![image-20221008145802211](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221008145802211.png)

先给一个主函数

```cpp
int main{
    int n;
    int a[100000];
    cin>>n;
    for(int i=0;i<n;i++)
        cin>>a[i];
    MaxSubseqSum(n,a)
}
```

####算法1：暴力二循环，时间复杂度O（n^2^）

```cpp
int MaxSubseqSum(int n,int a[]){
    int max = 0;
    for(int i=0;i<n;i++)
        int temp = 0
        for(int j=i;j<n;j++){
            int temp += a[j];
            if(temp>max)
                max = temp;
        }
    return max;
}
```

错误点：

```cpp
int temp += a[j];//写成了int temp=a[i]+a[j]
```

#### 算法2：贪心算法，在线处理

```cpp
int MaxSubseqSum(int n,int a[]){
    int max=0;
    int temp=0;
    for(int i=0;i<n;i++){
		temp += a[i]
        if(temp<0)
            temp = 0;
        else if(max<temp)
            max = temp;
    }
    return max;
}
```

如果需要[Maximum Subsequence Sum](https://blog.csdn.net/liyuanyue2017/article/details/83015775)也就是说还需要输出最大子列和的上下标：

```cpp
	int left = 0;
	int tmpleft = 0;
	int right = n-1;
	int max =0;
	int tmpSum=0;
	for(int i=0;i<n;i++){
		tmpSum+=a[i];
		if(tmpSum<0){
			tmpSum=0;
			tmpleft = i+1;   // 开头的数就在这段被抛弃子序列的下一个 
		}else if(max < tmpSum){
			max = tmpSum;        
			left = tmpleft;   // 每次更新最大值也就确定了一段子序列，保存此时的开头 
			right = i;       // 结尾的数就在每次更新最大值时 
		}
	}
	if(max>=0)
		cout<<max<<" "<<a[left]<<" "<<a[right];
	else
		cout<<0<<" "<<a[0]<<" "<<a[n-1];
	return 0;
```

### 01链表（List）的结构定义：

链表有多个结点（分数据域和指针域）：以多项式为例，链表每个结点存储多项式中的一个非零项的系数和指数两个数据域和一个指针域：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221008160547022.png" alt="image-20221008160547022" style="zoom: 50%;" />

如何用C++表示List的结构：

```cpp
typedef int Position//类型别名，现在Position相当于int类型
typedef struct LNode * List;//指针类型别名，相当于List = struct LNode *
struct LNode{
    ElementType Data[MAXSIZE];
    Position Last; /* 保存线性表中最后一个元素的位置 */
}
```

关于以上代码的解释： `typedef struct LNode * list`表示定义了一个别名`list`，`list`代表 `struct LNode *`类型的别名，它是一个指针类型。`list a`，就是定义了一个`struct LNode *`类型的变量`a`。

补充：

ElemType是数据结构的书上为了说明问题而用的一个词。它是element type（“元素的类型”）的简化体

具体的用法是：typedef int Elemtype；代表Elemtype是整形数据类型；

### 01-二分查找(BinarySearch)

和上面链表的结构要结合起来

```cpp
Position BinarySearch(List L,ElementType X){
	int left=1;
	int right->Last;//因为上面的结构体保存过Last的值所以这里可以用
    int pos;
    while(left<=right){
        pos = (left+right)/2;
        if(L->Data[pos] == X)
            return pos;
        else if(L->Data[pos] < X)
            left = pos+1;
        else if(L->Data[pos] > X)
			right = pos-1;
    }
    return 0;
}
```

## 2用C++来创建线性表（数组、链表）

**顺序存储的模板类代码：**

顺序表的封装需要三个属性：

1. 存储空间的起始位置。数组data的存储位置就是线性表存储空间的存储位置
2. 线性表的最大存储容量。数组长度MAXSIZE
3. 线性表的当前长度。length

在陈越的课程中C语言的写法是：

```c
typedef struct LNode *List;
struct LNode{
    ElementType Data[MAXSIZE];
    int Last;
};
```

####***顺序存储结构（数组）的实现方法：***

注意有一个问题解释数组下标从0开始，而存储数据从a1开始，差一个数据。

C++:

```cpp
const int MaxSize = 100;
template <class DataType>
class SeqList
{
public:
    SeqList(){length=0;}            //无参数构造方法
    SeqList(DataType a[],int n);    //有参数构造方法
    ~SeqList(){}                    //析构函数
    int Length(){return length;}    //线性表长度
    DataType Get(int i);            //按位查找
    int Locate(DataType x);         //按值查找
    void Insert(int i,DataType x);  //插入
    DataType Delete(int i);         //删除
    void PrintList();               //遍历
private:
    DataType data[MaxSize];         //顺序表使用数组实现
    int length;                     //存储顺序表的长度
};

//构造顺序表数组：
template <class DataType>
SeqList<DataType>::SeqList(DataType a[],int n)
{
    if(n>MaxSize) throw "wrong parameter";
    for(int i=0;i<n;i++)
        data[i]=a[i];
    length=n;
}

//按位查找：
template <class DataType>
SeqList<DataType>::Get(int n){
    if(i<0 && i>lenghth) throw "wrong Location";//throw的作用是抛出异常
	else return data[i-1];
}

//按值查找：
template <class DataType>
SeqList<DataType>::Locate(DataType x){
    for(it i=0;i<lenghth;i++)
        if(data[i] == x) return i+1;
	return 0;
}

//插入
template <class DataType>
SeqList<DataType>::Insert(int i,DataType x){
    if(length>=Maxsize) throw "wrong";
    if(i<1||i>length+1) throw "wrong";
    for(int j=length;j>i;j--)
   		data[j]=data[j-1];
    data[i-1]=x;
    length++;//最后总长度记得+1
}

//删除
template <class DataType>
SeqList<DataType>::Delete(int i){
    int x;
    if(length==0) throw "wrong";
    if(i<1||i>length+1) throw "wrong";
    for(int j=i;j<length;j++)
        data[j-1]=data[j];
    length--;
    return x;//把删掉这个数记录下来
}
```

数组顺序存储的优缺点：

**优点：**

- 随机访问特性，查找O(1)时间，存储密度高；
- 逻辑上相邻的元素，物理上也相邻；
- 无须为表中元素之间的逻辑关系而增加额外的存储空间；
- ==不用像用链表那样要实时的开辟动态空间，同时还要用深拷贝。==

**缺点：**

- 插入和删除需移动大量元素；
- 当线性表长度变化较大时，难以确定存储空间的容量；
- 造成存储空间的“碎片”



####***链式存储结构（链表）的实现方法：***

链表的定义是递归的，它或者为空null，或者指向另一个节点node的引用，这个节点含有下一个节点或链表的引用，线性链表的最后一个结点指针为“空”（通常用NULL或“^”符号表示）

```cpp
template<class DataType>
struct Node
{
    DataType data;              //存储数据,数据域
    Node<DataType> *next;       //存储下一个结点的地址，指针域
};

template<class DataType>
class LinkList
{
public:
    LinkList();                     
    LinkList(DataType a[], int n);  
    ~LinkList();                    
    int Length();                   
    DataType Get(int i);            
    int Locate(DataType x);         
    void Insert(int i, DataType x); 
    DataType Delete(int i);         
    void PrintList();               
private:
    Node<DataType> *first;          
};
```

**特点**：

- 用一组任意的存储单元存储线性表的数据元素， 这组存储单元可以存在内存中未被占用的任意位置
- 顺序存储结构每个数据元素只需要存储一个位置就可以了，而链式存储结构中，除了要存储数据信息外，还要存储它的后继元素的存储地址

```cpp
//无参构造：生成只有头节点的空链表：
template<class DataType>
LinkList<DataType>::LinkList()//构造函数
{
    first = new Node<Datatype>;//重新申请一块结点空间
    first->next = nullptr;
}

//析构函数
template<class DataType>
LinkList<DataType>::~LinkList()
{
    //将每个结点申请的内存全部删除
    while(first!=nullptr){
        Node<DataType>* q = first;
        first = first->next;
        delete q;
    }
}
```

**头插法构造单链表**

  头插法是每次将新申请的结点插在头结点后面
![这里写图片描述](https://img-blog.csdn.net/20180311152822301?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzA2MTE2MDE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

```cpp
template<class DataType>
LinkList<DataType>::LinkList(DataType a[], int n)
{
    first = new Node<DataType>;
    first->next = NULL;
    for (int i = 0; i < n; i++)
    {
        Node<DataType> *s = new Node<DataType>;
        s->data = a[i];
        s->next = first->next;
        first->next = s;
    }
}
```

**尾插法构造单链表**

  尾插法就是每次将新申请的结点插在终端节点的后面
<img src="https://img-blog.csdn.net/20180311152858388?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvcXFfMzA2MTE2MDE=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70" alt="这里写图片描述" style="zoom: 50%;" />

```cpp
template<class DataType>
LinkList<DataType>::LinkList(DataType a[], int n)
{
    first = new Node<DataType>;
    Node<DataType> *r = first;
    for (int i = 0; i < n; i++)
    {
        Node<DataType> *s = new Node<DataType>;
        s->data = a[i];
        r->next = s;
        r = s;
    }
    r->next = NULL;
}
```

**计算链表长度：**

```cpp
template<class DataType>
int LinkList<DataType>::Length(){
    Node<DataType> *p= first->next;
    int count = 0;
    while(p!=nullptr)
    	{p = p->next;
    	count++;}
    return count;
}
```

**按位查找：**

```cpp
template<class DataType>
int LinkList<DataType>::Get(int i){
    Node<DataType> *p = first->next;
    while (p != NULL && count<i)
    {
        p = p->next;
        count++;
    }
    if (p == NULL) throw "Location";
    else return p->data;
}

//按值查找
 int count = 1;
    while (p != NULL)
    {
        if (p->data == x) return count;
        p = p->next;
        count++;
    }
    return 0;
```

**插入：**

```cpp
template<class DataType>
void LinkList<DataType>::Insert(int i, DataType x)
{
    Node<DataType> *p = first;
    int count = 0;
    while(p != nullptr && count<i-1){
        p = p->next;
        count++;
    }
    if(p == NULL) throw "Location";
    else{
        Node<DataType> *s = new Node<DataType>;//申请新结点
        s->data = x;//数据域也要转移
        s->next = p->next;
        p-next = s;
    }
}
```

**删除：**要注意的是p == NULL || p->next == NULL

```c++
template<class DataType>
DataType LinkList<DataType>::Delete(int i)
{
    Node<DataType> *p = first;
    int count = 0;
    while (p != NULL && count<i - 1)
    {
        p = p->next;
        count++;
    }
    if (p == NULL || p->next == NULL) throw "Location";
    else {
        Node<DataType> *q = p->next;
        int x = q->data;
        p->next = q->next;
        return x;
    }
}
```

**遍历：**

```cpp
template<class DataType>
void LinkList<DataType>::PrintList()
{
	Node<DataType> *p = first;
    while(p !=NULL)
    {
        p = p->next;
        cout<<p->data<<endl;
    }
}
```



**有关双链表：**



#### 补充malloc和new的不同：

malloc和new的不同：

- 　从函数声明上可以看出。malloc 和 new 至少有两个不同: ***new 返回指定类型的指针，并且可以自动计算所需要大小。***比如：


```   c++
int *p;

p = new int; //返回类型为int* 类型(整数型指针)，分配大小为 sizeof(int);
//或

int* parr;

parr = new int [100]; //返回类型为 int* 类型(整数型指针)，分配大小为 sizeof(int) * 100;
```

 ***而 malloc 则必须由我们计算要字节数，并且在返回后强行转换为实际类型的指针。***

```cpp
int* p;
p = (int *) malloc (sizeof(int));
```

==malloc需要强制转换类型，自己指定大小。==

- new从自由存储区上分配内存，malloc从堆上分配内存；new/delete会调用构造函数/析构函数对对象进行初始化与销毁；operator new/delete可以进行重载；
- **new** 是c++中的操作符，**malloc**是c 中的一个函数

## 3堆栈（Stack）：

堆栈（Stack）：具有一定**操作约束**的线性表

- 只在一端（栈顶，Top）做插入、删除
- 插入数据：入栈（Push）//vector容器中入栈是`v.push_back();`
- 删除数据：出栈（Pop）
- 后入先出：Last In First Out（LIFO）

由于C++中本身包含了stack类（类模板），基本上stack类就可以满足我们的需求，所以很少需要我们自己建立堆栈

实例：

1. push(): 向栈内压入一个成员；//==stack容器用的是push不是push_back;==
2. pop(): 从栈顶弹出一个成员；
3. empty(): 如果栈为空返回true，否则返回false；
4. top(): 返回栈顶，但不删除成员；//==top不删除元素==
5. size(): 返回栈内元素的大小；

```cpp
#include<iostream>
#include<stack>
using namespace std;

int main()
{
    stack <int>stk;
    //入栈
    for(int i=0;i<50;i++){
        stk.push(i);//
    }
    cout<<"栈的大小:"<<stk.size()<<endl;
    while(!stk.empty())
    {
        cout<<stk.top()<<endl;
        stk.pop();
    }
    cout<<"栈的大小:"<<stk.size()<<endl;
    return 0;
}
```

 若为空栈顶元素则为-1，初始化的时候栈顶也设为-1，s.top = -1；Top指向Maxsize-1时表示满栈。最下面是0，最上面是Maxsize。

### 栈的顺序存储实现：

**有了stack之后一般不手撸栈**，此处为了强化一下理解所以手撸一下

栈的顺序存储结构通常由一个一维数组和一个记录栈顶元素位置的变量组成。

C++实现：

```cpp
#include <iostream>
using namespace std;
#define MAXSIZE 10
#define ERROR 0
#define OK 1
 
typedef int ElemType;
typedef struct{
    ElemType data[MAXSIZE];
    int  top;
}SqStack;
 
void Length(SqStack *S){
    S->top = -1;
}
 
int Push(SqStack *s , ElemType e){
    if(s -> top == MAXSIZE -1){    //栈满
        return ERROR;
    }
    s->top++;
    s->data[s->top] = e;
    return OK;
}
 
void show(SqStack *S){
    for(int i  = 0;i <= S->top;i++) {
        cout << S->data[i] << endl;
    }
}
 
int Pop(SqStack * S , ElemType *e){
    if(S->top == -1){
        return ERROR;
    }
    *e = S->data[S->top];
    S->top--;
    return OK;
}
 
int main(){
    SqStack S;
    Length(&S);
    while(-1) {
        cout << "1---往栈顶添加元素" << endl;
        cout << "2---显示栈元素" << endl;
        cout << "3---删除栈顶元素" << endl;
        int i, e ,w;
        cin >> i;
        switch (i) {
            case 1:
                cout << "请问你要加入的元素" << endl;
                cin >> e;
                Push(&S, e);
                break;
            case 2:
                show(&S);
                break;
            case 3:
                Pop(&S , &e);
                cout << "你清除了" << e << "这个元素" << endl;
                break;
        }
    }
 
}
```

### 栈的链式存储（链栈）

头文件：

```cpp
#include<iostream>
using namespace std;
class StackNode 
{
public:
	int  data;
	StackNode* next;//指向下一个结点的指针
};
class LinkStack 
{
public:
	LinkStack();
	~LinkStack();
	void Push(int x);//入栈
	int Pop();//出栈
	int GetTop();//获取栈顶元素
	bool Isempty();//判断是否为空
private:
	StackNode* top;//指向栈顶结点
};
```

源文件：

```cpp
#include<iostream>
#include"栈的链式存储.h"
using namespace std;

LinkStack()::LinkStack(){
    this->top = NULL;
}
LinkStack()::~LinkStack(){
    StackNode * p;
    while(top != NULL)
    {
        p=top;
        top=top->next;
        delete p;
    }
}
void LinkStack::Push(int x)//入栈
{
	StackNode* s = new StackNode;
	s->data = x;
	s->next = top;
	top = s;
}
int LinkStack::Pop()//出栈
{
	if (Isempty())
		cout << "空栈出啥呀" << endl;
	else
	{
		StackNode* n;
		int x;
		x = top->data;
		n = top;
		top = top->next;
		delete n;
		return x;
	}
}
int LinkStack::GetTop()//获取栈顶元素
{
	if (top != NULL)
		return top->data;
}
bool LinkStack::Isempty()
{
	if (top == NULL)
		return true;
	else return false;
}
```



## 4队列

- 插入和删除操作：只能在一端（front）插入，而在另一端（rear）删除

- 数据插入：入队列（AddQ）

- 数据删除：出队列（DeleteQ）

- 先进先出：FIFO

- 首先C++也是给了标准的模板来直接创建队列的：

  queue 的基本操作有：
  入队，如例：q.push(x); 将x 接到队列的末端。
  出队，如例：q.pop(); 弹出队列的第一个元素，注意，并不会返回被弹出元素的值。
  访问队首元素，如例：q.front()，即最早被压入队列的元素。
  访问队尾元素，如例：q.back()，即最后被压入队列的元素。
  判断队列空，如例：q.empty()，当队列空时，返回true。
  访问队列中的元素个数，如例：q.size()

  ```cpp
  #include <queue>
  int main()
  {
      queue<int> q;
      q.push(4);
      q.push(5);
      printf("%d\n",q.front());
      q.pop();
  }
  ```

  

### 队列的顺序存储实现：

队列的顺序存储结构通常由一个一维数组和一个记录队列头元素位置的变量 front 以及一个记录队列尾元素位置的变量 rear 组成，其中 front 指向整个队列的头一个元素的再前一个，rear 指向的是整个队列的最后一个元素，从 rear 入队，从 front 出队，且仅使用 n-1 个数组空间。==front是队头，rear是队尾，从头删除从尾加入。==

判断队列是否已满的方法：

```cpp
return ((Q->rear+1) % MaxSize == Q->front);
```

采用基于数组的方式来实现队列，为了合理利用所有空间，采用环形队列的方式进行实现，此处初始化时rear=0，front=1。

<img src="https://img-blog.csdnimg.cn/20200724210236264.png#pic_center" alt="img" style="zoom: 33%;" />

这里对为什么要多加一个空间做一下解释：首先对于队列中元素个数的计算方式为size = (rear+maxSize-front+1)%maxSize（简化起见，==size = rear-front+1==，其它计算方法实质都一样，取决于环形队列rear和front设计方式），==假设我们需要一个能够存储n个元素的队列且只开辟一个大小为n的数组，那么size的所有可能取值为0，1，2，…，n，共有n+1种结果，而rear-front+1的值为0，1，n-1只能表示n种情况，所以需要多一个空间才能表示n+1种结果。==


C++的实现代码：

```cpp
#include<iostream>
#include<string>
using namespace std;

template<class T>
class Myqueue{
private:
    int front;   //头元素下标
    int rear;    //尾元素下标
    int maxSize; //队列总空间大小
    T *array;
public:
    Myqueue(int size = 10) //构造函数
    {
        front = 1;
        rear = 0;
        maxSize = size + 1;//多一个位置来表示n-1种结构，循环数组
        array = new T[maxSize];
    }
      
    T back()//输出队尾
    {
        if (empty())
        {
            cout << "队列为空" << endl;
            return NULL;
        }
        return array[rear];
        
    bool empty()
    {
        if (size() == 0)
            return true;
        else 
            return false;
    }

    T frontValue()
    {
        if (empty())
        {
            cout << "队列为空" << endl;
            return NULL;
        }
        else
        {
            return array[front];
        }
    }

    void pop()
    {
        if (empty())
            cout << "队列已经为空" << endl;
        else
            front = (front + 1) % maxSize;
    }

    void push(T value)
    {
        if (size() == maxSize - 1)
        {
            cout << "队列已满，无法继续添加元素" << endl;
        }
        else
        {
            rear = (rear + 1) % maxSize;
            array[rear] = value;
        }
    }

    int size()
    {
        return (rear + maxSize - front + 1) % maxSize;
    }
};

int main()
{
    Myqueue<string> q(5);
    q.push("abc");
    q.push("def");
    q.push("ghi");
    q.push("jkl");
    q.push("mno");
    q.push("pqr");
    int len = q.size();
    cout << q.back() << endl;
    for (int i = 0; i < len; i++)
    {
        cout << q.frontValue() << endl;
        q.pop();
    }
    cout << q.empty() << endl;
    return 0;
}
```



### 队列的链表实现：

采用链表的方式，用front指向队列头结点，用rear指向队列尾结点，每添加一个元素就在链后加一个结点并将其设为rear，每删除一个元素就将front设置为原front的下一个结点，并将原front结点删除，和栈的实现较为类似

```cpp
#include <iostream>
#include <string>
using namespace std;

template <typename T>
class Node
{
public:
    T value;
    Node *next;
    Node(T value, Node* next = NULL)
    {
        this->value = value;
        this->next = next;
    }
};

template <typename T>
class Myqueue
{
private:
    Node<T> *front;
    Node<T> *rear;
    int length;

public:
    Myqueue()
    {
        front = rear = NULL;
        length = 0;
    }

    T back()
    {
        if (empty())
        {
            cout << "队列为空" << endl;
            return NULL;
        }
        return rear->value;
    }

    bool empty()
    {
        if (size() == 0)
            return true;
        return false;
    }
    T frontValue()
    {
        if (empty())
        {
            cout << "队列为空" << endl;
            return NULL;
        }
        else
            return front->value;
    }

    void pop()
    {
        if (empty())
            cout << "队列已经为空" << endl;
        else
        {
            Node<T> *temp = front;
            front = front->next;
            if (rear == temp)
                rear = front;
            delete (temp);
            length--;
        }
    }

    void push(T value)
    {
        length++;
        if (length == 1)
        {
            front = new Node<T>(value, NULL);
            rear = front;
        }
        else
        {
            rear->next = new Node<T>(value, NULL);
            rear = rear->next;
        }
    }

    int size()
    {
        return length;
    }
};


int main()
{
    Myqueue<string> q;
    q.push("abc");
    q.push("def");
    q.push("ghi");
    q.push("jkl");
    q.push("mno");
    q.push("pqr");
    int len = q.size();
    cout<<len<<endl;
    cout << q.back() << endl;
    for (int i = 0; i < len; i++)
    {
        cout << q.frontValue() << endl;
        q.pop();
    }
    cout << q.empty() << endl;
    return 0;
}
```



### 剑指21：合并两个有序链表：

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode* header = new ListNode(-1);
        ListNode* cur = header;
        //定义链表三的虚拟头节点，定义一个指针指向链表3的虚拟头节点
        while(list1 != nullptr && list2 != nullptr){
            if(list1->val <= list2->val){
                cur->next = list1;
                list1 = list1->next;
            }
            else
            {
                cur->next =list2;
                list2 = list2->next;
            }
            cur = cur->next;
        }
        cur->next = list1 == NULL ? list2 : list1;//表示的是某个链表走到头了

        return header->next;
        //返回链表3虚拟节点的下一位，就可以输出最终的合并结果。
    }
};
```

打印链表操作：

```cpp
//打印链表
void` `printLinkedList(ListNode* head)
{
 ``while``(head)//只要不为空就打印
 ``{
  ``cout<<head->value<<``" "``;
  ``head=head->next;
 ``}
 ``cout<<endl;
}
```

### 剑指24：反转链表：

双指针解法：两个指针先从nullptr和头结点开始转换位置，然后向后进行。

![image-20221010212328127](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221010212328127.png)

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode * cur = head, *pre = nullptr;
        while(cur != nullptr){
            ListNode* tmp = cur->next;
            cur->next = pre;
            pre = cur;
            cur = tmp;
        }
        return pre;
        //最终pre指向原链表的尾节点，新链表的头节点
    }
};
```

递归实现

```cpp
class Solution {
public:
ListNode* reverse(ListNode* pre, ListNode* cur) {
    if(cur == nullptr) return pre;
    ListNode* temp = cur->next;
    cur->next = pre;
    pre = cur;
    cur = temp;
    return reverse(pre, cur);
}

ListNode* reverseList(ListNode* head) {
    return reverse(nullptr, head);
}
};


*****************正宗写法*************
    class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        return recur(head, nullptr);           // 调用递归并返回
    }
private:
    ListNode* recur(ListNode* cur, ListNode* pre) {
        if (cur == nullptr) return pre;// 终止条件
        ListNode* res = recur(cur->next, cur); // 递归后继节点
        cur->next = pre;// 修改节点引用指向
        return res;// 返回反转链表的头节点
    }
};
```

### 剑指42：连续子数组的最大和

动态规划：

```cpp
int maxSubArray3(std::vector<int> &nums) {
    assert(!nums.empty());

    int n = nums.size();
    int maxSum = nums[0];

    // 如果当前值小于0，
    // 重新开始(全局最大值更新)
    for (int i = 1; i < n; i++) {
        // 更新当前的最大值
        if (nums[i - 1] > 0) {
            nums[i] += nums[i - 1];
        }
        // 更新全局的最大值
        maxSum = std::max(nums[i], maxSum);
    }

    return maxSum;
}
```

贪心算法：

```cpp
int Solution42::maxSubArray(std::vector<int> &nums) {
    assert(!nums.empty());

    int resSum = INT_MIN;//一开始要把max设置尾最小值，整数的最小值，防止有负数出现
    int curSum = 0;

    // 遍历数组
    for (int i = 0; i < nums.size(); i++) {
        // 当sum小于0时，就从下一个数重新开始
        // 同时更新每次叠加的最大值
        if (curSum <= 0) {
            curSum = nums[i];
        } else {
            // 和大于0时
            curSum += nums[i];
        }

        // 不断更新子串的最大值
        if (curSum > resSum) {
            resSum = curSum;
        }
    }

    return resSum;
}
```

### 剑指31：栈的压入、弹出序列

 遇到一样的马上弹出来：

```cpp
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        stack<int> st;
        int n = pushed.size();
        for (int i = 0, j = 0; i < n; i++) {
            st.emplace(pushed[i]);
            while (!st.empty() && st.top() == popped[j]) {
                st.pop();
                j++;
            }
        }
        return st.empty();
    }
};
```





## 5树

线性表的缺点：不管是用链表还是数组实现，都避免不了线性的时间复杂度问题。

树的特点：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221015144717068.png" alt="image-20221015144717068" style="zoom:67%;" />

==一棵N个结点的树有N-1条边==，除根结点外每个结点有且仅有一个父节点。

![image-20221015145601694](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221015145601694.png)



二叉树概念：

一个实数域，两个指针域：

<img src="https://img-blog.csdnimg.cn/20181026114920772.jpg" alt="img" style="zoom:80%;" />

- 完美二叉树：
- ![image-20221015145910186](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221015145910186.png)
- 完全二叉树：有n个结点的二叉树，对树中结点按从上至下、从左到右的顺序进行编号，编号为i的结点必须和满二叉树中位置相同。

![image-20221015150554362](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221015150554362.png)



####二叉树的存储结构：

#####1.顺序存储结构（数组）：

==重点在于：左子树 == 根节点*2+1、右子树 == 根节点`*`2+2==

利用完全二叉树形式来表示，每个结点都表示出来，如果非完美二叉树就很浪费空间。

<img src="https://img-blog.csdnimg.cn/20181026115134161.jpg" alt="img" style="zoom:50%;" />

```cpp
#include <iostream>
#include <vector>

using namespace std;
```

**可以直接定义树的类，不像链式存储需要定义结点那样：**

```cpp
template<class T>
class CMyTreeArr{
   vector<T> vecBuff; 
   CMyTreeArr();		// 默认构造函数
   ~CMyTreeArr();  		// 析构函数

   void clear();	 	// 清空数 方便操作
   void initTree(T arr[], size_t len);		// 初始化
   bool find_data(T const& findVal);	// 查找
   void appendNode(T const& data);		// 增加结点
    
   // 四种遍历方式
   // 默认从第一个元素开始遍历  下标为 0  （数组）
   void prePrint(int index = 0);		// 前序遍历
   void inPrint(int index = 0);		// 中序遍历
   void posPrint(int index = 0);		// 后序遍历
   void levelPrint();				// 层级遍历    依次输出值就行
};
```

类外实现类的方法：

==类模板在成员函数类外实现时，需要加上模板参数列表==

```cpp
template<class T>
inline CMyTreeArr<T>::CMyTreeArr(){
    vecBuff.clear();  // 初始化清空
}
template<class T>
inline CMyTreeArr<T>::CMyTreeArr(){
    clear();
template<typename T>
inline void CMyTreeArr<T>::clear()
{
    vecBuff.clear();		// vector 类的成员函数   直接调用 
}
template<typename T>
inline void CMyTreeArr<T>::initTree(T arr[], size_t len){
    for(int i=0;i<len;i++)
    {	
        vecBuff.clear();
        vecBuff.push_back(a[i]);
    }
}
template<typename T>
inline bool CMyTreeArr<T>::find_data(T const& findVal){
    auto iter = find(vecBuff.begin(),vecBuff.end(),findVal);
   	return !(iter == vecBuff.end());
}
    
```

**先序遍历：**

```cpp
inline void CMyTreeArr<T>::prePrint(int index){
    if(index>=0 && index<vecBuff.size()){
        cout<<vecBuff[index]<<" ";  //输出根节点
        prePrint(2* index +1);//左子树递归
        prePrint(2*index +2);//右子树递归
    }
}
```

**中序遍历：**

```cpp
template<typename T>
inline void CMyTreeArr<T>::inPrint(int index){
   if(index < vecBuff.size() && index >= 0)
   {
       inPrint(index*2+1);
       cout<<vecBuff[index]<<" ";
       inPrint(index*2+2);
   }
}
```

**后续遍历：**

```cpp
template<typename T>
inline void CMyTreeArr<T>::posPrint(int index)
{
    if(index < vecBuff.size() && index >= 0)
    {
        inPrint(2 * index + 1);
        inPrint(2 * index + 2);
        cout << vecBuff[index] << " ";
    }
}
```

**层序遍历：**

```cpp
template<typename T>
inline void CMyTreeArr<T>::posPrint(int index)
{
    if(index < vecBuff.size() && index >= 0)
    {
        inPrint(2 * index + 1);
        inPrint(2 * index + 2);
        cout << vecBuff[index] << " ";
    }
}
```

**调用程序：**

```cpp
int main(){
    CMyTreeArr<int> *MyTreeTwo = new CMyTreeArr<int>();
    int arr[]{ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15 };

    int nSize = sizeof(arr) / sizeof(arr[0]);		// 求出数组长度的一种方法

    MyTreeTwo->initTree(arr, nSize);
}
```



**inline补充**：inline是C++关键字，==在函数声明或定义中，函数返回类型前加上关键字inline，即可以把函数指定为内联函数==。***这样可以解决一些频繁调用的函数大量消耗栈空间（栈内存）的问题。***关键字inline必须与函数定义放在一起才能使函数成为内联函数，仅仅将inline放在函数声明前面不起任何作用。inline是一种“用于实现”的关键字，而不是一种“用于声明”的关键字。

主要总结：让函数指定为内联函数，解决频繁调用的函数大量消耗空间（栈内存）的问题。



##### 2.链式存储结构：（层序遍历用的queue）

**建立好结点模板：**

```cpp
#include <iostream>
#include <deque> // 下面的层级遍历的算法需要用到队列

using namespace std;

template <typename T>
struct TreeNode
{
    T			data;		// 数据域
    TreeNode*	lchild;		// 左子结点指针域
    TreeNode*	rchild;		// 右子结点指针域

    // 结构体构造初始化
    // C++里面   结构体和类没有本质   只是少了限定修饰符
    TreeNode() : data(0), lchild(nullptr), rchild(nullptr) {}
};
```



实现树的链式存储：

```cpp
template <typename T>
class CMyTreeList
{
    TreeNode<T>* pRoot;		// 只需要一个根结点作为数据存储  就能找到所有的左子树 和右子树

public:
    CMyTreeList();		// 默认构造
    ~CMyTreeList();		// 析构

    // len 数组的长度	index从哪个位置初始化
    TreeNode<T>* initTree(T arr[], size_t len, int index = 0);	 // 默认从0 开始初始化
    
private:
    // 按引用访问树  提高效率	  
    // clear 不加&  可以导致内存崩溃  
    void clear(TreeNode<T>*& root);		// 清空树	
    void prePrint(TreeNode<T>*& root);		// 前序遍历
    void inPrint(TreeNode<T>*& root);		// 中序遍历
    void posPrint(TreeNode<T>*& root);		// 后序遍历
    void levelPrint();  			// 层级遍历	不需要参数

public:
    // 因为类外不能访问私有成员	
    // 所有我们重载上述几种访问私有成员的方法  将他们封装起来
    void clear();  		// 清空树  方便操作
    
    void prePrint();		// 前序遍历
    void inPrint();		// 中序遍历
    void posPrint();		// 后序遍历
};
```



树成员的实现方法：

```cpp
template <typename T>
inline CMyTreeLise<T>::CMyTreeList()
{
    pRoot = nullptr;		// 直接置空
}

template <typename T>
inline CMyTreeLise<T>::~CMyTreeList()
{
    clear();			// 清空树  释放内存
}

template <typename T>
inline void CMyTreeLise<T>::clear(TreeNode<T>*& root){
    if(root){
        clear(root->lchild);
        clear(root->rchild);
        
        delete root;
        root = nullptr;
    }

template <typename T>
inline TreeNode<T>* CMyTreeLise<T>::initTree(T arr[], size_t len, int index)
{
    if(index >=len)
    {return nullptr;}
    
    TreeNode<int>* tempNode = new TreeNode<T>; //new + 数据类型
    //递归使用前序遍历方式初始化
    temNode ->data = arr[index];
    temNode ->lchild = initTree(arr,len,index*2+1);
    temNode ->rchild = initTree(arr,len,index*2+2);
    pRoot = tempNode;
    return pRoot;
}
    
template<typename T>
inline void CMyTreeList<T>::prePrint()		// 前序遍历
{
    prePrint(pRoot);
}

template<typename T>
inline void CMyTreeList<T>::prePrint(TreeNode<T>*& root)   {
    if(root){
  		cout << root->data << " ";		// 依次输出根  左子树  右子树 
        prePrint(root->lchild);
        prePrint(root->rchild);
    }
}

template<typename T>
inline void CMyTreeList<T>::inPrint()  		// 中序遍历
{
    inPrint(pRoot);  
}

template<typename T>
inline void CMyTreeList<T>::inPrint(TreeNode<T>*& root)
{
    if (root)  // 判断是否存在 
    {
        prePrint(root->lchild);  		 // 依次输出左子树 根 右子树 
        cout << root->data << " ";  
        prePrint(root->rchild);
    }
}

template <typename T>
inline void CMyTreeList<T>::posPrint()		// 后序遍历
{
    posPrint(pRoot);
}

template <typename T>
inline void CMyTreeList<T>::posPrint(TreeNode<T>*& root)
{
    if (root)
    {
        prePrint(root->lchild);			// 依次输出左子树 右子树 根
        prePrint(root->rchild);
        cout << root->data << " ";
    }
}
```

链式结构的层序遍历：要使用队列

```cpp
template <typename T>
inline void CMyTreeList<T>::levelPrint()
{
    deque<TreeNode<T>*>* deq = new deque<TreeNode<T>*>;  	// 双端队列  也可以用 queue
  
    TreeNode<T>* root = pRoot;		// 保存根   队列的头结点 
    deq->push_back(root);		// 根结点入列

    while(!deq->empty())		// 不是空列   一直循环
    {
        root = deq->front();		// 保存头结点 
        cout << root->data << " ";	// 输出头结点 
        deq->pop_front();		// 头结点 出列

        if (root->lchild)		// 如果有左子树，则入列
        {
            deq->push_back(root->lchild);
        }
        if (root->rchild)		// 如果有右子树，则入列
        {
            deq->push_back(root->rchild);
        }
    }
    
}
```







### 4种二叉树的遍历很重要！！！

![image-20221015153648687](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221015153648687.png)

总结：

先序、中序和后序遍历过程：遍历过程中经过结点的路线一样，只是访问各结点的时机不同，即：

- 先序遍历是第一次"遇到"该结点时访问
- 中序遍历是第二次"遇到"该结点（此时该结点从左子树返回）时访问
- 后序遍历是第三次"遇到"该结点（此时该结点从右子树返回）时访问

![img](https://img-blog.csdnimg.cn/20181030202857229.jpg)

==递归的实质是使用了堆栈==

**由两种遍历序列确定二叉树：必须包含中序遍历才可以唯一确定。没有中序（仅前后序）不行**





### 二叉搜索树（BST），也叫二叉排序树/二叉查找树

定义：

 二叉搜索树（BST）也称二叉排序树或二叉查找树

二叉搜索树：一棵二叉树，可以为空；如果不为空，满足以下性质：

1. 非空**左子树**的所有键值**小于**其根结点的键值
2. 非空**右子树**的所有键值**大于**其根结点的键值
3. 左、右子树都是二叉搜索树

![img](https://img-blog.csdnimg.cn/20181101090543537.jpg)

查找和查找最大最小都比较简单，查找就和目前结点比，如果小，往左递归，如果大往右递归。

最大元素在书的最右分支的端节点上，最小元素一定在树的最左分支上。

**删除很麻烦：**

删除的结点有左、右两棵子树：要用另外一个结点代替被删除的结点：

- 取右子树中最小元素
- 或者取左子树中最大元素



二叉搜索树的建立：

重要的是==插入和删除==

```cpp
#include<iostream>
#include<malloc.h>
using namespace std;
typedef int ElementType;
typedef struct TreeNode *BinTree;
struct TreeNode{
	ElementType Data;
	BinTree Left;
	BinTree Right;
};

// 查找递归实现 
BinTree Find(ElementType X,BinTree BST){
	if(!BST)  // 如果根结点为空，返回 NULL 
		return NULL; 
	if(X < BST->Data) // 比根结点小，去左子树查找 
		return Find(X,BST->Left); 
	else if(BST->Data < X)  // 比根结点大，去右子树查找 
		return Find(X,BST->Right);
	else if(BST->Data == X) // 找到了 
		return BST;
}

// 查找非递归实现
BinTree IterFind(ElementType X,BinTree BST){
	while(BST){
		if(X < BST->Data)
			BST = BST->Left;
		else if(BST->Data < X)  // 比根结点大，去右子树查找 
			BST = BST->Right;
		else if(BST->Data == X) // 找到了 
			return BST;
	}
	return NULL;
} 
//非递归的实质就是while(BST){if(x< BST->Data){BST=BST->Left}}


// 查找最小值的递归实现
BinTree FindMin(BinTree BST){
	if(!BST)    // 如果为空了，返回 NULL 
		return NULL;  
	else if(BST->Left)   // 还存在左子树，沿左分支继续查找 
		return FindMin(BST->Left);
	else  // 找到了 
		return BST;
} 

// 查找最大值的非递归实现
BinTree FindMax(BinTree BST){
	if(BST)  // 如果不空 
		while(BST->Right)   // 只要右子树还存在 
			BST = BST->Right;
	return BST;
} 

// 插入
BinTree Insert(ElementType X,BinTree BST){
	if(!BST){  // 如果为空，初始化该结点 
		//BST = (BinTree)malloc(sizeof(struct TreeNode));
        BST = new BinTree；
		BST->Data = X;
		BST->Left = NULL;
		BST->Right = NULL;
	}else{ // 不为空 
		if(X < BST->Data)  // 如果小，挂在左边 
			BST->Left = Insert(X,BST->Left);
		else if(BST->Data < X)  // 如果大，挂在右边 
			BST->Right = Insert(X,BST->Right);
		// 如果相等，什么都不用做 
	}
	return BST;
} 

// 删除
BinTree Delete(ElementType X,BinTree BST){
	BinTree tmp;
	if(!BST)
		cout<<"要删除的元素未找到";
	else if(X < BST->Data)   // X 比当前结点值小，在左子树继续查找删除 
		BST->Left = Delete(X,BST->Left);
	else if(BST->Data < X)   // X 比当前结点值大，在右子树继续查找删除 
		BST->Right = Delete(X,BST->Right);
	else{  //  找到被删除结点 
		if(BST->Left && BST->Right){  // 被删除结点有俩孩子结点 
			tmp = FindMin(BST->Right);   // 找到右子树中值最小的
			BST->Data = tmp->Data;     // 用找到的值覆盖当前结点 
			BST->Right = Delete(tmp->Data,BST->Right);    // 把前面找到的右子树最小值结点删除 
		}else{  // 被删除结点只有一个孩子结点或没有孩子结点 
			tmp = BST;
			if(!BST->Left && !BST->Right)  // 没有孩子结点 
				BST = NULL;
			else if(BST->Left && !BST->Right)  // 只有左孩子结点 
				BST = BST->Left;
			else if(!BST->Left && BST->Right)  // 只有右孩子结点 
				BST = BST->Right;
			free(tmp);
		}
	}
	return BST;
} 

// 中序遍历 
void  InOrderTraversal(BinTree BT){
	if(BT){
		InOrderTraversal(BT->Left);  // 进入左子树 
		cout<<BT->Data;  // 打印根 
		InOrderTraversal(BT->Right);  // 进入右子树 
	}
}
int main(){
	BinTree BST = NULL;
	BST = Insert(5,BST); 
	BST = Insert(7,BST); 
	BST = Insert(3,BST); 
	BST = Insert(1,BST); 
	BST = Insert(2,BST); 
	BST = Insert(4,BST); 
	BST = Insert(6,BST); 
	BST = Insert(8,BST); 
	BST = Insert(9,BST); 
	/*
			    5
			   /\
			  3  7
             /\	 /\
            1 4 6  8
			\      \
			 2      9
	*/
	cout<<"中序遍历的结果是："; 
	InOrderTraversal(BST);
	cout<<endl;
	cout<<"查找最小值是："<<FindMin(BST)->Data<<endl;
	cout<<"查找最大值是："<<FindMax(BST)->Data<<endl; 
	cout<<"查找值为3的结点左子树结点值为："<<Find(3,BST)->Left->Data<<endl;
	cout<<"查找值为7的结点右子树结点值为："<<IterFind(7,BST)->Right->Data<<endl;
	cout<<"删除值为5的结点"<<endl;
	Delete(5,BST);
	/*
			    6
			   /\
			  3  7
             /\	  \
            1 4    8
			\      \
			 2      9
	*/
	cout<<"中序遍历的结果是："; 
	InOrderTraversal(BST);
	cout<<endl;
	return 0;
}
```



另一种好懂一点的：

```cpp
#include <iostream>
using namespace std;

// 二叉树的节点结构体
struct node {	
	int data;	  // 数据域 
	node* lchild; // 指针域：左孩子
	node* rchild; // 指针域：右孩子
};

// 创建新节点
node* newNode(int v) {
    node* Node = new node;
    Node->data = v;
    Node->lchild = Node->rchild = nullptr;
    return Node;
}

// 二叉查找树的查找操作
bool search(node* root, const int& val) {
	if (root == nullptr)   return false;
	if (root->data == val) return true;
	else if (root->data > val) {
		search(root->lchild, val);
	} else {
		search(root->rchild, val);
	}
}

// 二叉查找树的插入操作
void insert(node* root, const int& val) {
	if (root == nullptr) {
		root = newNode(val);
	}

	if (root->data == val) {
		return; // 已经有相同的值
	} else if (root->data > val) {
		insert(root->lchild, val);
	} else {
		insert(root->rchild, val);
	}
}

// 二叉查找树的建立
node* create(vector<int>& data) {
	node* root = nullptr;
	for (auto& iter : data) {
		insert(root, iter);
	}
	return root;
}

// 二叉查找树的删除
/*
	为保证删除某一个节点之后仍然为一个二叉查找树，
	一种方法是，找到删除节点的左子树中的最大值，替换掉删除的节点
	另一种方法是，找到删除节点的右子树中的最小值，替换掉删除的节点
	替换的方法是进行删除节点的递归操作
*/

// 传入的是左孩子节点，找到左子树中的最大值，
node* GetLeftMax(node* root) {
	while (root != nullptr) {
		root = root->rchild;
	}
	return root; 
}

// 传入的是右孩子节点，找到右子树中的最小值，
node* GetRightMin(node* root) {
	while (root != nullptr) {
		root = root->lchild;
	}
	return root; 
}

// 二叉查找树的删除操作
void deleteNode(node* &root, int& val) {
	if (root == nullptr) return;
	if (root->data > val) {
		deleteNode(root->lchild, val);
	} else if (root->data < val) {
		deleteNode(root->rchild, val);
	} else {
		if (root->lchild == nullptr && root->rchild == nullptr) {
			delete root;	// 释放内存
			root = nullptr; // 指针置空
		} else if (root->lchild != nullptr) { 
			node* pre = GetLeftMax(root->lchild);
			root->data = pre->data; // 使用前驱节点替换要删除的节点
			deleteNode(root->lchild, pre->data); // 递归删除掉替换的节点
		} else if (root->rchild != nullptr) { 
			node* post = GetRightMin(root->rchild);
			root->data = post->data; // 使用后继节点替换要删除的节点
			deleteNode(root->rchild, post->data); // 递归删除掉替换的节点
		}
	}
}

int main() {
	
	return 0;
}
```



###平衡二叉树（AVL）

也要是一棵BST（二叉搜索树）

要尽可能使树的深度小一点：

如何求树的深度：

```cpp
int  GetHeight(BinTree BT){
    int max,hl,hr;
    if(BT){
        hl = GetHeight(BT->Left);
        hr = GetHeight(BT->Right);
        max=(hl>hr)?hl:hr;
        max++;
        return max;
    }
    else{return 0;}
}
```

平衡因子（Balance  Factor，BF）：BF（T）=hL-hR（左树高度-右树高度）

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220929153457033.png" alt="image-20220929153457033" style="zoom:50%;" />

必须！每一个！结点的左右子树的平衡因子绝对值不超过1



== 最少结点数：n~h~=n~h-1~+n~h-2~+1，高度为h==

==给定结点数为n的AVL树的最大高度为h=O（log~2~n）==

**重要的是平衡二叉树的调整：**

比较简单的两种就是

1. **RR旋转：**

当"插入结点"(BR)是"被破坏平衡结点"(A)**右子树**的**右子树**时，即 RR 插入时，采用 RR 旋转调整
![img](https://img-blog.csdnimg.cn/20181102110800268.jpg)

其基本思路是把 B 的左子树腾出来挂到 A 的右子树上，返回 B 作为当前子树的根。

```cpp
AVLTree RRRotation(AVLTree A){
	AVLTree B = A->right;   // B 为 A 的右子树  
	A->right = B->left;    // B 的左子树挂在 A 的右子树上 
	B->left = A;   //  A 挂在 B 的左子树上 
	return B;  // 此时 B 为根结点了   
}
```

2. **LL旋转**

当"插入结点"(BL)是"被破坏平衡结点"(A)**左子树**的**左子树**时，即 LL 插入，采用 RR 旋转调整
![img](https://img-blog.csdnimg.cn/20181102112405164.jpg)
其基本思路是把 B 的右子树腾出来挂到 A 的左子树上，返回 B 作为当前子树的根

```cpp
AVLTree LRRotation(AVLTree A){
    AVLTree B = A->lefr;
    A->left=B->right;
    B->right=A;
    return B;
}
```



比较难的LR双旋和RL双旋：

1.**LR双旋：（左边结点先RR，然后根结点LL）**

当"插入结点"(CL 或者 CR)是"被破坏平衡结点"(A)**左子树**的**右子树**时，即 LR 插入，采用 LR 旋转调整
![img](https://img-blog.csdnimg.cn/20181102112415831.jpg)
基本思想是先将 B 作为根结点进行 **RR 单旋**转化为 LL 插入，再将 A 作为根结点进行 **LL 单旋**（先 RR 再 LL)

```	cpp
AVLTree LRRotation(AVLTree A){
	// 先 RR 单旋
	A->left = RRRotation(A->left);//先以右节点为根节点LL
	// 再 LL 单旋 
	return LLRotation(A); //再以原根结点为根RR
}

```





2.**RL双旋：（右边的结点先LL，后以根结点RR）**

当"插入结点"(CL 或者 CR)是"被破坏平衡结点"(A)**右子树**的**左子树**时，即 RL 插入，采用 RL 旋转调整
![img](https://img-blog.csdnimg.cn/20181102112435166.jpg)
基本思想是先将 B 作为根结点进行 **LL 单旋**转化为 RR 插入，再将 A 作为根结点进行 **RR单旋**（先 LL 再 RR）

```cpp
AVLTree RLRotation(AVLTree A){
	// 先 LL 单旋
	A->right = LLRotation(A->right);//先以右节点为根节点LL
	// 再 RR 单旋 
	return RRRotation(A); //再以原根结点为根RR
}

```





![image-20221016151911250](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221016151911250.png)



#### 习题Root of AVL Tree

```cpp
#include<iostream>
#include<malloc.h>
typedef struct AVLNode *AVLTree;
struct AVLNode{
	int data;     // 存值 
	AVLTree left;  // 左子树 
	AVLTree right;  // 右子树 
	int height;  // 树高 
};
using namespace std;

// 返回最大值 
int Max(int a,int b){
	return a>b?a:b;
}

// 返回树高，空树返回 -1 
int getHeight(AVLTree A){
	return A==NULL?-1:A->height;
}

// LL单旋
// 把 B 的右子树腾出来挂给 A 的左子树，再将 A 挂到 B 的右子树上去 
AVLTree LLRotation(AVLTree A){
	// 此时根节点是 A 
	AVLTree B = A->left;  // B 为 A 的左子树  
	A->left = B->right;   // B 的右子树挂在 A 的左子树上 
	B->right = A;     //  A 挂在 B 的右子树上 
	A->height = Max(getHeight(A->left),getHeight(A->right)) + 1;
	B->height = Max(getHeight(B->left),A->height) + 1;
	return B;  // 此时 B 为根结点了 
}

// RR单旋
AVLTree RRRotation(AVLTree A){
	// 此时根节点是 A 
	AVLTree B = A->right;
	A->right = B->left;
	B->left = A;
	A->height = Max(getHeight(A->left),getHeight(A->right)) + 1;
	B->height = Max(getHeight(B->left),A->height) + 1;
	return B;  // 此时 B 为根结点了 
}

// LR双旋 
AVLTree LRRotation(AVLTree A){
	// 先 RR 单旋
	A->left = RRRotation(A->left);
	// 再 LL 单旋 
	return LLRotation(A);
}

// RL双旋
AVLTree RLRotation(AVLTree A){
	// 先 LL 单旋
	A->right = LLRotation(A->right);
	// 再 RR 单旋 
	return RRRotation(A); 
}

AVLTree Insert(AVLTree T,int x){
	if(!T){  // 如果该结点为空，初始化结点 
		T = (AVLTree)malloc(sizeof(struct AVLNode));
		T->data = x;
		T->left = NULL;
		T->right = NULL;
		T->height = 0;
	}else{  // 否则不为空， 
		if(x < T->data){  // 左子树 
			T->left = Insert(T->left,x);
			if(getHeight(T->left)-getHeight(T->right)==2){  // 如果左子树和右子树高度差为 2 
				if(x < T->left->data)  // LL 单旋 
					T = LLRotation(T); 
				else if(T->left->data < x)  // LR双旋
					T = LRRotation(T); 
			}
		}else if(T->data < x){
			T->right = Insert(T->right,x);
			if(getHeight(T->right)-getHeight(T->left)==2){
				if(x < T->right->data)  // RL 双旋 
					T = RLRotation(T); 
				else if(T->right->data < x)  // RR单旋
					T = RRRotation(T); 
			}
		}
	}
	//更新树高 
	T->height = Max(getHeight(T->left),getHeight(T->right)) + 1;
	return T;
} 


int main(){
	AVLTree T=NULL;
	int n;
	cin>>n;
	for(int i=0;i<n;i++){
		int tmp;
		cin>>tmp;
		T = Insert(T,tmp);
	}
	cout<<T->data;
	return 0;
}
```





#### 堆

优先队列（priority Queue）：特殊的"队列"，取出元素的顺序是依照元素的优先级（关键字）大小，而不是元素进入队列的先后顺序，以**完全二叉树**存储



堆主要用：完全二叉树来表示，因为有优先级，所以最上面肯定是最大的活最小的，要让他们先出。

需要同时满足：==完全二叉树+小顶/大顶==

堆有两个特性：

- 结构性：==用数组表示的完全二叉树==
- 有序性：任一结点的关键字是其子树所有结点的最大（最小）值
  - 最大堆：也称大顶堆：最大值
  - 最小堆：也称小顶堆：最小值

```cpp
//最大堆
#include<stdio.h>
#include<malloc.h>
#define MaxData 100000
#define ERROR -1
typedef int ElementType;
typedef struct HeapStruct *MaxHeap;
struct HeapStruct{
	ElementType *Elements;   // 存储堆元素的数组 
	int Size;      // 堆的当前元素个数 
	int Capacity;  // 堆的最大容量 
};

MaxHeap Create(int MaxSize);  // 建堆 
bool IsFull(MaxHeap H);    // 判断堆是否满
bool Insert(MaxHeap H,ElementType item);   // 插入元素
bool IsEmpty(MaxHeap H);    //  判断堆是否为空
ElementType DeleteMax(MaxHeap H);  // 删除并返回堆中最大元素
void LevelOrderTraversal(MaxHeap H);  // 层序遍历 

// 建堆 
MaxHeap Create(int MaxSize){
	MaxHeap H = (MaxHeap)malloc(sizeof(struct HeapStruct));
	// Elements[0] 作为哨兵，堆元素从  Elements[1] 开始存放 
	H->Elements = (ElementType *)malloc((MaxSize+1) * sizeof(ElementType));
	H->Size = 0;
	H->Capacity = MaxSize;
	// "哨兵"大于堆中所有可能的值 
	H->Elements[0] = MaxData;
	return H;
} 

// 插入，从完全二叉树的最后一个位置插入 
bool Insert(MaxHeap H,ElementType item){
	if(IsFull(H)){
		printf("堆已满，无法插入！\n");
		return false;
	}
	int i = ++H->Size;  // 指向堆中最后一个位置 
	for(;H->Elements[i/2] < item;i/=2)    // 向上找比 item 大的结点 
		H->Elements[i] = H->Elements[i/2];  //  向下赋值 
	H->Elements[i] = item;  // 找到了，把 item 值放进去 
	return true;
}

// 删除，从根结点删除 
ElementType DeleteMax(MaxHeap H){
	int parent,child;
	ElementType Max,tmp;
	if(IsEmpty(H)){
		printf("堆为空，无法删除！\n");
		return ERROR;
	}
	Max = H->Elements[1];  // 拿到最大值
	tmp = H->Elements[H->Size--];  // 拿到完全二叉树最后一个值 
	// 判别条件：parent 是否有左孩子结点 
	for(parent=1;parent*2<=H->Size;parent=child){
		// 左右孩子结点中找较大的值 
		child = 2 * parent;  // 左孩子结点 
		// child!=H->Size 表示 child 不为当前最后一个结点，即 parent 有右孩子结点 
		if((child!=H->Size) &&(H->Elements[child] < H->Elements[child+1]))
			child++;  
		// 给 tmp 找个合适的位置 
		// 如果当前左右孩子结点比 tmp 都小，说明 tmp 位置已经合适 
		if(H->Elements[child] <= tmp)
			break;
		else    // 否则把较大的孩子结点提上来，自己继续下去找 
			H->Elements[parent] = H->Elements[child];
	}
	H->Elements[parent] = tmp;  // 在合适的位置把 tmp 放进去 
	return Max;
} 

// 判断是否已经满 
bool IsFull(MaxHeap H){
	return (H->Size == H->Capacity);
}

// 判断是否为空
bool IsEmpty(MaxHeap H){
	return !H->Size;
}

// 层序遍历
void LevelOrderTraversal(MaxHeap H){
	int i;
	printf("层序遍历的结果是：");
	for(i = 1;i<=H->Size;i++){
		printf("%d ",H->Elements[i]);
	} 
	printf("\n"); 
} 

int main(){
	MaxHeap H;
	int MaxSize = 100;
	H = Create(MaxSize);
	Insert(H,55);
	Insert(H,66);
	Insert(H,44);
	Insert(H,33);
	Insert(H,11);
	Insert(H,22);
	Insert(H,88);
	Insert(H,99);
	/*
		 99
		/  \
	   88  66
	  / \  / \
	 55 11 22 44
	/ 
   33	  
	*/
	LevelOrderTraversal(H);
	DeleteMax(H);
	LevelOrderTraversal(H);
	DeleteMax(H);
	LevelOrderTraversal(H);
	DeleteMax(H);
	LevelOrderTraversal(H);
	DeleteMax(H);
	LevelOrderTraversal(H);
	return 0;
}
```

最小堆：（插入式建堆法）

```cpp
#include<iostream>
#include<malloc.h>
const int MinData = -100000;  // 哨兵值
const int MaxSize = 1005;   // 最大个数 
using namespace std;
typedef struct HeapStruct *Heap;
struct HeapStruct{
	int *data;   // 存值的数组 
	int size;   // 当前元素个数 
	int capacity;  // 最大容量 
};

// 初始化堆
#include<iostream>
#include<malloc.h>
const int MinData = -100000;  // 哨兵值
const int MaxSize = 1005;   // 最大个数 
using namespace std;
typedef struct HeapStruct *Heap;
struct HeapStruct{
	int *data;   // 存值的数组 
	int size;   // 当前元素个数 
	int capacity;  // 最大容量 
};

// 初始化堆
Heap Create(){
	Heap H;
	H = (Heap)malloc(sizeof(struct HeapStruct));
	H->data = (int *)malloc(sizeof(int) * (MaxSize+1));
	H->size = 0;
	H->capacity = MaxSize;
	H->data[0] = MinData;
	return H;
} 

// 插入
void Insert(Heap H,int x){
	int i = ++H->size;  // 指向数组最后一个 
	for(;H->data[i/2]>x;i/=2)
		H->data[i] = H->data[i/2];
	H->data[i] = x;
} 

// 遍历 
void bl(Heap H){
	for(int i=1;i<=H->size;i++)
		cout<<H->data[i]<<" ";
}

int main(){
	Heap H;
	H = Create();
	int n;
	cin>>n;
	for(int i=0;i<n;i++){
		int t;
		cin>>t;
		Insert(H,t);
	}
	bl(H);
	return 0;
} 
```

[(4条消息) 数据结构（九）堆_叫我皮卡丘的博客-CSDN博客](https://blog.csdn.net/liyuanyue2017/article/details/83713957)



#### 哈夫曼树（最优二叉树/带权路径长度（WPL）最小的二叉树）

![image-20221006141943236](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221006141943236.png)

最优二叉树或哈夫曼树：WPL 最小的二叉树

要使得带权路径长度（WPL）最小，必须使权值越大的叶节点靠近跟结点，而权值越小的叶节点越远离根节点。每次找最小的两个拼起来，然后再和别的拼

哈夫曼树的特点：

- 没有度为1的结点
- n个叶子结点的哈夫曼树共有2n-1个结点
- 哈夫曼树的任意非叶节点的左右子树交换后仍是哈夫曼树
- 对于同一组权值，可能存在不同构的多棵哈夫曼树





##7 排序

### 7.1冒泡排序

 ```cpp
 void bubbleSort(int *a,int n)
 {
     for(int i=0;i<n-1;i++){
         int flag=0;
         for(int j=0;j<n-i-1;j++){
             if(a[j]>a[j+1]){
             	swap(a[j],a[j+1]);
                 flag=1;
             }
         }
         if(flag==0) break;
     }
 }
 ```

时间复杂度O（n^2^）,空间复杂度O（1）；

### 7.2选择排序

选择排序是一种简单直观的排序算法，无论什么数据进去都是 O(n²) 的时间复杂度。所以用到它的时候，数据规模越小越好。唯一的好处可能就是不占用额外的内存空间了吧。

```cpp
template<typename T> 
void selection_sort(std::vector<T>& arr) {
        for (int i = 0; i < arr.size() - 1; i++) {
                int min = i;
                for (int j = i + 1; j < arr.size(); j++)
                        if (arr[j] < arr[min])
                                min = j;
                std::swap(arr[i], arr[min]);
        }
}
```

###7.3 插入排序

<img src="https://www.runoob.com/wp-content/uploads/2019/03/insertionSort.gif" alt="img" style="zoom: 50%;" />

```cpp
void insertSort(int a[],int len){
    for(int i=1;i<len;i++){
        j=i-1;
        while(j>0 && a[j]>a[i]){
            a[j+1]=a[j];
            j--;
        }
        a[j+1]=a[i];
    }
}
```



时间复杂度O(n^2)，空间复杂度O(1)。

### 7.4希尔排序

就是插入排序的升级版，但希尔排序是非稳定排序算法。希尔排序的基本思想是：先将整个待排序的记录序列分割成为若干子序列分别进行直接插入排序，待整个序列中的记录"基本有序"时，再对全体记录进行依次直接插入排序。见数据结构的笔记。==增量序列不断缩小！！==

```cpp
void shellSort(int *unsortArray, const int &length, int step) {
	while (step > 0) {
		for (int i = step; i < length; ++i) {
			int tem = i;
			while (tem >= step) {
				if (unsortArray[tem] < unsortArray[tem - step]) {
					swap(unsortArray[tem], unsortArray[tem - step]);
				}
				tem -= step;
			}
		}
		--step;
	}
}
```

时间复杂度O（N*logN）,时间复杂度依赖于步长的选择。

空间复杂度O（1）

### 7.5并归排序

<img src="https://www.runoob.com/wp-content/uploads/2019/03/mergeSort.gif" alt="img" style="zoom:50%;" />

时间复杂度 O(N*logN)，空间复杂度为O(N)。需要额外的空间
先将所有数两个一组排序，再将两组四个数一起排序为新的一组，循环下去每次合并两组，直到所有数有序。

```cpp
//递归：
#include<iostream>
using namespace std;
 
void Merge(int arr[],int low,int mid,int high){
    //low为第1有序区的第1个元素，i指向第1个元素, mid为第1有序区的最后1个元素
    int i=low,j=mid+1,k=0; //mid+1为第2有序区第1个元素，j指向第1个元素
    int *temp=new(nothrow) int[high-low+1]; //temp数组暂存合并的有序序列
    if(!temp){ //内存分配失败
        cout<<"error";
        return;
    }
    while(i<=mid&&j<=high){
        if(arr[i]<=arr[j]) //较小的先存入temp中
            temp[k++]=arr[i++];
        else
            temp[k++]=arr[j++];
    }
    while(i<=mid)//若比较完之后，第一个有序区仍有剩余，则直接复制到t数组中
        temp[k++]=arr[i++];
    while(j<=high)//同上
        temp[k++]=arr[j++];
    for(i=low,k=0;i<=high;i++,k++)//将排好序的存回arr中low到high这区间
		arr[i]=temp[k];
    delete []temp;//删除指针，由于指向的是数组，必须用delete []
}
 
//用递归应用二路归并函数实现排序——分治法
void MergeSort(int arr[],int low,int high){
    if(low<high){
        int mid=(low+high)/2;
        MergeSort(arr,low,mid);
        MergeSort(arr,mid+1,high);
        Merge(arr,low,mid,high);
    }
}
 
int main(){
    int a[10]={5,1,9,3,7,4,8,6,2,0};
    MergeSort(a,0,9);
    for(int i=0;i<10;i++)
        cout<<a[i]<<" ";
    return 0;
}

```



```cpp
//非递归
void MergeSort2(int arr[],int n)//n代表数组中元素个数，即数组最大下标是n-1{
	/*
	int step = 1;
	while(step<n) //当元素个数不是2的幂时可能会出错，未考虑第2个序列个数不足的情况
	{
		for(int i=0;i<=n-step-1;i+=2*step)
			Merge(arr,i,i+step-1,i+2*step-1);
		step*=2;
	}*/
 
	int size=1,low,mid,high;
	while(size<=n-1){
		low=0;
		while(low+size<=n-1){
			mid=low+size-1;
			high=mid+size;
			if(high>n-1)//第二个序列个数不足size
				high=n-1;
			Merge(arr,low,mid,high);//调用归并子函数
			low=high+1;//下一次归并时第一关序列的下界
		}
		size*=2;//范围扩大一倍
	}
}
```

时间复杂度为O(nlogn)，空间复杂度为 O(n)，归并排序比较占用内存，但效率高且稳定。





##9 KMP算法

match[],数组的生成

```cpp
void get_match(string T, int *match)
{
    int i,j;
    i=1;
    j=0;
    next[1]=0;
    while(i<T.size()){
        if(j==0||T[i]==T[j])//T[i]是后串、T[j]是前串
        {
            ++i;
            ++j;
            match[i]=j;
        }
        else
            j=match[j];
    }
}
```

KMP

```cpp
int KMP(string S,string T,int pos){
    int i=pos;
    int j=1;
    int match[255];//构建一个数组
    get_match(T,next);
    while(i<=S.size() && j<=T.size()){
       if(j==0||S[i]==T[j])//T[i]是后串、T[j]是前串
        {
            ++i;
            ++j;
        } 
        else{
            j=match[j];
        }
    }
    if(j>T.size())
        return i-T.size();
    else
        return 0;
}
```

改进的KMP：

只要改get_match()函数,在if内加一段

```
if(j==0||T[i]==T[j])//T[i]是后串、T[j]是前串
        {
            ++i;
            ++j;
            match[i]=j;
            if(T[i]!=T[j]){
            	match[i]=j;
            }
            else
            	match[i]=match[j];
        }

```

### 7.6快速排序

### 7.7基数排序

###7.8堆排序+表排序

### 7.9排序的比较

![image-20221027202306784](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221027202306784.png)
