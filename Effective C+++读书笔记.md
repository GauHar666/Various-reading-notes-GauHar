#  Effective C+++读书笔记

## 条款01-03

![image-20221114140243891](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221114140243891.png)

![image-20221114140300706](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221114140300706.png)

![image-20221114140317661](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221114140317661.png)

![image-20221114140328090](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221114140328090.png)

## 条款04.确定对象被使用之前已经被初始化

static对象其寿命从被构造出来一直到程序结束为止，他包括global对象、定义于namespace作用域内的对象.....

- 一个问题在于C++对于定义于不同的编译单元内的non-local static对象的初始化相对次序并没有明确定义，一般找不到正确的初始化次序

  **解决方法：**将每个non-local static对象搬运到自己的专属函数内（该对象在此函数内被声明为static），==这些函数返回一个reference指向其所含的对象。==

  <img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221114141959682.png" alt="image-20221114141959682" style="zoom:67%;" />

总结：

1. 请将内置对象进行手工初始化

2. 构造函数最好使用成员初值列

   ```cpp
   ABEntry::ABEntry(const string& name.const string& address,const list<int>& phone):theName(name), theAddress(address),thePhone(phones),numTimesConsulted(0){}
   ```

3. 请以local static对象替代non-local static对象







## 条款7.为多态基类声明virtual析构函数

C++明确指出，当derived class对象经由一个base class指针被删除的时候，该base class 一定要带着一个non-virtual析构函数。如果基类没有析构，派生类中的数据可能未被销毁，因为基类的析构没有被重写。

==vitual函数的目的是允许派生类的实习可以客制化==。

==任何class有vitual函数都几乎确定应该也有应该vitual析构函数==

想要实现出virtual函数，那么对象必须携带信息，这些信息通常是由一个所谓vptr（virtual table pointer）指针指出的。vptr指向一个由函数指针构成的数组，称为vbtl（virtual table）；每一个带有virtual的函数的class都有一个相应的vtbl。当对象调用某一virtual函数的时候，实际被调用的函数取决于该对象的vptr所指向的那个vtbl；

绝对不能吧一个没有虚析构函数的类当成基类让别的类继承。

##条款8. 别让异常逃离析构函数

程序并没有禁止析构函数吐出异常，但是它不鼓励我们这么做，比如你在一个容器内创建了多个这样的类，你在该块内结束的时候，你要一个一个析构，每次析构抛出异常，当两个即以上异常同时存在的话会导致程序的不明确执行。

两个不那么好的方法避免报错：

![image-20221129194742404](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221129194742404.png)

析构函数绝地不能吐出异常，如果客户需要对某个操作函数运行期间抛出的异常做反映，那么class应该提供应该普通函数用来执行析构。



## 条款9. 绝不在构造和析构过程中调用virtual函数

比如说调用子类的构造函数的时候，会优先调用基类（父类）的构造，而在base class构造的期间，virtual里函数不是virtual函数。



## 条款10. 令operator= 返回一个对*this 的引用

赋值采用的是右结合律：

```cpp
x=y=z=5;  --->   x=(y=(z=5));
```

为了实现这种链式的赋值，赋值操作符必须返回一个reference指向操作符的左侧实参，这是为classes实现赋值操作符时应该遵循的协议，该协议使用于所有的赋值相关运算。

 ```cpp
 class Widget{
     Widget& operator=(const Widget& rhs){
         return* this;
     }
 }
 ```

只是个协议，你可以不遵守，但是最好遵守

仿函数：

```cpp
        bool operator==(const Person& p){
            if(this->m_Name == p.m_Name && this->m_Age == p.m_Age){
                return true;
            }
            else{
                return false;
            }
        }



        MyInteger& operator++()
        {
            m_Num++;
            return *this;
        }
```



## 条款11 在operator= 中处理“自我赋值”

自我赋值看起来很愚蠢，但是程序有的时候确实会这么做且合法。任意一个父类的指针或引用都可以指向一个子类的对象。

所以有可能你引用了一个父类的对象，有可能和子类是一个对象。

解决方法：在operator=前面加一个“证同测试”，以达到自我赋值的检验目的



## 条款12. 赋值对象的时候勿忘其每一个成分

因为你自定义不用编译器提供的拷贝构造和拷贝赋值的时候，你在类内新添加元素并不会帮你也自动拷贝，所以如果你定义了自己的拷贝构造和拷贝赋值，那么你每次添加新的元素都需要重写你的拷贝构造拷贝赋值函数。



任何时候在对于子类（派生类）写拷贝函数的时候，必须小新地赋值其base class的成分，那些成分往往是private，所以无法直接访问，一个调用相应的base class 的函数



## 条款13 以对象管理资源

为了确保一个调用指针的函数返回的资源总是会被释放，就需要将资源放进对象内，当控制流离开f，该对象的析构函数会自动释放那些资源。利用析构函数来释放资源。

最好使用智能指针避免手动释放内存是最好的



## 条款16 成对使用new和delete时需要采取相同形式

就是delete，new出来的数组的时候，需要在前面加一个[],不能只写一个数组名

```cpp
std::string* stringPtr1=new std::string[100];
delete []stringPtr1;
```



## 条款17 以独立语句将new对象存储与智能指针内

如果不这么做，有可能会发生难以察觉的资源泄漏

```cpp
//错误的方法：
processWidget(std::shared_ptr<Widget>(new Widget),priority());
//如果先new然后priority(),priority发生错误了，就会造成内存泄漏

//正确的方法：
std::shared_ptr<Widget>pw(new Widget);
processWidget(pw,priority());
```



## 条款18 正确使用接口

C++中的接口有很多：function接口、calss接口、template接口等等



## 条款19. 设计class犹如设计type

设计class的时候要考虑以下问题：

- 新的class 的对象应该如何被创建和被销毁
- 对象的初始化和对象的赋值应该有什么样的差别
- 如果对象以值传递回出现什么情况
- 新的类型的合法值是什么
- 是否需要继承自他人或给他人继承，取决了要不要重写virtual函数或者要不要定义虚析构函数（从而成为虚基类）。
- .....

## 条款20. 宁以pass-by-reference-to-const替代pass-by-value

在缺省的情况下C++将以by value的形式传递对象至函数，除非你另外指定，否则函数参数都是以实际实参的复件为初值，而调用段所获得的亦是函数返回值的一个复件。这些副本对象都是由对象的拷贝构造函数拷贝出来的，比如

```cpp
bool validateStudent(Student s);
Student plato;
bool platoIsOK=validateStudent(plato);
```

这个过程中回调用Student的拷贝构造函数，如何当函数结束之后又会调用一次析构函数。而student内由有两个string对象，他还继承自别的一些类，那么上面的操作就会带来很多次析构+很多次构造的成本。



**为了降低这些成本**：使用pass by reference-to-const的方法

```cpp
bool validateStudent(const Student& s);
```

这种传递方式的效率非常高，因为没有任何构造函数或者析构函数倍调用，原因是没有任何新的对象被创建。

这个==const==至关重要，有了const才不会让原本以引用方式传入的参数被改变。



同时使用以常量引用的方式传值的话，还可以解决类继承问题中的切割问题，slicing问题

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221211143907082.png" alt="image-20221211143907082" style="zoom:67%;" />

但是以上这个规则往往并不适用与内置类型，以及STL的迭代器和函数对象，对于他们而言这种反复构造和析构的代价很小。



## 条款21必须返回对象时，别妄想返回其reference

看了上一条条款之后看你回犯一些致命的错误：开始传递一些references指向其实并不存在的对象。

直接把表达式的值返回，不要再新建什么引用的对象之类的对象。

![image-20221211145524325](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221211145524325.png)

## 条款22 将成员变量声明为private

其实本质上只有两种封装权限：

- private--->指封装的
- public和protected----->不封装的

因为public会让所有使用了这个成员的对象因为删除掉这个对象而被破坏

protected会让所有的派生类出问题。

## 条款23 用非成员和非友元函数替换成员函数

![image-20221211191358668](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221211191358668.png)

越多的函数可以访问一段数据，那么数据的封装性就越差

能够访问private成员变量函数的只有class的member函数加上friend函数而已

面对这种调用很多类内部函数的函数，比较自然的做法是让clearBrowser成为一个non-member函数并且位于WebBrowser所在的同一个命名空间中。

## 条款25 考虑写出一个不抛出异常的swap函数

只要T类型支持拷贝构造和拷贝赋值，那么缺省的swap（也就是系统给的那个）实现代码就会帮你置换类型为T的对象，我们不需要再做另外的工作。

![image-20221211194946361](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221211194946361.png)

## 条款26 尽可能延后变量定义式的出现时间

应该延后到这份定义知道能够给它初值为止。

对于循环来说：是应该把变量定义在循环外还是循环内好呢？

```cpp
int i;
for(int j=0;j<n;j++){i=j+2};

for(int j=0;j<n;j++){
    int i=0;
    ...
}
```

第一种做法：1个构造+1个析构+n个赋值

第二种做法：n个析构+n个构造

如果赋值的成本远小于构造和析构，那么一般是第一种好点。反之第二种好。



## 条款27.尽量少做转型的动作

转型：旧式的`double j=0.01; int i=(int) j;`

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221212160629470.png" alt="image-20221212160629470" style="zoom:80%;" />

在类型转换的过程中并不只是简单的让编译器把某种类型看成是另外一种类型。其实类型的底层表述不同，中间执行了很多过程。

- 尽量避免转型，特别是在注重效率的代码中避免dynamic_casts
- 如果转型是必须的，尽量封装在函数内部
- 尽量使用新型转换，不要使用就行转换

## 条款28 避免返回handles指向对象内部成员

引用、指针、迭代器都属于handles（号码牌，用来获取某个对象），返回handle会造成对象的封装性降低，有可能导致虽然调用const成员函数却造成对象状态改变。 



## 条款29 为“异常安全”而努力是值得的

异常安全有两个条件，当异常被抛出的时候，带有异常安全性的函数会：

- 不泄露任何资源
- 不允许数据败坏

对于数据败坏要保证：

- 基本承诺：如果异常被抛出，程序内的任何事物仍然保持在有效状态之下。
- 强烈保证：成功就完全成功，如果函数失败，程序会回复到调用函数之前的状态。
- 不抛弃保证



## 条款30 透彻了解inlining的里里外外

看起来像函数，动作像函数，但是又不用承受函数调用所带来的开销

inline函数的背后整体观念是，将”对此函数的每一个调用“都以函数本体替换之，这样做的缺点就是会增加目标代买的大小，过度使用inline会导致代码膨胀，降低代码效率

- inline只是对编译器的一个申请，而不是强制的命令。这项申请可以是隐喻的，也可以是显式提出的（直接inline）：

  - 一般隐喻就是将函数定义在class 的定义式之内：

  ```cpp
  class Person{
  public:
  	int age() const{return theAge};
  private:
      int theAge;
  }
  ```

  类似于常见的max函数就是inline的，而且inline的函数一定被置于头文件中，因为大多建设环境的时候必须inline

inline的函数必须在执行前（也就是编译期就必须明确），而和virtual函数不同的就是，virtual函数是动态编译的。

通过函数指针调用的函数，一般不用inline。构造函数和析构函数一般也不被设为是inline。

应该将inline限制在小型、被频繁调用的函数身上。

## 条款31 将文件间的编译依存关系降至最低

- 如果使用对象的引用、对象的指针可以完成任务，就不要使用对象
- 如果可以，尽量以class的声明来替换class的定义
- 为声明和定义提供不同的头文件。

C++中，使用handle classes(句柄类)的目的，是为了降低文件之间的编译依存关系。

比如，我有一个类Person,在很多地方都用到了这个类（#incude Person.h),在程序不断完善的过程中，难免会对该类进行重新设计或者一些修改。当Person.h被很多文件包含时，即使我们只是对Person类做了很小的改动，那么所有包含该头文件的文件，都需要重新编译，这会花费大量的无谓的时间，我想这是每一个编程人员都不希望看到的，为了解决此类问题的发生，我们便想到了句柄类。

我们把Person类设计成一个 handle class (句柄类），而重新定义一个新类 PersonImpl，作为具体的实现类，当然原本Person类中的成员变量，和成员函数的具体实现都放在PersonImpl类中。在Person类中定义一个指向PersonImpl类的指针，用于调用具体的实现。这样一来，当实现修改了，我们只需要重新编译Person文件即可。

```cpp
//Person.h  
//the handle class  
//定义  
#include <string>  
#include <memory>  
class PersonImpl;  
class Person  
{  
public:  
    Person(const std::string& name,const int &id,const std::string& addr);  
    std::string rename() const;  
    int reid() const;  
    std::string readdr() const;  
private:  
    std::tr1::shared_ptr<PersonImpl> pImpl; //指针，指向具体的完成实现工作的类 PersonImpl  
      
};  
  
//Person.cpp  
//the handle class  
//实现  
#include "Person.h"  
#include "PersonImpl.h" //必须这样做，否则无法调用其成员函数，  
                        //注意，PersonImpl有着和句柄类Person完全相同的成员函数,2者接口完全相同  
                           
Person::Person(const std::string& name,const int &id,const std::string& addr)  
    :pImpl(new PersonImpl(name,id,addr))  
{  
}  
std::string Person::rename() const  
{  
    return pImpl->rename(); //通过指针调用实现类里的成员函数，完成具体动作  
}  
int Person::reid() const  
{  
    return pImpl->reid();  
}  
std::string Person::readdr() const  
{  
    return pImpl->readdr();  
}  
//PersonImpl.h  
//the implement class  
//定义  
#include <string>  
#include <memory>  
class PersonImpl  
{  
public:  
    PersonImpl(const std::string& name,const int &id,const std::string& addr);  
    std::string rename() const;  
    int reid() const;  
    std::string readdr() const;  
private:  
    std::string theName;  
    int theId;  
    std::string theAddress;  
      
};  
  
//PersonImpl.cpp  
//the implement class  
//实现  
#include "PersonImpl.h"  
PersonImpl::PersonImpl(const std::string& name,const int &id,const std::string& addr)  
    :theName(name),theId(id),theAddress(addr)  
{  
}  
std::string PersonImpl::rename() const  
{  
    return theName;  
}  
int PersonImpl::reid() const  
{  
    return theId;  
}  
std::string PersonImpl::readdr() const  
{  
    return theAddress;  
}  
//Main.cpp  
#include <iostream>  
#include "Person.h"  
//主程序，只需要包含Person类，因为Person类的接口永远不会改变，如果实现文件PersonImpl中的接口或者成员改变了  
//只需要重新编译Person.h，而不需要重新编译包含person.h的文件了  
int main()  
{  
    Person man1("Tom",10,"England");  
    std::cout<<"the name:"<<man1.rename()<<std::endl;  
    std::cout<<"the id:"<<man1.reid()<<std::endl;  
    std::cout<<"the Address:"<<man1.readdr()<<std::endl;  
    system("pause");  
    return 0;  
}  
```



## 条款32 确定你的public继承塑膜出is-a关系

如果让class D以public继承自class B，你便是告诉C++编译器，每一个类型为D的对象同时也是一个类型为B的对象，反之不成立。比如student继承自person，每个student都是person，但是每个person不一定是student。说明子类更特殊化，

==任何函数如果期望获得一个类型为Person（或pointer-to-Persom或Person的引用）的实参，也都原因接受Student的。这个论点只对public继承有效==

public继承意味着，适用于base classes身上的每一件事情也一定适用于derived classes，因为每一个派生类的对象也是一个基类对象。

## 条款33 避免遮掩继承而来的名称

**![image-20221216214938749](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221216214938749.png)**

这意味着如果你继承base class并加上重载函数，而你又希望重新定义或覆写其中某一部分，那么你必须为哪些原本会被遮掩的每个名称引入一个using声明式，防止你继承的名称会被遮掩。

## 条款34区分接口继承和实现继承

基类的成员函数有三种声明方式：

- 纯虚函数
- 非纯虚函数的虚函数
- 普通函数

而纯虚函数的public继承的子类相当于只继承了函数的接口，而纯虚函数并不一定没有自己的实现，纯虚函数可以在类外实现自己的功能



## 条款37 绝不重新定义继承而来的缺省参数值

因为virtual函数是动态绑定的，而缺省参数值确实静态绑定的。

```cpp
#include <iostream>      
using namespace std;      
      
class A      
{      
    public:      
    virtual void Print(int a = 999)      
    {      
        cout<<a<<endl;      
    }      
};      
      
class B : public A      
{      
    public:      
    virtual void Print(int a = 666)      
    {      
        cout<<a<<endl;      
    }      
};      
      
void Test(A& a)      
{      
    a.Print();      
}      
      
int main()      
{      
    B b;                                                                                                                                    
    Test(b);      
    return 0; 
}

```

- 这段代码的输出结果是999而非666，也就充分验证我们的结论

给了默认值不要改。



##条款39 明智而审慎地使用private继承

private继承而来的子类的所有成员，都会变成private。

private继承意味着只有实现部分被继承，接口部分应该被省略。如果D以private形式继承B，意思是D对象根据B对象实现而得。

- private继承意味着is-implemented-in-terms of（根据某物实现出）。它通常比复合的级别要低，但是当派生类需要访问基类的protected的成员，或者需要重新定义继承而来的virtual函数时，这么设计是合理的。



##条款40 明智而审慎地使用多重继承

多重继承的格式：

```cpp
class D: public A, private B, protected C{
    //类D新增加的成员
}
```

如果两个类中有相同的成员，那么子类中使用的时候会引起歧义。为了解决歧义，在使用的时候需要指明是哪个类的成员

```cpp
D.A::checkOut();
```

从正确行为的观点来看，public继承总应该是virtual。为了避免继承得来的成员变量重复，使用virtual继承的那些classes所产生的对象往往比使用non-virtual继承的兄弟们体积要大，访问virtual base classes的成员变量时，也比访问non-virtual base classes

==也就是所谓的虚继承==

## 条款41. 了解隐式接口何编译期多态

**运行期多态**

的设计思想要归结到类继承体系的设计上去。对于有相关功能的对象集合，我们总希望能够抽象出它们共有的功能集合，在基类中将这些功能声明为虚接口（虚函数），然后由子类继承基类去重写这些虚接口，以实现子类特有的具体功能。典型地我们会举下面这个例子：
![img](https://images2015.cnblogs.com/blog/610439/201601/610439-20160115112003194-1372188564.png)

运行期多态的实现依赖于虚函数机制。当某个类声明了虚函数时，编译器将为该类对象安插一个虚函数表指针，并为该类设置一张唯一的虚函数表，虚函数表中存放的是该类虚函数地址。运行期间通过虚函数表指针与虚函数表去确定该类虚函数的真正实现。

**编译期多态**：

对模板参数而言，多态是通过模板具现化和函数重载解析实现的。**以不同的模板参数具现化导致调用不同的函数**，这就是所谓的编译期多态。
相比较于运行期多态，实现编译期多态的类之间并不需要成为一个继承体系，它们之间可以没有什么关系，但约束是它们都有相同的隐式接口。

```cpp 
 
class Animal
{
public :
    void shout() { cout << "发出动物的叫声" << endl; };
};
class Dog
{
public:
     void shout(){ cout << "汪汪！"<<endl; }
};
class Cat
{
public:
     void shout(){ cout << "喵喵~"<<endl; }
};
class Bird
{
public:
     void shout(){ cout << "叽喳!"<<endl; }
};
template <typename T>
void  animalShout(T & t)
{
    t.shout();
}
int main()
{
    Animal anim;
    Dog dog;
    Cat cat;
    Bird bird;
 
    animalShout(anim);
    animalShout(dog);
    animalShout(cat);
    animalShout(bird);
 
    getchar();
}

```

在编译之前，函数模板中t.shout()调用的是哪个接口并不确定。在编译期间，编译器推断出模板参数，因此确定调用的shout是哪个具体类型的接口。**不同的推断结果调用不同的函数**，这就是编译器多态。这类似于重载函数在编译器进行推导，以确定哪一个函数被调用。

![image-20221222210557935](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221222210557935.png)

**所谓的显式接口**

是指类继承层次中定义的接口或是某个具体类提供的接口，总而言之，我们能够在源代码中找到这个接口.显式接口以函数签名为中心，例如

```cpp
void AnimalShot(Animal & anim)
{
    anim.shout();
}
```

我们称shout为一个显式接口。在运行期多态中的接口皆为显式接口。

**而对模板参数而言，接口是隐式的**，奠基于有效表达式。例如：

```cpp
template <typename T>
void AnimalShot(T & anim)
{
    anim.shout();
}
```

  对于anim来说，必须支持哪一种接口，要由模板参数执行于anim身上的操作来决定，在上面这个例子中，T必须支持shout()操作，那么shout就是T的一个隐式接口。

- classes和templates都支持接口和多态
- 对classes而言接口是显式的，以函数签名为中心，多态则是通过virtual函数发生于运行期
- 对templates参数而言，接口是隐式的，多态是通过template具体化和函数重载解析发生于编译期



##条款43 学习处理模板化基类的名称

![image-20221223000142209](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221223000142209.png)



## 条款44 将与参数无关的代码抽离程序

class template的成员函数只有在被使用的时候才会被初始化。

而在编写template的时候，重复的代码是隐式的，需要程序员来避免。



## 条款45 运用成员函数模板接受所有兼容类型

