#C++小知识点（面经）

###1.struct和union

char ：1个字节
char*(即指针变量): 8个字节
short int : 2个字节
int：  4个字节
unsigned int : 4个字节
float:  4个字节
double:  8个字节
long:  8个字节
long long:  8个字节
unsigned long:  8个字节

1.在存储多个成员信息时，[编译器](https://so.csdn.net/so/search?q=编译器&spm=1001.2101.3001.7020)会自动给struct第个成员分配存储空间，struct 可以存储多个成员信息，而Union每个成员会用同一个存储空间，只能存储最后一个成员的信息

2.都是由多个不同的数据类型成员组成，但在任何同一时刻，[Union](https://so.csdn.net/so/search?q=Union&spm=1001.2101.3001.7020)只存放了一个被先选中的成员，而结构体的所有成员都存在。

3.对于Union的不同成员赋值，将会对其他成员重写，原来成员的值就不存在了，而对于struct 的不同成员赋值 是互不影响的。

struct 简单来说就是一些相互关联的元素的集合，说是集合，其实它们在内存中的存放是有先后顺序的，并且每个元素都有自己的内存空间。那么按照什么顺序存放的呢？其实就是按你声明的变量顺序来存放的

```cpp
struct sTest

{

    int a;  //sizeof(int) = 4

    char b;  //sizeof(char) = 1

    shot c； //sizeof(shot) = 2

}x;
```

所以在内存中至少占用 4+1+2 = 7 byte。然而实际中占用的内存并不是7 byte，这就涉及到了字节对齐方式。





union 的不同之处就在于，它所有的元素共享同一内存单元，且分配给union的内存size 由类型最大的元素 size 来确定，如下的内存就为一个double 类型 size ：

```cpp
union uTest

{

    int a;   //sizeof(int) = 4

    double b;  //sizeof(double) = 8

    char c;  //sizeof(char) = 1

}x;
```

所以分配的内存 size 就是8 byte。既然是内存共享，理所当然地，它不能同时存放多个成员的值，而只能存放其中的一个值，就是最后赋予它的值，如：

x.a = 3; x.b = 4.5; x.c = ‘A’;       这样你只看到x.c = ‘A’，而其它已经被覆盖掉，失去了意义。

内存对齐：

```cpp
union u
{
　double a;
　int b;
};

union u2
{
　char a[13];
　int b;
};

union u3
{
　char a[13];
　char b;
};
cout<<sizeof(u)<<endl; // 8
cout<<sizeof(u2)<<endl; // 16
cout<<sizeof(u3)<<endl; // 13
//都知道union的大小取决于它所有的成员中，占用空间最大的一个成员的大小。所以对于u来说，大小就是最大的double类型成员a了，所以sizeof(u)=sizeof(double)=8。但是对于u2和u3，最大的空间都是char[13]类型的数组，为什么u3的大小是13，而u2是16呢？关键在于u2中的成员int b。由于int类型成员的存在，使u2的对齐方式变成4，也就是说，u2的大小必须在4的对界上，所以占用的空间变成了16（最接近13的对界）。
```

　　**结论：复合数据类型，如union，struct，class的对齐方式为成员中对齐方式最大的成员的对齐方式。**



先后定义的顺序不同可能会导致struct的内存大小不同：

```cpp
struct s1
{
　char a;
　double b;
　int c;
　char d;
};

struct s2
{
　char a;
　char b;
　int c;
　double d;
};

cout<<sizeof(s1)<<endl; // 24
cout<<sizeof(s2)<<endl; // 16
```

同样是两个char类型，一个int类型，一个double类型，但是因为对界问题，导致他们的大小不同。计算结构体大小可以采用元素摆放法，我举例子说明一下：首先，CPU判断结构体的对界，根据上一节的结论，s1和s2的对界都取最大的元素类型，也就是double类型的对界8。然后开始摆放每个元素。

　　对于s1，首先把a放到8的对界，假定是0，此时下一个空闲的地址是1，但是下一个元素d是double类型，要放到8的对界上，离1最接近的地址是8了，所以d被放在了8，此时下一个空闲地址变成了16，下一个元素c的对界是4，16可以满足，所以c放在了16，此时下一个空闲地址变成了20，下一个元素d需要对界1，也正好落在对界上，所以d放在了20，结构体在地址21处结束。由于s1的大小需要是8的倍数，所以21-23的空间被保留，s1的大小变成了24。

　　对于s2，首先把a放到8的对界，假定是0，此时下一个空闲地址是1，下一个元素的对界也是1，所以b摆放在1，下一个空闲地址变成了2；下一个元素c的对界是4，所以取离2最近的地址4摆放c，下一个空闲地址变成了8，下一个元素d的对界是8，所以d摆放在8，所有元素摆放完毕，结构体在15处结束，占用总空间为16，正好是8的倍数。



### 2.智能指针



智能指针面试常考：**[(7条消息) C/C++面试：什么是智能指针？智能指针有什么作用？分为哪几种？各自有什么样的特点？_OceanStar的学习笔记的博客-CSDN博客_什么是智能指针](https://blog.csdn.net/zhizhengguan/article/details/112302192)**

[(7条消息) C++智能指针总结（面试常问）_Sunrise的博客的博客-CSDN博客_智能指针 面试](https://blog.csdn.net/weixin_41969690/article/details/107912842)



### 3.函数前和函数后加const的区别

有关函数后面加const的解释：

- 前面使用const 表示返回值为const
- 后面加 const表示函数不可以修改class的成员，const限定

我们定义的类的[成员函数](https://so.csdn.net/so/search?q=成员函数&spm=1001.2101.3001.7020)中，常常有一些成员函数不改变类的数据成员，也就是说，这些函数是"只读"函数，而有一些函数要修改类数据成员的值。如果把不改变数据成员的函数都加上const关键字进行标识，显然，可提高程序的可读性。其实，它还能提高程序的可靠性，**已定义成const的成员函数，一旦企图修改数据成员的值，则编译器按错误处理**。 const成员函数和const对象 实际上，const成员函数还有另外一项作用，即常量对象相关。对于内置的数据类型，我们可以定义它们的常量，用户自定义的类也一样，可以定义它们的常量对象。
1、非静态成员函数后面加const（加到非成员函数或静态成员后面会产生编译错误）
2、表示成员函数隐含传入的this指针为const指针，决定了在该成员函数中， 任意修改它所在的类的成员的操作都是不允许的（因为隐含了对this指针的const引用）；
3、唯一的例外是对于mutable修饰的成员。加了const的成员函数可以被非const对象和const对象调用，但不加const的成员函数只能被非const对象调用



###4.函数后加&

详见CPP primerP483-484

指出this的左值和右值属性的方式和定义const成员函数是相同的：即在参数列表后面放一个引用限定符：从而阻止对右值的一系列操作。

```cpp
class Foo{
public:
    Foo &operator=(const Foo&) &;//再加一个引用限定
};
Foo &Foo::operator=(const Foo &rhs) &{
    return *this;
} 
```

引用限定符可以是&也可以是&&，分别指出指向左值和右值。同时和const一样，只能用在非static成员上。一个函数可以同时const和&限定，但是const要在前面。也可以用const和&来区分是否重载。



### 5.有关于文件检索和C++的版本

在linux下常用grep来查找系统内指定的字符串。而windows（windows没有grep，可以安装grep for windows但是没有必要）底下常用的是findstr，可以指定目录。文件里面的指定行出现的。

```
    其实windows下也有一个类似的命令findstr,比如：
   
    C:\Windows\system32>netstat -an|findstr 1521
        其实windows下也有一个类似的命令findstr,比如：
   
    C:\Windows\system32>netstat -an|findstr 1521
    
    二者的区别在于find搜索的东西需要用引号扩起来。
```

如果编译器支持11版本，可以通过：`#define __cplusplus 201103L`

可以：

```cpp
cout<<__cplusplus<endl;//看看版本。
```



### 6.endif和ifdef

\#ifdef和#endif必须成对使用。  
 从理论上讲可以出现在任何地方（头文件和实现文件中）  
 通常为了防止头文件被多次包含，在头文件中使用是必须的：  
 如：#ifndef  MY_HEAD_H  //头文件开头,名字是任意的,注意不要和其它头文件冲突    

在vs中就是#program once最方便。

一般情况下，源程序中所有的行都参加编译。但是有时希望对其中一部分内容只在满足一定条件才进行编译，也就是对一部分内容指定编译的条件，这就是**“条件****编译”。有时，希望当满足某条件时对一组语句进行编译，而当条件不满足时则编译另一组语句。** 

条件编译 命令 最常见的形式为： 

\#ifdef  表示符
程序段1 
\#else 
程序段2 
\#endif

它的作用是：当标识符已经被定义过(一般是用#define命令定义)，则对程序段1进行编译，否则编译程序段2。 
其中#else部分也可以没有，即： 
\#ifdef 
程序段1 
\#denif

**在头文件中使用#ifdef和＃ifndef是非常重要的，可以防止双重定义的错误。**



###7.`.`和`->`的区别

- A.B则A为对象或者结构体； 点号（.）：左边必须为实体。
- A->B则A为指针，->是成员提取，A->B是提取A中的成员B，A只能是指向类、结构、联合的指针； 箭头（->）：左边必须为指针；

```cpp
class A
{
public:
    int a = 0;
};
int main()
{
    A b;
    A *p = &b;
    b.a; //类类型的对象访问类的成员
    p->a; //类类型的指针访问类的成员
}
```

->相当于（*it）



### 8.static的详解

当程序执行到它的定义处时，编译器为它在栈上分配空间，函数在栈上分配的空间在此函数执行结束时会释放掉，这样就产生了一个问题:如果想将函数中此变量的值保存至下一次调用时，如何实现？ 最容易想到的方法是定义为全局的变量，但定义一个全局变量有许多缺点，最明显的缺点是破坏了此变量的访问范围（使得在此函数中定义的变量，不仅仅只受此函数控制）。static 关键字则可以很好的解决这个问题。


（1）在修饰变量的时候，static 修饰的静态局部变量只执行初始化一次，而且延长了局部变量的生命周期，直到程序运行结束以后才释放。
（2）static 修饰全局变量的时候，**这个全局变量只能在本文件中访问，不能在其它文件中访问，即便是 extern 外部声明也不可以**。
（3）static 修饰一个函数，则这个函数的只能在本文件中调用，不能被其他文件调用。static 修饰的变量存放在全局数据区的静态变量区，包括全局静态变量和局部静态变量，都在全局数据区分配内存。初始化的时候自动初始化为 0。
（4）不想被释放的时候，可以使用static修饰。比如修饰函数中存放在栈空间的数组。如果不想让这个数组在函数调用结束释放可以使用 static 修饰。
（5）考虑到数据安全性（当程序想要使用全局变量的时候应该先考虑使用 static）。

没有被初始化的静态全局变量会被自动初始化为0.

静态变量都在全局数据区分配内存，包括静态局部变量。

2.3 静态局部变量
（1）该变量在全局数据区分配内存；
（2）静态局部变量在程序执行到该对象的声明处时被首次初始化，即以后的函数调用不再进行初始化；
（3）静态局部变量一般在声明处初始化，如果没有显式初始化，会被程序自动初始化为 0；
（4）它始终驻留在全局数据区，直到程序运行结束。但其作用域为局部作用域，当定义它的函数或语句块结束时，其作用域随之结束。

被 static 修饰的变量、被 static 修饰的方法统一属于类的静态资源，是类实例之间共享的

在 C++ 中，静态成员是属于整个类的而不是某个对象，静态成员变量只存储一份供所有对象共用。所以在所有对象中都可以共享它。

**静态成员函数中不能引用非静态成员**

**类的非静态成员函数可以调用用静态成员函数**，**但反之不能**

**静态成员只能在类外进行初始化**（写力扣的时候常用）

静态成员函数没有this指针，静态成员函数主要用来访问静态数据成员 而不能访问非静态成员。



### 9.weak_ptr(死锁的情况)

![image-20221209151120921](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221209151120921.png)

==weak_ptr是用来解决shared_ptr相互引用时的死锁问题==,如果说两个shared_ptr相互引用,那么这两个指针的引用计数永远不可能下降为0,资源永远不会释放。==它是对对象的一种弱引用，不会增加对象的引用计数，和shared_ptr之间可以相互转化，shared_ptr可以直接赋值给它，它可以通过调用lock函数来获得shared_ptr。==

```cpp

#include<iostream>
#include<memory>
using namespace std;
class B;
class A
{
public:
    shared_ptr<B> pb_;
    ~A()
    {
        cout<<"A delete\n";
    }
};
class B
{
public:
    shared_ptr<A> pa_;
    ~B()
    {
        cout<<"B delete\n";
    }
};
  
void fun()
{
    shared_ptr<B> pb(new B());
    shared_ptr<A> pa(new A());
    pb->pa_ = pa;
    pa->pb_ = pb;
    cout<<pb.use_count()<<endl;
    cout<<pa.use_count()<<endl;
}
  
int main()
{
    fun();
    return 0;
}
```

可以看到fun函数中pa ，pb之间互相引用，两个资源的引用计数为2，当要跳出函数时，智能指针pa，pb析构时两个资源引用计数会减一，但是两者引用计数还是为1，导致跳出函数时资源没有被释放（A B的析构函数没有被调用）

如果把其中一个改为weak_ptr就可以了，我们把类A里面的shared_ptr pb_; 改为weak_ptr pb_; 这样的话，资源B的引用开始就只有1，当pb析构时，B的计数变为0，B得到释放，B释放的同时也会使A的计数减一，同时pa析构时使A的计数减一，那么A的计数为0，A得到释放。

==注意的是我们不能通过weak_ptr直接访问对象的方法，比如B对象中有一个方法print(),我们不能这样访问，pa->pb_->print(); 因为pb_是一个weak_ptr，应该先把它转化为shared_ptr,如：shared_ptr p = pa->pb_.lock(); p->print();==

如果weak_ptr绑定的shared_ptr已经被释放了，那么weak_ptr返回的就是一个nullptr



### 10.静态类型和动态类型

 静态类型在编译时已经确定了,它是变量声明时的类型或表达式生成的类型.而动态类型则是变量或表达式表示的内存中的对象的类型.动态类型直到运行时才能知道.

```cpp
Quote *pQuote=new Bulk_quote;
```

 指针pQuote的静态类型是Quote,在编译时就已经确定了.但是它的动态类型是Bulk_quote.直到运行时才知道它指向的是基类还是派生类.如果一个变量非指针也能引用.则它的静态类型和动态类型永远一致.但基类的指针或引用可能与其动态类型不一致.

```cpp
	Bulk_quote bulk;
	Quote* pQuote = &bulk;
	Quote& rQuote = bulk;
	//传递给item的如果是派生类对象,即是静态类型和动态类型不同的情况.
	double print_total(ostream & os, const Quote & item, size_t n);

```



### 11.C++的强制类型转换

在C++语言中新增了四个关键字static_cast、const_cast、reinterpret_cast和dynamic_cast。这四个关键字都是用于强制类型转换的。新类型的强制转换可以提供更好的控制强制转换过程，允许控制各种不同种类的强制转换。

1. **static_cast**

**用法：static_cast <类型说明符> （变量或表达式）**

**它主要有如下几种用法：**
  （1）用于类层次结构中基类和派生类之间指针或引用的转换
   进行上行转换（把派生类的指针或引用转换成基类表示）是安全的
   进行下行转换（把基类的指针或引用转换为派生类表示），由于没有动态类型检查，所以是不安全的
  （2）用于基本数据类型之间的转换，如把int转换成char。这种转换的安全也要开发人员来保证
  （3）把空指针转换成目标类型的空指针
  （4）把任何类型的表达式转换为void类型
  注意：static_cast不能转换掉expression的const、volitale或者__unaligned属性。

**static_cast:可以实现C++中内置基本数据类型之间的相互转换。**

如果涉及到类的话，static_cast只能在**有相互联系的类型中进行相互转换,**不一定包含虚函数。

一般用于数据类型的强制转换

```cpp
//这种形式是从C继承过来的
int a=10;
int b=3;
double result=(double) a/(double) b;
//利用static_cast来做类型转换。
double result=static_cast<double>(a) / static_cast<double>(b);
```

2. **const_cast**:

**而const_cast则正是用于强制去掉这种不能被修改的常数特性，但需要特别注意的是const_cast不是用于去除变量的常量性，而是去除指向常数对象的指针或引用的常量性，其去除常量性的对象必须为指针或引用。**

```cpp
#include<iostream>
using namespace std;
 
 
int main()
{
    const int a = 10;
 
    const int * p = &a;
 
    int *q;
 
    q = const_cast<int *>(p);//去除其常量性
 
    *q = 20;    //fine
 
    cout <<a<<" "<<*p<<" "<<*q<<endl;
 
        cout <<&a<<" "<<p<<" "<<q<<endl;
 
    return 0;
}
```

**之后我们定义了一个普通的指针\*q。将p指针通过const_cast去掉其常量性，并赋给q指针。之后我再修改q指针所指地址的值时，这是不会有问题的。**而且原本的a的值并不会被改变。

3. **reinterpret_cast:**

reinterpret_cast主要有三种强制转换用途：***改变指针或引用的类型、将指针或引用转换为一个足够长度的整形、将整型转换为指针或引用类型***。

**用法：reinterpret_cast<type_id> (expression)**
  type-id必须是一个指针、引用、算术类型、函数指针或者成员指针。

```cpp
int *a = new int;
double *d = reinterpret_cast<double *>(a);
//将整型指针通过reinterpret_cast强制转换成了双精度浮点型指针。
```

4. **dynamic_cast:**

和动态绑定相关，具体见网页：[(9条消息) C++强制类型转换_恋恋西风的博客-CSDN博客_c++强制数据类型转换](https://blog.csdn.net/q610098308/article/details/115915802)



### 12.C++中explict和constexpr

- C++提供了关键字explicit，可以阻止不应该允许的经过转换[构造函数](https://so.csdn.net/so/search?q=构造函数&spm=1001.2101.3001.7020)进行的隐式转换的发生,声明为explicit的构造函数不能在隐式转换中使用。当类的声明和定义分别在两个文件中时，explicit只能写在在声明中，不能写在定义中。

- 所谓常量表达式，指的就是由多个（≥1）常量组成的表达式。换句话说，如果表达式中的成员都是常量，那么该表达式就是一个常量表达式。这也意味着，常量表达式一旦确定，其值将无法修改。constexpr 关键字的功能是使指定的常量表达式获得在程序编译阶段计算出结果的能力，而不必等到程序运行阶段。C++ 11 标准中，constexpr 可用于修饰普通变量、函数（包括模板函数）以及类的构造函数。

```cpp
//常量表达式函数的定义,定义函数的时候只能有一句return语句别的都不能有。
constexpr int display(int x){
    return 1 + 2 + x;
}
```

注意，constexpr 修饰类的构造函数时，要求该构造函数的函数体必须为空，且采用初始化列表的方式为各个成员赋值时，必须使用常量表达式。

```cpp
//自定义类型的定义
struct myType {
    constexpr myType(char *name,int age):name(name),age(age){};
    const char* name;
    int age;
    //其它结构体成员
};
```



### 13.OOP与泛型编程

相同：都能处理在编写程序时不知道类型的情况，

不同：OOP能处理类型在程序运行之前都未知的情况，而在泛型编程中，在编译的时候就能直到类型了。

OOP将 datas 和methods联系在一起；GP将 datas 和methods分开；这么做都是对具体的抽象。OOP的关键是类，类实例化出对象；GP的泛型是相对于强类型程序语言而定义的，GP 编程本身不需要指定类型的datas，实例化时需要datas,更像是methods的抽象。

采用GP：
containers和algorithms团队可以各自闭门造车，其间以iterators联通即可。
algorithms通过iterators确定操作范围，并通过Iterators取container元素

所有的algorithms，其内最终设计元素本身的操作，就是比大小。

==当编译器遇到一个模板定义的时候，它并不生成代码，只有当实例化出模板的一个特定版本的时候，编译器才会生成代码==，所以与类不同，模板的头文件通常既包含声明也包含定义。模板的一些错误，大部分 都是在实例化的时候出现



### 14. 左值右值的定义：

左值（一般是永久存在的）：赋值、下标、解引用、前置递增或递减、表达式

右值（短暂存在的）：算术、关系、位、后置递增递减、+const的左值引用、字面常量（“abc”）、临时对象（string）()="world"；）、函数的返回值。



只要把左值放到`std::move()`内，就可以变成一个右值。它的功能很简单，就是将某个左值强制转化为右值。



### 15. 虚继承

当发生多重继承（简单点的例子菱形继承）的时候，有可能一个派生类继承了多份相同的数据，从而产生二义性

利用虚继承可以解决菱形继承的问题。

```cpp
class sheep : virtual public Animal{};

class Tuo : virtual public Animal {};
```

Animal 称为虚基类，关键词==virtual==

只要虚继承之后，两个数据变为一块内存，对哪个父类进行指定都是对同一个进行修改。

```cpp
	YangTuo yt;
	yt.sheep::m_age = 18;
	yt.Tuo::m_age = 20;
	cout << "yt.sheep::m_age =" << yt.sheep::m_age << endl;
	cout << "yt.Tuo::m_age =" << yt.Tuo::m_age << endl;
	cout << "yt.m_age= " << yt.m_age << endl;
```

![image-20220421160138392](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220421160138392.png)



在C++语言中，**虚继承**是的目的是令某个类做出声明，承诺愿意共享它的基类。其中，共享的基类子对象称为**虚基类**，无论虚基类在继承体系中出现了多少次，在派生类中都只包含唯一一个共享的虚基类子对象。

### 16.enum枚举

C++允许程序员创建自己的数据类型，比如本节要将的枚举类型。枚举数据类型是一种由程序员定义的数据类型，其合法值是与它们关联的一组命名整数常量。

之所以被称为枚举类型，就是因为命名常量是作为数据类型定义的一部分而枚举或列出的，以下是枚举类型声明的示例：

`enum <类型名> {<枚举常量表>};`

```cpp
enum color_set1 {RED, BLUE, WHITE, BLACK}; // 定义枚举类型color_set1
enum week {Sun, Mon, Tue, Wed, Thu, Fri, Sat}; // 定义枚举类型week
```



- 关键字enum——指明其后的标识符是一个枚举类型的名字。
- 枚举常量表——由枚举常量构成。"枚举常量"或称"枚举成员"，是以标识符形式表示的整型量，表示枚举类型的取值。枚举常量表列出枚举类型的所有取值，各枚举常量之间以"，"间隔，且必须各不相同。取值类型与条件表达式相同。

枚举常量代表该枚举类型的变量可能取的值，编译系统为每个枚举常量指定一个整数值，默认状态下，这个整数就是所列举元素的序号，序号从0开始。 可以在定义枚举类型时为部分或全部枚举常量指定整数值，在指定值之前的枚举常量仍按默认方式取值，而指定值之后的枚举常量按依次加1的原则取值。 各枚举常量的值可以重复。例如：

![image-20221211134814938](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221211134814938.png)

可以创建枚举的对象，比如说：

```cpp
ccolor_set color1,color2;
color1=RED;//将枚举常量值赋给枚举变量
int i=color1;//值为1，也就是让i的值赋为RED在枚举列表中的位置。

```

- 枚举变量可以直接输出，但不能直接输入。如：cout >> color3;  //非法
- 不能直接将常量赋给枚举变量。如： color1=1; //非法
- 不同类型的枚举变量之间不能相互赋值。如： color1=color3; //非法
- 枚举变量的输入输出一般都采用switch语句将其转换为字符或字符串；枚举类型数据的其他处理也往往应用switch语句，以保证程序的合法性和可读性。

### 17.类型转换

C++中的类型转换包括隐式类型转换和显式类型转换。隐式类型转换是指在编译时自动进行的类型转换，例如将一个整型值赋给一个浮点型变量。显式类型转换则需要在代码中显式地指定要进行的类型转换，例如使用强制类型转换运算符（例如，在一个浮点值前面加上（int），将其转换为整型值）。
