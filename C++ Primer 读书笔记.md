# C++ Primer 读书笔记

\1.    类内部的函数在类外声明的时候必须使用inline声明成内联函数。

\2.    返回this对象的函数：inline Screen & Screen::set(char c){ return *this;}//注意函数的返回值的类型是类的引用。若返回的不是引用，则返回值是*this的副本，只能改变临时变量，不能改变值，就是深浅拷贝问题。

\3.    即使两个类的成员列表完全一致，他们也是不同的类型。

\4.    和函数的声明和定义可以分开一样，类的声明和定义也可以分开。这样的单独声明被称之为：前向声明，而这个类被称为：不完全类型。可以定义指向这种类型的指针或引用。

\5.    因为只有当类全部完成后类才能被定义，所以一个类 成员类型不能是自己，但是成员允许是指向自身类型的指针或引用。

\6.    如果一个类指定了一个友元类，则友元类的成员函数可以访问此类包括非公有成员在哪点所有成员，而且类的友元并不传递，一个友元类中的友元不可以访问当前类内的非公有成员。也可以单独让某一个类中的某个成员函数作为友元：friend void Window_mgr::clear(xx)

\7.    extern的作用是：声明一个变量而不是定义他

\8.    编译器处理完类中所有的声明之后才会处理成员函数的定义。

\9.    一般内层作用域可以重新定义外层作用域中的名字。但是如果成员使用了外层作用域中的某个名字，而该名字代表一种类型，则类不能在之后重新定义该名字。

\10.   如果成员是const或者引用格式的时候，必须将其初始化。所以在构造函数中必须现实的初始化。就是用：和，那种初始化：constFef(int ii):i(ii),ci(ii),ri(i){. }

\11.   提供cin作为接受istream&参数的构造函数的默认实参。

\12.   每个参数都提供了默认值的构造函数也是默认构造函数。

\13.   可以通过将构造函数声明为explicit加以阻止将其隐式转换。只能在类内部使用，类外部不用使用。

\14.   聚合类：书本p266,相当于说是最简单的类。

\15.   字面值常量：算术类型、引用、指针、某些类。

\16.   constexpr是常量表达式的意思。





### 6.函数

- 没有返回值的return，即`return;`,只能用在void函数中，用来是其在中间位置提前退出。

- 返回值必须返回和函数类型相同的值/可以隐式转换的值。

- ==千万不要返回局部对象的引用或指针==

  - 因为函数调用完成后这部分的存储空间将会被释放，那么引用和指针将不再有有效区域。
  - 

- C++11规定：函数可以返回花括号内包围的值的列表，==返回一个vector对象==。

- 允许主函数非void类型但没有返回值，没有的时候默认return 0；

- 返回0代表成功，其他值代表失败

- 预处理变量：定义在`cstdlib`头文件中，目前见到的有nullptr、NULL、表示成功/失败的：EXIT_FAILURE、EXIT_SUCCESS.预处理变量前面不能加std::，也不能在using中声明。

- 返回数组指针，因为数组不能被拷贝，所以函数不能返回数组，但是考研返回数组的指针或引用。`using arrT=int[10]`==`typedef int arrT[10]`,两个等价。然后就可以定义函数：`arrT* func(int i);`func函数返回一个指向含有10个整数的数组的指针。

- 如果想定义一个返回数组指针的函数，则数组的维度必须跟在函数名后面，也要跟在形参列表后面，具体如：`int (*func(int i))[10];` 形参是整形的返回10个int类型数组的指针。

  - 对于C++11特性新的写法：`auto func(int i)-> int(*)[10];`

- ```cpp
  string (&func(string (&arrStr)[10]))[10]
   
  /************************************************************
  逐层理解：
    func(string (&arrStr)[10]),名为func的函数有一个string型的含有10个元素的数组的引用参数
    (&func(string (&arrStr)[10])),表明我们可以对函数返回的结果也是一个引用
    (*func(int i))[10],表明对函数的返回是一个大小是10的数组的引用
    string (&func(string (&arrStr)[10]))[10],表示返回的数组中的元素是string类型
  ************************************************************/
  ```

  这一部分在书本P206，很难懂。

- 重载应该在形参的数量或者形参的类型上有所不同。==不允许两个函数只有返回类型不同，这样的重载是不允许的。==

- 一个形参加不加const不能作为区别。但是const如果是指针或者引用就可以是用来重载的对象。

- 三种**函数相关的语言特性**：

  - **默认实参**：`string screen(int ht=24,int wid=80);`,需要注意的是：一旦某个形参被赋予了默认值，那么他后面的所有形参都必须有默认值。调用的时候可以省略默认实参，见书本P212。函数的声明可以有很多次，但是在给定作用域内只能被赋予一次默认实参，也就是说函数的后续声明只能为之前没有默认形参的值添加实参。

  - **内联函数**：==内联函数可以避免函数调用的开销！！==，实质上是在函数返回类型前面加上inline，在定义的时候加哦。inline本身不能用在递归函数中。

    ```cpp
    inline const char *num_check(int v)
    {
        return (v % 2 > 0) ? "奇" : "偶";
    }
    ```

  - **constexpr函数**：指能够用于常量表达式的函数，

- assert预处理宏：assert（expr），先对expr表达式求值，如果表达式为假（0），则输出信息并终止程序，如果为真，则什么也不做。==预处理变量都不用using进行声明，预处理变量在函数内必须唯一==。

- NDEBUG预处理变量：如果定义了# define NDEBUG，则取消所有的assert判断。

- 顶层const不影响传入函数的对象

- 函数指针：`bool (*pf)(const string &,const string &)`          pf是一个指向函数的指针，其中该函数的参数是两个const string的引用，返回值是bool类型，括号一定要加，不然就变成返回值是bool* 类型。

- 可以直接把函数作为实参来使用，此时他会自动转换成指针`useBigger(s1,s2,lengthCompare);` 这个函数里面的lengthCompare就是函数，直接当成指针传入。

### 7.类

- 类成员函数的声明必须在类内，**函数的定义可以在类外**。
- `std::string isbn() const(return bookNP;)`后面的const的作用是**修改隐式this指针类型**,C++允许把const放在成员函数的参数列表之后，这样表示的是this指向常量的一个指针。==把这样的使用方法称之为常量成员函数==
- 默认情况下this的类型是指向类类型非常量版本的常量指针。比如`Slae_data * const`
- 编译器处理类的时候：是优先编译成员的声明，然后菜轮到成员函数体。所以函数体可以随意使用类中的其他成员而无需在一这些成员出现的次序。
- 类外定义的时候，函数名前面要加上作用域，保持和定义与声明完全相同：

```cpp
double Sales_data::avg_price() const{
    ////
}
```

- this指针可以直接做对象返回： return *this，直接返回调用该函数的对象。

- ```cpp
  class Person
  {
  private:
  	string strName;
  	string strAddress;
  public:
  	string getName() const { return strName; }//要用const 因为不会修改
  	string getAddress() const { return strAddress; }
      std::istream &read(std::istream &is, Person &per)
  {
  	is >> per.strName >> per.strAddress;
  	return is;
  }
   
  std::ostream &print(std::ostream &os, const Person &per)
  {
  	os << per.getName() << per.getAddress();
  	return os;
  }
  };
  ```

- 如果函数在概念上属于类，但是不定义在类中，，则它一般与类的声明（不是定义）要在同一个头文件内，

  ```cpp
  istream &read(istream &is,Sales_data &item){
      ....
  }
  ```

  read函数接受一个IO类型的引用作为其参数，因为IO类属于不能被拷贝的类型，因此只能通过引用来传递。这里的is在调用的时候可以是：`read(cin,trans);`这样的。

- 一个类可以有多个构造函数，但是每个构造函数必须是重载的。

- 如果在块中的内置类型或复合类型的对象被默认初始化，则他们的值将不会被定义。所以不适用于合成的默认构造函数；还有当一个类中包含其他类类型的成员且这个成员没有默认构造函数，那么编译器就无法初始化。

- C++中规定，如果我们需要默认的行为，那么可以通过在参数列表后写上`=default`来要求编译器生成默认构造函数。

- 下面的就是一个构造函数重载的结构体。

- <img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221030140410830.png" alt="image-20221030140410830" style="zoom: 25%;" />

- 一种新的初始值赋值方法,在块之前，用：赋初值。

  ```cpp
  Sale_data(const std::string &s,unsigned n,double p):bookNo(s),units_sold(n),revenue(p*n){}
  ```

- 当类需要分配类对象之外的资源时，合成的版本的拷贝函数往往会失效。动态的内存类应该使用vector/string来避免分配和释放内存带来的复杂性。

- 构造函数和部分成员函数仔public后，而数据成员和作为实现部分的函数则跟在private后面。

- struct和class都可以用来定义类，默认访问权限不同，struct默认全public，class默认全private。

- 封装是指保护类的成员不被随意访问的能力。通过把类的实现细节设置为private，我们就能完成类的封装。封装实现了类的接口和实现的分离。封装有两个重要的优点：一是确保用户代码不会无意间破坏封装对象的状态；二是被封装的类的具体实现细节可以随时改变，而无需调整用户级别的代码。

- 当非成员函数确实需要访问类的私有成员时，我们可以把它声明成该类的友元

- 类可以允许其他类或者函数访问他的非公有成员，仔这个函数前面加个friend，比如：`friend std::istream &read(.....)`,==友元的声明只能出现在类定义的内部，位置不限，最好在类定义开始或结束时集中声明友元。==，**同时友元只是一个权限声明**，**不能作为函数声明**，**要有另外的函数声明**。

- `typedef std::string::size_type pos`=`using pos =std::string::size_type`,都是起别名的作用。

- 用来定义类型的成员必须先定义后使用！！！，所以一开始就要先定义好

- 定义在类内部的成员函数时自动inline的。

- 即使一个类内部，即使是const成员函数内，也可以通过**mutable**关键字来改变数据成员，比如`mutable size_t access_ctr`

- 静态数据成员可以是不完全类型，可以使用静态成员作为默认实参。静态成员与类本身有关，而不是与类的各个对象有关，通过static使其与类关联在一起。

- 虽然静态成员不属于类的某个对象，但是仍然可以通过类的对象、引用、指针来访问静态成员。

- 因为静态数据成员不属于类的任意一个对象，所以它们并不是在创建类的对象是被绑定的。**不能在类的内部初始化静态成员，必须在类的外部定义和初始化每个静态成员。类内初始化要用const**

  ```cpp
  class A{
  public:
  	static double rate;
      static const int vecSize=20;
      static vector<double> vec;
  };
  
  double A::rate=6.5;
  vector<double> A::vec(vecSize);//类外什么的时候不用反复static了
  ```

### 8.IO类

- 目前的IO库设施：
  - istream（输入流）类型
  - ostream（输出流）类型
  - cin，一个istream对象
  - cout，一个ostream对象
  - cerr，ostream对象，通常用于输出程序错误信息，写入到标准错误。
  - `>>`和`<<`
  - getline函数，从一个给定的ostream读取一行数据，存入一个给定的string对象中。
- iostream头文件定义了用于读写流的基本类型。
- fstream定义了读写命名文件的类型
- sstream定义了读写内存string对象的类型
- 宽字符语言对应的操作就是加了个w，比如：wcin，wcout...
- 标准库的流特性可以无差别的应用于：普通流、文件流、string流、char、宽字符流等。这是通过**继承机制来实现的。**
- IO对象不能拷贝或者赋值，因此不能将形参或者返回值设置为流类型。
- IO库条件状态P279
- 确定一个流对象的状态最简单的方法就是将它当作一个条件来用：比如`while(cin>>word)`如果输入操作成功，流保持有效状态，则条件为真。
- 将流当作条件使用的代码就等价于！fail（），而eof和bad操作只能表示特定错误。
- 从给定流中读取数据，直到遇到文件结束标识时停止，将打印的数据读取在标注输出上，在返回流之前对流进行复位：

```cpp
istream &print(istream &is, string &item)
{
    while (is >> item)
        ;
    // is.clear();

    is.clear(cin.rdstate() & ~is.failbit & ~is.eofbit);

    return is;
}
```

- 每个输出流都管理有关缓冲区，有了缓冲机制，操作系统就可以将程序的多个输出操作组合成单一的系统级写操作。刷新输出缓冲区的几个操作符

  - cout<<"hi"<<endl; //输出hi和一个换行，然后刷新缓冲区
  - cout<<"hi"<<flush;  //输出hi，然后刷新缓冲区，不附加任何东西
  - cout<<"hi"<<ends; //输出一个hi和一个空字符，然后刷新缓冲区

  如果想要每次输出之后都刷新缓冲区：则使用`unitbuf`操作符

  ```cpp
  cout<<unitbuf; //所有输出操作后都立刻刷新缓冲区
  cout<<nounitbuf; //回到正常缓冲方式
  ```

- 如果想要对文件进行读写操作，只要包含一个`#include <fstream>`文件就可以了同时包含了 ofstream（对文件进行写）、ifstream（对文件读）、和fstream（读写）三个，有这几个头文件创建的对象可以直接对文件使用>>或<<进行读写操作。

  - open（）函数，打开文件，具体可以看黑马

  - 当一个fstream对象被销毁的时候，close（）会被自动调用。

  - 读文档文件操作：

    ```cpp
    #include <iostream>
    #include <string>
    #include <vector>
    #include <fstream>
    
    using namespace std;
    
    int main()
    {
        ifstream input("test.txt");
        vector<string> vec;
        string str;
    	//每个单词单独存储
        //while(input>>str){vec.push_back(str);} 
        while (getline(input, str))
            vec.push_back(str);
    
        for (auto &i : vec)
            cout << i << endl;
    
        return 0;
    }
    ```

  - 从main函数传入文件名作为参数：

  ```cpp
  int main(int argv, char **argc)
  {
      ifstream input(argc[1]);
  
      Sales_data total;
  
      if (read(input, total))
      {
          Sales_data trans;
  
          while (read(input, trans))
          {
  ```

- 每个流都有一个关联的文件模式：

  具体键P286，in是读方式，out是写方式，app是末尾追加的方式。

  out和app一般以管道的方式连在一起。

  于ifstream关联的文件默认以in模式打开，于ofstream关联的文件默认以out模式打开，于fstream关联的默认以in或out模式打开。

### 9.顺序容器

\1.    虽然vector在每次重新分配内存时都要移动所有元素，但是这样的扩张操作比list和deque要快。

\2.    shrink_to_fit()只适用于vector string duque，可以将capacity（）减小为和size（）相同大小。

\3.    reserve（n） 分配至少能容纳n个元素的内存空间。如果需求大小小于或等于当前容量，reverse就什么也不做，如果大于，那么capacity将会大于等于reserve参数。

\4.    resize只改变元素数目，不改变容器容量。

\5.    链表、等别的容器没有capacity的操作原因是因为不需要连续的内存。

\6.    const char* 创建string时指向的数组必须以空字符结尾

\7.    如果越界了会抛出out_of_range的异常。

\8.    assign（）详见书P302，然后主要是做替换。

\9.    string.replace(11,3,”5th”); 是erase和insert的一种缩写，表示从第11位开始，删除3个字符并插入5th。

\10.   string搜索返回的是string::size_type类型的值，没找到返回-1（string::npos）.。 首先是find（）函数，查找参数指定的字符串，若找到，则返回第一个匹配位置的下标

\11.   string num(”123456789”),name(”r2d2”). . Auto pos=name.find_first_of(num).找到name中第一个在num中出现的下标。不在的是：find_first_not_of

\12.   实现数值和字符串之间的转换：string s=to_string(i),表示将整数i转换为字符表示形式。

\13.   double d=stod(s);  将字符串s转换为浮点型

\14.   stoi（字符串，起始位置，几进制）

\15.   默认情况下，stack和queue是基于deque实现的，priority_queue是在vector之上实现的，因为要求随机访问。栈stack基于deque实现，也可以在list或vector上实现 。queue也可以在list或vector实现，priortity_queue也可以用deque实现。

\16.   所有的适配都要求容器具有添加和删除元素以及访问尾元素的能力，索引用array和forward_list

- 顺序容器：vector、deque（双端队列）、list（双向链表，支持双向顺序访问）、forward_list（单向链表）、string、array
- 对于forward_list而言，不支持size操作，因为保存或计算其大小就会比手写链表多出额外的开销。对于其他容器而言，size**都是一个快速的常量时间复杂度的操作。**
- 如果程序需要在头位置插入或删除元素，一般使用list会比较好
- 如果程序只有头部或尾部插入/删除，则用deque。
- 定义一个没有默认构造函数的类型：

```cpp
vector<noDefault> v1(10,init);   //定义没有默认构造函数的类型容器时，必须提供元素初始化器
```

- `const_iterator`  表示可以读取元素，但不能修改元素的迭代器类型。

- 容器的操作

  - c1=c2    表示将c1中的元素替换为c2中的元素
  - swap（a，b）  交换两容器中的元素
  - 迭代器是可以进行++、--等累加累减操作的。

- 对于迭代器取值，要使用解引用的方式，比如`*it`.

- cbegin和cend表示的是const类型的迭代器。不需要写访问的时候用

- 容器的默认初始化：

  - C c{}

  - C c={a,b,c,d}

  - C c(b,e)   c初始化为迭代器b和e指定范围中的元素的拷贝。范围中元素的类型必须与C的元素类型相容。

  - 顺序容器的另一种构造：

    接受一个容器的大小，和一个可选的元素初始值。

    ```cpp
    vector<int> ivec(10,-1);  //10个int，每个都初始化为-1
    list<int> l(10);   //十个元素，每个都初始化为0
    deque<string> d(10);   //十个空string
    
    ```

- array是C++1新出的标准，array<int,24>,要指定固定大小

- `seq.assign(b,e);`将seq中的元素替换为迭代器b和e所表示的范围中的元素。

- `seq.assign(n,t);`将seq在元素替换为n个t

- 运算符赋值必须两个容器相同类型，assign赋值可以允许从一个不同但相容的类型赋值。

- 两个容器具有相同大小且所有元素都两两对应相等，则两个容器相等，否则不等

- 若大小不相等，当时按序来某个位置元素大于另外一个位置，则这个容器大。

```cpp
//比较list<int>和vector<int>是否相等
bool i_v_equal(vector<int> &ivec,list<int> &ilist){
    //比较list和vector元素的个数
    if(ilist.size()!=ivec.size())
        return false;
    auto lb=ilist.cbegin();         //list首元素
    auto le=ilist.cend();           //list尾元素
    auto vb=ivec.cbegin();          //vector首元素
    for(;lb!=le;lb++,vb++)
        if(*lb!=*vb)
            return false;
    return true;
}
```

- 顺序容器和关联容器的不同指出在于两者组织元素的方式不同，这些不同直接关系了 元素如何存储、访问、添加以及删除。
- 有关于容器的insert（）
  - `c.insert(p,t)` 在迭代器p指向的元素之前创建一个值为t的元素，返回指向添加新元素的迭代器位置
  - `c.insert(p,n,t)` 在迭代器p位置之前插入n个值为t的元素，返回指向新添加的第一个元素的迭代器
  - `c.insert(p,b,e)` 将另一个迭代器b-e之间的元素插入到迭代器p指向的元素之前。
  - `c.insert(p,il)` il是一个花括号包围的元素值列表，将这些值插入到p指向的元素之前
- 向vector/string/deque容器中非头尾位置插入元素都需要移动元素。而向vector和string添加元素可能需要重新分配存储空间。
- 当使用对象来初始化容器的时候，或者将对象插入到容器中是，实际放到容器中的是一个浅拷贝。
- 不支持push_front的可以用insert（v.begin（），3）；

```cpp
    string a; 
    deque <string> b;
    while(cin>>a){
        b.push_back(a);
    }
    deque<string>::iterator begin=b.begin();
    deque<string>::iterator end=b.end();
    while(begin!=end){
        cout<<*begin<<endl;
        ++begin;
    }
```

- ① 向一个vector,string，deque插入元素.会使现有指向容器的迭代器失效.

```cpp
#include<iostream>
#include<vector>
using namespace std;
int main(void){
    vector<int> iv={1,1,2,1};
    int some_val=1;
    vector<int>::iterator iter=iv.begin();
    int org_size=iv.size(),new_ele=0;       //原大小和新元素个数
    //每个循环步都重新计算 "mid",保证指向iv原中央元素
    while(iter!=(iv.begin()+org_size/2+new_ele))
        if(*iter==some_val){
            iter=iv.insert(iter,2*some_val);    //iter指向新元素
            new_ele++;
            iter++;iter++;                      //吧tier推进到旧元素的下一个位置
        }else iter++;                           //简单推进iter
        //用begin()获取vector首元素迭代器,遍历vector中的所有元素
        for(iter=iv.begin();iter!=iv.end();iter++)
            cout<<*iter<<endl;
        return 0;
}

```

- front和back返回的都是引用。
- 删除元素相关：
  - `c.erase(p)`  删除迭代器p所指元素，返回一个指向被删元素之后元素的迭代器
  - `c.erase(b,e)`删除迭代器b和e所指范围内的元素，返回一个指向最后一个被删元素之后元素的迭代器。
  - `clear()`删除c中所有元素，返回void。
- forward_list的特殊操作：
  - `insert_after 、emplace_after、erase_after`等一系列操作,详见书本P313
  - forward_list定义了首前迭代器：`before_begin()`，这个迭代器允许链表首元素之前并不存在的元素之后添加或删除元素。和end（）一个道理
- ==向容器中添加元素和从容器中删除元素的操作可能回事指向容器元素的指针、引用、迭代器失效==
- insert和erase返回的都是迭代器，每次在返回时更新迭代器，即可防止迭代器失效：详见课本P316页。



### 10泛型算法

\1.    标准库并没有给每个容器都定义成员函数实现各种操作，而是定义了一组泛型算法，简称算法，实现了一些经典算法的公共借口，比如排序和搜索等。包含在头文件《algorithm》和numeric中

- 大部分定义在algorithm、numeric中

- 迭代器大部分都是前闭后开的，[v.begin(),v.end())。

- 算法的特性在于：只需要应该迭代器就可以进行元素的访问，不依赖于容器的类型。同时给算法永远不会改变底层容器的大小，有可能改变元素的位置，但是永远不会直接添加或删除元素。

- 大部分的算法都需要先提供一个迭代器范围

  - 只读算法

    - find
    - count
    - accumulate（v.begin(),v.end(),0）;//求和操作，从开始到结尾，和初值设置为0
    - equal（第一个容器始，第一个容器止，第二个容器始）//比较两个容器是否一一对应，默认一样长。

  - 写入算法

    向目标位置迭代器写入数据的算法假定目的位置足够大，能容纳要写入的元素。

    - fill（`*`，`*`，元素）

  - 插入迭代器：

    `back_inserter`会创建一个容器，使用他时会调用push_back(),

    ```cpp
    vecypr<int> vec;
    auto it=back_inserter(vec);
    *it=42;//相当于把42插回去了。
    ```

  - 拷贝算法：

    - 此算法接受三个迭代器，前两个表示一个输入范围，第三个表示目的序列的起始位置，**传递给copy的目的序列至少要包含与输入序列一样多的元素**`ret=copy(v.begin(),v.end(),v2);`

      返回的是增量后的迭代器的尾元素位置

  - replace（list.begin(),list.end(),0,40）; 把0全换成40.

  - ![image-20221114195725566](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221114195725566.png)

这样就实现了算法和操作的数据结构的分离.提升了编程的效率.

**算法是不应该知道容器的存在的**



- sort算法接收的前两个参数是两个迭代器，最后一个参数是一个**谓词**。

  **谓词**：是一个可以调用的表达式，其返回结果是一个能用作条件的值，标准库算法所使用的谓词包括一元谓词和二元谓词，看你接受几个参数叫几元。

  比如，比较字符串谁长：

  ```cpp
  bool isShorter(const string &s1,const string &s2){ //谓词一般都是bool返回类型
      return s1.size()<s2.size();//返回值一般是一个表达式
  }
  
  sort(words.begin(),words.end(),isShorter)//直接把名字传进来就可以不用加括号。
  ```

  如果既要完成排序又要保证相等元素的相对位置，该怎么办呢？可以使用 stable_sort() 函数。相同元素不交换，保证位置稳定。

- find_if()函数接受的第三个参数和find不同，第三个参数接受的是一个谓词，并且find_if只接受一元谓词



**有关lambda：**

四种可调用对象：

- 函数
- 函数指针
- 重载了函数调用运算符的类
- lambda表达式

一个lambda表达式表示一个可以调用的代码单元，可以理解为一个未命名的内联函数。外形和函数一模一样，区别在于lambda有可能第一在函数内部、同时必须使用尾置返回。

语法形式：`[ capture ] ( params ) opt -> ret { body; };`

其中 capture 是捕获列表，params 是参数表，opt 是函数选项，ret 是返回值类型，body是函数体。

```cpp
auto f = [](int a) -> int { return a + 1; };
auto f = [](int a){ return a + 1; };//也允许省略返回值的定义
```

lambda 表达式在没有参数列表时，参数列表是可以省略的。因此像下面的写法都是正确的：

```cpp
auto f1 = [](){ return 1; };
auto f2 = []{ return 1; };  // 省略空参数表
```

lambda不能有默认参数

```cpp
class A
{
    public:
    int i_ = 0;
    void func(int x, int y)
    {
        auto x1 = []{ return i_; };                    // error，没有捕获外部变量
        auto x2 = [=]{ return i_ + x + y; };           // OK，捕获所有外部变量
        auto x3 = [&]{ return i_ + x + y; };           // OK，捕获所有外部变量
        auto x4 = [this]{ return i_; };                // OK，捕获this指针
        auto x5 = [this]{ return i_ + x + y; };        // error，没有捕获x、y
        auto x6 = [this, x, y]{ return i_ + x + y; };  // OK，捕获this指针、x、y
        auto x7 = [this]{ return i_++; };              // OK，捕获this指针，并修改成员的值
    }
};
int a = 0, b = 1;
auto f1 = []{ return a; };               // error，没有捕获外部变量
auto f2 = [&]{ return a++; };            // OK，捕获所有外部变量，并对a执行自加运算
auto f3 = [=]{ return a; };              // OK，捕获所有外部变量，并返回a
auto f4 = [=]{ return a++; };            // error，a是以复制方式捕获的，无法修改
auto f5 = [a]{ return a + b; };          // error，没有捕获变量b
auto f6 = [a, &b]{ return a + (b++); };  // OK，捕获a和b的引用，并对b做自加运算
auto f7 = [=, &b]{ return a + (b++); };  // OK，捕获所有外部变量和b的引用，并对b做自加运算
```

捕获列表可以捕获的东西，看上面。没捕获到的就不能用，捕获列表尾空，说明只能使用lambda所在函数中定义的（非static）变量使用捕获列表。



自定义一个lambda：

```cpp
int main()
{
    auto sum = [](int a, int b) {return a + b; };
    cout << sum(1, 1) << endl;

    return 0;
}
```



- 当定义一个lambda时，编译器生成一个与lambda对应的新的类类型。传递的参数接受编译器生成类类型的未命名对象。为什么喜欢用auto呢，因为是一个对象类型，自己写，你其实不知道这个对象具体是啥。
- 由于被捕获的变量的值是在lambda创建的时候拷贝的，（普通变量是调用的时候拷贝的），因此随后对其修改不会影响到lambda内对应的值。
- []写=号代表隐式捕捉值，&隐式捕捉引用。

- 如果希望能改变应该lambda捕获的值的话，就要加上mutable

  ```cpp
  auto f=[v] () mutable{return ++v};//这样就可以改变v的值了。
  ```

- lambda函数只在一两个地方使用的时候是最方便的，如果需要在多处使用，一般要去定义函数。

- ![image-20221115161317561](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221115161317561.png)

`_1,_2`表示的是占位符

ref函数的作用就是返回一个对象，包含给定的引用，此对象是可以拷贝的

有关bind 见书本P354-358

![image-20221116184353739](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221116184353739.png)

![image-20221116184431628](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221116184431628.png)

- 反向迭代器：就是++会往前，--会往后，从尾向前移动的迭代器。除了forward_list 之外的迭代器，其他容器都支持反向迭代器。反向迭代器的名称：`v.crbegin()` 和`v.crend()`，这里的begin和end分别指向尾和头。用于反向打印。，sort算法也可以传入反向迭代器来递减排序。

- 如何将反向迭代器转换为正常的迭代器呢：可以使用base，比如：`line.crbegin().base()`就把反向迭代器转换为正常的正向迭代器。

  查找最后一个值为0的代码：

  ```cpp
  int main()
  {
      list<int> lst{10, 2, 3, 0, 4, 5, 0, 1, 2, 3};
      auto f = find(lst.rbegin(), lst.rend(), 10);
  
      int index = 0;
      auto beg = lst.begin();
  
      while (beg != f.base())
      {
          ++index;
          ++beg;
      }
  
      cout << index << endl;
  
      return 0;
  }
  ```

- `copy(vec.rbegin() + 3, vec.rbegin() + 7, back_inserter(lst));`//逆序定位置拷贝。



- 算法形式下的迭代器分类

![image-20221117194546131](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221117194546131.png)

输入迭代器：可以读取序列中的元素：必须支持：`==、！=、++、*、->（相当于（*it）.member,即解引用迭代器，并提取对象成员）`。常常对应的就是：istream_iterator。

输入输出迭代器都只能进行单遍扫描算法

5中具体的见书本P366 

![image-20221117203628273](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221117203628273.png)

添加_if的算法一般第三个参数都是一个谓词。

在常见的算法后面_copy一般是蒋元素操作完之后拷贝到另外一个新的容器中去，第三个参数放的就是新容器的名字。

List和forward_list定义了几个函数形式的算法：list.merge（lst2）将l1

和l2合并，list.sort(),不能用外部接口算法的sort。List.splice(),切片，见书本370.而且链表的操作会改变容器，会对元素产生变化。

 

###11.关联式容器

关联式容器和顺序式容器的根本不同在于：关联式容器中的元素是按关键字来保存和访问d的，与之相对的，顺序容器中的元素是按照它在容器中的位置来顺序保存和访问的。

主要是map和set。

从map中输出元素的方法：

 ```cpp
  for (const auto& w : word_count) {
 
   cout << w.first << " " << w.second << endl;
 
   }
 ```

关联式容器的迭代器都是双向的。

Map和set这类的容器会自动排序，如果没有定义<的函数不可以直接构造map或这类的容器，unordered的这类可以。

如果传入自定义的数据类型，那么要跟着传入它的比较方式：

Multiset<Sales_data,decltype(compareIsbn)*> ms(conpareIsbn);

上述代码表示用这个方法比较ms中元素，decltype声明函数指针类型（后面要加*）。

set是关联容器，进行查找、修改操作效率高

list是顺序容器，插入删除操作效率低，随机访问速度慢

 

vector的unique（）：

从头到尾，判断当前元素是否等于上一个元素，将不重复的元素移到前面来(赋值操作)，而不是将重复的元素移动到后面去。因为是判断当前元素是否等于上一个元素，所以要去重的容器必须是经过排序的有序容器。可以有三个参数，前两个是范围，第三个是自定义的去重方式：返回值：去重以后vector中没有重复元素的下一个位置的迭代器。如果返回v.end（）说明没有重复。

Pair中的两个元素用普通访问符号就可以访问他们，也就是.点就可以。

初始化的方法：pair<T,T> p（v1,v2）；或者p={v1，v2}；再或者make_pair(v1,v2);

 

当解引用应该关联式容器的迭代器时，会得到一个value_type的值引用，对于map就是解引用出来一个pair。其第一个first元素是const的。

Map和set都有begin和end操作，也支持++操作



- 对于关联式容器来说，没有什么push_back()，pop这类的操作，插入元素用的就是insert

  - 向一个map类型容器插入元素的时候记得要插入pair类型，一般要自己构造：`word_count.insert(pair<string,int>(word,1));  `或者是：`word_count.insert(make_pair(word,1));`最简单的可以直接用一个花括号：`word_count.insert({word,1});`

- 对于删除元素来说：还是使用的erase，可以提供一个迭代器，一对迭代器删除等等

  - 说一个特殊一点的：可以指定key（键）来删除元素，然后直接把值也给删了，删除之后返回值是删除值元素的个数，如果没有返回0.

    ```cpp
    int main(int argc, char* argv[])
    {
        multimap<string, string> authortobook_m{ { "123","1,2,3" },{ "456","4,5,6" }, { "789","7,8,9" } };
        auto it = authortobook_m.find("123");
        if(it!=authortobook_m.end())
            authortobook_m.erase(it->first);
    }
    ```

- map的下标操作，只有map和unordered_map提供了下标运算和对应at函数。与其他下标运算不同的是：如果关键字并不存在在map当中，你对其取下标操作了，他会自动创建一个key值到这个map中,并将初值赋为0。由于会插入，所以只能对非const的map使用下标操作。

- 对于查找关联式容器中元素的方法：主要有`find`和`count`两种，find适用于不计数，count适用于统计多少个。

  - `c.lower_bound(k)` 返回一个迭代器，指向==第一个关键字不小于k==的元素
  - `c.upper_bound(k)` 返回一个迭代器，指向==第一个关键字大于k==的元素
  - `c.equal_range(k)`  返回一个迭代器pair，表示关键字等于k的元素范围，若k不存在，则pair的两个成员都等于c.end()

- 如果对于mul系列的容器，可以先count找到有多少个，然后再用find循环向后，查找count出来的次数，对于mul系列的容器，可以使用lower_bound和upper_bound得到一个迭代器的范围，表示具有该关键字的元素的范围。

- 直接用equal_range，返回的迭代器对组pair，`for(auto pos=authors.equal_range(search_item);pos.first!=pos.second;++pos.first)`

  ```cpp
  int main(int argc, char* argv[])
  {
      multimap<string, string> authortobook_m{ { "123","1,2,3" },{ "123","1,4,5" } ,{ "456","4,5,6" }, { "789","7,8,9" } };
      set<string> s;
      for (const auto& author : authortobook_m) {
          s.insert(author.first);
      }
      for (const auto& author : s) {
          cout << author << ": ";
          for (auto m = authortobook_m.equal_range(author); m.first != m.second; ++m.first) {
              cout << m.first->second << " ";
          }
          cout << endl;
      }   
  }
  ```

  

- 无序容器：

  - 就是那几个unordered的容器，他们不会从小到大排序，底层使用了哈希表。

    ![image-20221119140141023](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221119140141023.png)

  - 关于上面这张图，讲的是无序容器底层哈希表的篮子操作（有的地方也叫桶操作）。



### 12.动态内存

![image-20221211135814102](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221211135814102.png)

| 成员方法名      | 功 能                                                        |
| --------------- | ------------------------------------------------------------ |
| operator=()     | 重载赋值号，使得同一类型的 shared_ptr 智能指针可以相互赋值。 |
| operator*()     | 重载 * 号，获取当前 shared_ptr 智能指针对象指向的数据。      |
| operator->()    | 重载 -> 号，当智能指针指向的数据类型为自定义的结构体时，通过 -> 运算符可以获取其内部的指定成员。 |
| swap()          | 交换 2 个相同类型 shared_ptr 智能指针的内容。                |
| reset()         | 当函数没有实参时，该函数会使当前 shared_ptr 所指堆内存的引用计数减 1，同时将当前对象重置为一个空指针；当为函数传递一个新申请的堆内存时，则调用该函数的 shared_ptr 对象会获得该存储空间的所有权，并且引用计数的初始值为 1。 |
| get()           | 获得 shared_ptr 对象内部包含的普通指针。                     |
| use_count()     | 返回同当前 shared_ptr 对象（包括它）指向相同的所有 shared_ptr 对象的数量。 |
| unique()        | 判断当前 shared_ptr 对象指向的堆内存，是否不再有其它 shared_ptr 对象再指向它。 |
| operator bool() | 判断当前 shared_ptr 对象是否为空智能指针，如果是空指针，返回 false；反之，返回 true。 |

>  除此之外，C++11 标准还支持同一类型的 shared_ptr 对象，或者 shared_ptr 和 nullptr 之间，进行 ==，!=，<，<=，>，>= 运算。



```cpp
#include <iostream>
#include <memory>
using namespace std;
int main()
{
    //构建 2 个智能指针
    std::shared_ptr<int> p1(new int(10));
    std::shared_ptr<int> p2(p1);
    //输出 p2 指向的数据
    cout << *p2 << endl;
    p1.reset();//引用计数减 1,p1为空指针
    if (p1) {
        cout << "p1 不为空" << endl;
    }
    else {
        cout << "p1 为空" << endl;
    }
    //以上操作，并不会影响 p2
    cout << *p2 << endl;
    //判断当前和 p2 同指向的智能指针有多少个
    cout << p2.use_count() << endl;
    return 0;
}
```



除了自动和static对象之外，C++还支持动态分配对象。**动态分配的对象的生存期与他们在哪里创建的无关，只有当显式地被释放时，这些对象才会销毁**

目前为止，我们接触过：静态内存和栈内存。

**静态内存**：用来保存局部static对象，类static数据成员，以及定义在任何函数之外的变量。

**栈内存**：用来保存定义在函数内的非static对象。

以上两种内存中的对象都由编译器自动创建和销毁

除了上述两种之外，每个程序还拥有一个内存池，这部分内存被称为**自由空间**，或者可以被称之为**堆区**，程序利用堆来**动态分配（danamically allocate）**对象，动态对象的生命周期由程序来控制，不用的时候要显式地销毁（new和delete）。

![image-20221119201859790](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221119201859790.png)

具体可以看黑马的笔记，对于四个区的存储给了很详细的描述。



12.1智能指针：

- new，在动态内存中为对象分配空间并返回一个指向该对象的指针，可以对对象初始化
- delete，销毁对象，释放内存

C++11为了更安全地使用动态内存，提供了两种智能指针类型来管理动态内存对象：

与普通指针的区别在于它会负责自动释放所指对象，

- shared_ptr:允许多个指针指向同一个对象。
- unique_ptr:独占所指对象，
- 还有一个名为weak_ptr的伴随类，他是一种弱引用，指向shared_ptr所管理的对象

上述三个都被定义在memory头文件中。



类似vector，智能指针 也是一个模板，所以在初始化的时候也要指定指向的类型：

```cpp
shared_ptr<string> p1;
shared_ptr<list<int>> p2;
```

默认初始化的智能指针，里面放的是空指针。

![image-20221120141842933](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221120141842933.png)

- make_shared:常用方法：

`shared_ptr<int> p3=make_shared<int> (42)`//指向一个42int

也可以用auto来保存make_shared的结果，比较方便。

可以认为每个shared_ptr都有一个关联的计数器，通常称其为引用计数。只要拷贝一个shared_ptr或者增加了一个，计数器就会默认递增。

同时只要当计数器变为0的时候，shared_ptr会自动调用析构函数，释放自己所管理的内存，只要分配给他，就会在恰当的时间被释放，不用手动释放。



程序使用动态原因：

- 程序不知道自己需要多少内存
- 程序不知道所需对象的准确类型
- 程序需要在多个对象之间共享数据

当我们希望和容器不一样的时候：比如容器使用的时候拷贝一个副本，副本容器的生命周期是单独的。而我们希望如果一个拷贝的东西和原本的东西共享相同的元素，某个对象被销毁的时候，底层元素不能被销毁，拷贝他的另外一个对象指向了最初被创建的那些元素。书P404。



以下是strBlob类

```cpp
#pragma once
#include <iostream>
#include<vector>
#include<string>
using namespace std;
class StrBlob {
public:
	typedef std::vector<string>::size_type size_type;
	StrBlob();
	StrBlob(initializer_list<string> il);
	size_type size()const { return data->size(); };
	bool empty()const { return data->empty(); };
	void push_back(const string& t) { data->push_back(t); };
	void pop_back();
	string& front();
	string& back();
	const string& front()const;
	const string& back()const;
private:
	shared_ptr <vector<string>> data;
	void check(size_type i, const string& msg)const;
};
StrBlob::StrBlob() :data(make_shared<vector<string>>()) {};
StrBlob::StrBlob(initializer_list<string>il) :data(make_shared<vector<string>>(il)) {};
void StrBlob::check(size_type i, const string& msg)const
{
	if (i >= data->size())
		throw out_of_range(msg);
}
void StrBlob::pop_back()
{
	check(0, "pop_baxk on sempty StrBlob");
	data->pop_back();
}
string& StrBlob::front()
{
	check(0, "front on empty StrBlob");
	return data->front();
}
string& StrBlob::back()
{
	check(0, "back on empty StrBlob");
	return data->back();
}
const string& StrBlob::front()const
{
	check(0, "front on empty StrBlob");
	return data->front();
}
const string& StrBlob::back()const
{
	check(0, "back on empty StrBlob");
	return data->back();
}

```



int *p=new int  ;//表示默认初始化为空，

int *p=new int（） ；  //表示默认初始化为0

同时 用new分配const对象也是合法的：`const int *pci= new const int(1024);`

const的对象必须进行初始化。

防止内存耗尽，可以给new一个参数，来抛出分配失败的信息：这种形式的new称为**定位new**，防止自由空间耗尽。

```cpp
int *p2=new(nothrow) int;//如果分配失败，new就返回一个空指针
```



用智能指针的好处就是，可以防止delete和new带来的一切问题。

在很多机器上delete之后的指针仍然保存着已经释放掉的动态内存的地址，这样的指针被称为**空悬指针**。

```cpp
#include <iostream>
#include<vector>
using namespace std;
shared_ptr<vector<int>> dvec()
{
    return make_shared<vector<int>>();
}
shared_ptr<vector<int>> inputVec(shared_ptr<vector<int>>pvec)
{
    int i;
    while (cin >> i)
    {
        pvec->push_back(i);
    }
    return pvec;
}
void print(shared_ptr<vector<int>>pvec)
{
    for (auto i : *pvec)
    {
        cout << i << " ";
    }
    cout << endl;
}
int main()
{
    auto pvec = dvec();
    inputVec(pvec);
    print(pvec);
    return 0;
}

```

用智能指针的好处，不用自己去想在什么时候释放内存。

使用new来初始化智能指针，智能用初始化形式，不可以赋值：

`shared_ptr<int> p(new int(42));`,但是建议还是用make_shared<>

同时不可以隐式转换。

智能指针还定义了一个名为get的函数，它返回一个内置指针，指向智能指针管理内存的对象

```cpp
shared_ptr<int> p(new int(42));
int *q=p.get();//使用q的时候要注意，不要
```



为了防止程序再异常发生后能够正确的被释放，最简单的方法就是使用智能指针

```cpp
void f(){
    shared_ptr<int> sp(new int(42));//分配一个新的对象
    //这段代码抛出一个异常，且在f中未被捕获
    //代码结束时shared_ptr自动释放内存
}
```

如果用new+delete的话，会在new后直接报错，然后delete就删不掉。



- 智能指针和哑类

并不是所有的类都定义了析构函数，特别是那些为C和C++两种语言设计的类，通常都要求用户显式释放所使用的资源。

![image-20221121164751501](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221121164751501.png)

```cpp
//如果使用智能指针管理资源不算new分配的，要传给他一个删除器（释放器，deleter）
connection c=connect(&d);
void end_connection(connection*p){disconnect(*p)}//这个就是删除器。
shared_ptr<connection>p(&c,end_connection);
```



- unique_ptr

与shared_ptr不同的是，某个时刻，只能有一个unique_ptr指向其给定的对象，当unique_ptr被销毁的时候，它所指的对象也被销毁。没有类似make_unique这样的标准库函数返回这种值。

因为只能指向一个对象，所以不支持拷贝和赋值操作。

虽然不能拷贝或者赋值，但是可以通过调用release或reset将指针的所有权从一个（非const）unique_ptr转移到另一个unique；

![image-20221121170218272](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221121170218272.png)

release会切断unique_ptr和他原来管理的对象之间的联系，release返回的指针通常被用来初始化另一个智能指针或给另一个智能指针赋值。一定要用一个返回值接受它：

```cpp
p2.release(); //错误，p2不会释放内存，而且我们会丢失指针
auto p=p2.release();
```



- weak_ptr:不控制所指向对象生存期的智能指针，指向一个由shared_ptr管理的对象，将其绑定的时候，不会影响shared_ptr的引用计数，若shared_ptr被销毁，对象直接释放，不管有没有weak_ptr指向它。

一系列操作见书本P420。

由于弱共享指针的对象有可能不存在，所以不能直接用其访问对象，必需调用lock，这个函数用于检查weak_ptr指向的对象是否仍存在。若存在返回一个指向共享对象的shared_ptr：

```cpp
//一般用法：
if(shared_ptr<int> np=wp.lock()){
    
}
```

弱智能指针weak_ptr区别于shared_ptr之处在于：

weak_ptr不会改变资源的引用计数，只是一个观察者的角色，通过观察shared_ptr来判定资源是否存在
weak_ptr持有的引用计数，不是资源的引用计数，而是同一个资源的观察者的计数
**weak_ptr没有提供常用的指针操作，无法直接访问资源，需要先通过lock方法提升为shared_ptr强智能指针，才能访问资源**

weak_ptr内几个重要成员函数：

成员函数use_count() 观测资源引用计数

成员函数expired() 功能相当于 use_count()==0 表示被观测的资源(也就是shared_ptr的管理的资源)是否被销毁

成员函数lock()从被观测的shared_ptr获得一个可用的shared_ptr对象， 进而操作资源。但当expired()==true的时候，lock()函数将返回一个存储空指针的shared_ptr


请注意强弱智能指针的一个重要应用规则：**定义对象时，用强智能指针shared_ptr，在其它地方引用对象时，使用弱智能指针weak_ptr**。

```cpp
class B; // 前置声明类B
class A
{
public:
	A() { cout << "A()" << endl; }
	~A() { cout << "~A()" << endl; }
	weak_ptr<B> _ptrb; // 指向B对象的弱智能指针。引用对象时，用弱智能指针
};
class B
{
public:
	B() { cout << "B()" << endl; }
	~B() { cout << "~B()" << endl; }
	weak_ptr<A> _ptra; // 指向A对象的弱智能指针。引用对象时，用弱智能指针
};
int main()
{
    // 定义对象时，用强智能指针
	shared_ptr<A> ptra(new A());// ptra指向A对象，A的引用计数为1
	shared_ptr<B> ptrb(new B());// ptrb指向B对象，B的引用计数为1
	
    // A对象的成员变量_ptrb也指向B对象，B的引用计数为1，因为是弱智能指针，引用计数没有改变
	ptra->_ptrb = ptrb;
	// B对象的成员变量_ptra也指向A对象，A的引用计数为1，因为是弱智能指针，引用计数没有改变
	ptrb->_ptra = ptra;

	cout << ptra.use_count() << endl; // 打印结果:1
	cout << ptrb.use_count() << endl; // 打印结果:1

	/*
	出main函数作用域，ptra和ptrb两个局部对象析构，分别给A对象和
	B对象的引用计数从1减到0，达到释放A和B的条件，因此new出来的A和B对象
	被析构掉，解决了“强智能指针的交叉引用(循环引用)问题”
	*/
	return 0;
}

```

还有一个作用就是用于线程安全的对象回调与析构——弱回调：[(6条消息) weak_ptr 的几个应用场景 —— 观察者、解决循环引用、弱回调_爱好学习的青年人的博客-CSDN博客](https://blog.csdn.net/qq_53111905/article/details/122240842)



![image-20221123190041871](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221123190041871.png)





allocator定义在头文件memory中，它帮助我们==将内存分配和对象构造分离开==，它分配的内存是原始的、未构造的。allocator也是一个模板，定义他的时候必须指明可分配的对象类型，他会根据给定的对象类型来确定恰当的内存大小。

```cpp
allocator<string> alloc;
auto const p = alloc.allocate(n);
这个allocate调用为n个string分配了内存。
```



为了使用allocate返回的内存，我们必须用construct构造对象，使用为构造的内存，其行为是未定义的。具体见课本P428-429

具体就是先allocate，然后construct，然后destory，最后deallocate

```cpp
allocator<string> alloc;
auto const p=alloc.allocate(n);
auto q=p;//q指向最后构造的元素之后的位置
alloc.construct(q++);//构造的指针q为空字符串
alloc.construct(q++,10.'c');
//如果没有构造（construct）就直接使用原始的内存，这种定义方式是错误的。

//删除内存
while(q!=p){
    alloc.destory(--q);//destory是逆序销毁的
}

alloc.deallocate(p,n);
```





智能指针面试常考：**[(7条消息) C/C++面试：什么是智能指针？智能指针有什么作用？分为哪几种？各自有什么样的特点？_OceanStar的学习笔记的博客-CSDN博客_什么是智能指针](https://blog.csdn.net/zhizhengguan/article/details/112302192)**

[(7条消息) C++智能指针总结（面试常问）_Sunrise的博客的博客-CSDN博客_智能指针 面试](https://blog.csdn.net/weixin_41969690/article/details/107912842)





## 第三部分 有关于类

### 13 拷贝控制

当定义一个类的时候，我们会显式或隐式指定此类型的对象拷贝、移动、赋值、销毁的时候要做什么，所以会定义**五种**特殊的成员函数来控制这些操作：**拷贝构造函数、拷贝赋值运算符、移动构造函数、移动赋值运算符、析构函数**。这些被称为拷贝控制。



什么是拷贝构造函数：

==如果一个构造函数的第一个参数是自身类型的引用，且任何额外参数都有默认值==，则次构造函数是拷贝构造函数

```cpp
class Foo{
public:
    Foo();  //默认拷贝构造函数
    Foo(const Foo&);//拷贝构造函数
}
```

黑马中的拷贝构造：

```cpp
//拷贝构造函数写法：
class Person {
public:
	Person(const Person &p)
	{
        //将传入对象的属性拷贝
        age = p.age；
		cout << "构造函数的调用" << endl;//如果不写，里面就是空的
	}
};
```

拷贝构造的目的是为了：拷贝一份和自身类一模一样的东西所以需要传入一个固定的自身的引用。 因为拷贝构造函数再几种情况下都会被隐式地使用，所以拷贝构造函数通常不应该是explicit的。

即使我们定义了其他的构造函数，编译器也会为我们提供一个拷贝构造函数（如果我们没有定义拷贝构造的话），这和合成默认构造函数不同。



直接初始化和拷贝初始化的区别：

![image-20221126140454817](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221126140454817.png)

拷贝初始化是通过拷贝构造函数或移动构造函数来完成的。

```cpp
vector<int> v1(10);//正确的
vector<int> v2=10;//错误的：接收单一大小参数的构造函数是explicit的。
```



拷贝构造函数使用的场景：在用=定义变量时使用；将对象作为实参传递给一个非引用形参时；从一个返回类型非引用的函数返回一个对象；用花括号列表初始化一个数组中的元素或一个聚合类中的成员。



类可以重载其赋值运算符来将其变为拷贝赋值运算符：

重载运算符必须定义为成员函数，类外的话要定义为static。

赋值运算符重载通常返回一个指向其左侧运算对象的引用。

==数组是不能拷贝的！！只能逐个赋值数组元素==

合成拷贝赋值运算符：是编译器默认的，一般用来禁止该类型对象的赋值。如果并非出于此目的，他会将右侧运算对象的每个非static成员赋予左侧运算对象的对应成员。



- 析构函数

构造函数初始化对象的非static数据成员；析构函数释放对象使用的资源，并销毁对象的非static数据成员。

==析构函数没有返回值，也不接受参数，不能被重载，对于一个给定类，只会有唯一一个析构函数。==

析构函数按照成员初始化顺序的逆序进行销毁。销毁一个内置指针类型不会delete它所指的对象，与普通指针不同，智能指针是类类型，所以具有析构函数，智能指针成员在析构阶段会被自动销毁。

==当一个对象的引用或指针离开作用域的时候，析构函数不会执行。析构函数体自身并不直接销毁成员，成员是在析构函数体之后隐含的析构阶段中被销毁的。==

```cpp
struct X {
    X() { std::cout << "X()" << std::endl; }
    X(const X&) { std::cout << "X(const X&)" << std::endl; }
    X& operator= (const X& x);
    ~X() { std::cout << "~X()" << std::endl; }
};

X& X::operator=(const X& x)//看看这
{
    std::cout << "=X()" << std::endl;
    return* this;
}
static X xs;//调用默认构造函数

int main() {
    vector<X> xv;//不调用
    X x;//调用默认构造函数
    xv.push_back(x);//调用一个拷贝构造函数
    xv.emplace_back(x);//调用一个拷贝构造函数，然后析构
    X* xn = new X(x);
    X x1(x);
    delete xn;
    {
        X x3 = x1;//调用一个拷贝构造函数
    }//离开定义域时析构
    X x2 = x1;
}//尚未析构的全部析构
```

如果将上述的函数直接=default，就是显式地要求编译器生成合成版本。同时合成的版本将隐式地声明为内联的，如果不希望是内联的，那么应该只对成员的类外定义使用=default。

 大多数的类都应该定义默认的构造、拷贝构造函数和拷贝赋值运算符。无论是隐式的还是显示的，尽量不要用合成的。

**将拷贝构造函数和拷贝赋值运算符定义为删除函数**从而阻止拷贝：但是有的类不应该定义（也不是不应该定义，而是要定义一个不拷贝的），比如iostream类需要阻止拷贝构造功能，以免多个对象写入或读取相同的IO缓冲。

```cpp
//虽然我们定义了，但是不能以任何方式使用它，在函数的参数列表后面加上=delete
class NoCopy{
    NoCopy()=default;
    NoCopy(const NoCopy&)=delete;//删除函数的定义，用来阻止拷贝
    NoCopy &operator =(const NoCopy&)=delete; //阻止赋值
}
```

`=delete`必须在函数第一次声明的时候就出现。析构函数不可以是删除的成员。如果一个类有const成员，则它不能使用合成的拷贝赋值运算符。

旧的标准是怎么做的呢：是将拷贝构造函数和拷贝赋值运算符声明为private的来阻止拷贝。但是这么做：友元和成员函数还是可以拷贝对象的。为了阻止这一现象的出现，我们只声明他们，不定义他们。==声明 但不定义一个成员函数是合法的。（除了子类继承父类的虚函数）==

```cpp
//13.18题
#ifndef _EMPLOYEE_H_
#define _EMPLOYEE_H_
#include <string>
using std::string;
class employee
{
public:
    employee() = default;
    employee(string& s) :name(s), identity(++initail_number) {}
    ~employee() {}
    employee(employee&)=delete;
    employee& operator=(employee&) = delete;

private:
    string name;
    unsigned identity;
    static unsigned initail_number;
};
unsigned employee::initail_number = 1000;
#endif // !_EMPLOYEE_H_ 

```



对于成员是用智能指针来管理动态内存的类，当拷贝、赋值或销毁类对象的时候引用计数会发生改变乃至被销毁。



因为TextQuery和QueryResult的成员是用智能指针来管理动态内存，不需要定义一个自己版本的析构函数，因此不需要拷贝和赋值函数



- 赋值运算符==常常组合了析构函数和构造函数的操作==。赋值操作会销毁左侧对象的资源，会从右侧运算对象拷贝数据。

但是顺序非常重要：先将右侧运算对象拷贝到一个局部临时对象中，然后销毁左侧运算对象的现有成员。

```cpp
HasPtr& HasPtr::operator=(const HasPtr &rhs){
    auto newp=new string(*rhs.ps);
    delete ps;
    ps=newp;
    i=rhs.i;
    return this;
}
```



swap底层的操作其实是交换指针。



某些类需要在运行的时候分配可变大小的内存空间，这种类我们通常可以使用标准库的容器来保存他们。一般用vector最好。如何自己手动模拟vector的工作原理：

对于容器底层每次开辟新空间的时候要把旧元素拷贝过去，然后销毁原本的空间，这样的操作是会带来极大的消耗的。所以底层可以使用移动构造函数来减少这种消耗：相当于移动了指针，而没有拷贝原有的数据：

![image-20221128145709860](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221128145709860.png)

管理的内存不会被拷贝，但是会接管内存的所有权。



- 对象移动（move）：

移动主要用在某些情况下：对象拷贝后就立即销毁了，这些情况下移动而非拷贝对象会大幅度提升性能。初次之外，想IO类或者是unique_ptr这样的类，这些类都包含不能被共享的资源（比如指针或者是IO缓冲）。因此这些类型的对象不能被拷贝，但是可以被移动。

- 右值引用：

为了支持移动操作，新标准引入了新的引用类型——右值引用。也就是绑定到右值的引用，用的是`&&`符号。==右值引用只能绑定到将要销毁的对象==

一般来说，左值表达式表示的是应该对象的身份，右值表达式表示的是对象的值。对于常规的引用，我们可以称它为左值引用。

![image-20221128152155787](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221128152155787.png)

![image-20221128152625655](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221128152625655.png)



move函数的作用就是将一个左值直接转化为右值

```cpp
int &&rr3=std::move(rr1);
```

使用move就默认承诺，除了对rr1赋值或销毁它之外，不会再使用它，不让和浅拷贝一样。

同时对于move不听歌using的声明，如果没有using namespace std；的话，要：`std::move;`



**左值引用和右值引用的区别**：

左值引用：不能将其绑定到要求转换的表达式、字面常量或是返回右值的表达式。返回左值的函数有赋值、下标、解引用和前置递增递减运算符。
右值引用：可以绑定到这类表达式，但是不能绑定到左值上。返回右值的函数有算数、关系、位以及后置递增递减运算符。



```cpp
int f();
vector<int>vi(100);
int& r1 = f();//f()的返回值相当于一个常量，只能使用const的左值引用或者右值引用
int& r2 = vi[0];//下标，左值引用
int& r3 = r1;//此时r1相当于一个变量，左值引用
int& r4 = vi[0] * f();//算术运算，右值引用
```





- 移动构造函数和移动赋值运算符：

和拷贝构造操作有所不同的是：移动主要是从给定对象窃取资源而不是进行拷贝操作。

移动构造必须保证，一旦资源完成移动，源对象必须不再指向被移动的资源——这些资源的所有权已经归属新的对象。

move的底层逻辑：

```cpp
StrVec::StrVec(StrVec &&s) noexcept : elements(s.elements),first_free(s.first_free),cap(s.cap){
    s.elements=s.first_free=s.cap=nullptr;//把原本的滞空
}
```

移动构造函数不分配任何新内存，它接管给定的StrVec中的内存。在接管内存之后，他会将给定对象中的指针都置为nullptr，这样就完成了从给定对象的移动操作。此对象将会继续存在



==移动构造一般针对右值，拷贝构造一般针对左值==。如果没有移动构造函数，那么右值也会被拷贝。



五个拷贝控制成员应该看成一个整体：

- 拷贝构造函数
- 拷贝赋值运算符
- 析构函数
- 移动构造函数
- 移动赋值运算符



通过调用for来讲construct从旧内存中将元素拷贝到新内存中：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221129142312515.png" alt="image-20221129142312515" style="zoom:67%;" />

现在可以用移动迭代器来进行遍历：

移动迭代器返回的是一个右值引用，通过使用标准库的`make_move_iterator`函数将一个普通迭代器转换为一个移动迭代器。

移动赋值运算符：

```cpp
inline StrVec& StrVec::operator=(StrVec&rhs)
{
    if (this != &rhs) {
        free();
        elements = rhs.elements;
        first_free = rhs.first_free;
        cap = rhs.cap;
        rhs.elements = rhs.first_free = rhs.cap = nullptr;
    }
    return *this;
}
```



==对于unique_ptr的不能拷贝的规则：==

不能拷贝unique_ptr的规则有一个例外：我们可以拷贝或赋值一个将要被销毁的unique_ptr，编译器知道要返回的对象将要被销毁，因此会执行一种特殊的"拷贝" -- 移动。最常见的就是从函数返回unique_ptr，因为返回的是右值。



区分移动和拷贝的重载函数通常有一个版本接受一个`const T&`的拷贝版本，和一个`T&&`的移动版本

```cpp
void push_back(const X&);//拷贝版本：能绑定到任意类型的X
void push_back(X&&); //移动：只能绑定到类型X的可修改的右值
```

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221129144430401.png" alt="image-20221129144430401" style="zoom:70%;" />





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



总结：移动构造和移动赋值接受一个非const的右值引用，拷贝版本接受一个const的左值引用。





### 14 重载运算与类型转换

当运算符作用于类类型的运算对象是，可以通过重载重新定义该运算符的含义，重载一般由关键字operator和其后要定义的运算符号共同组成，和其他函数一样，重载的运算符号也包含返回类型，参数列表和具体的函数体。

如果一个运算符函数是一个成员函数，则它的第一个（左侧）运算对象绑定到隐式的this指针上，因此成员函数的显示参数数目比运算符的运算对象少一个。

==如果是类的成员，那么重载运算符它至少要含有一个类类型的参数，不可以两个int这样的，或者一个int 一个string。==

有四个运算符不能被重载：`::   .*    ?:   .`

 **有关于运算符重载的返回类型：**

- 逻辑运算符和关系运算符一个返回bool
- 算数运算符应该返回应该类类型的值
- ==赋值运算符和复合运算符应该返回左侧运算对象的一个引用==

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221130205442874.png" alt="image-20221130205442874" style="zoom:70%;" />

输出运算符的第一个形参一般（90%）都是非常量，因为输出流一般会改变状态

对于`<<`的重载

```cpp
ostream &operator<<(ostream &os,const Sales_data &item){
    os<<item.isbn()<<;
    return os;//返回他的ostream形参
}
```

```cpp
ostream& operator<<(ostream&os,const Date& d)
{
    os << d.year << "年" << d.month << "月" << d.day << "日" << endl;
    return os;
}
```



对于重载输入运算符>>

![image-20221130211102132](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221130211102132.png)

注意第一第二个参数都是非常量，同时要再内部if（is）来检查合法性。

```cpp
istream& operator>> (istream& is, Sales_data& s)
{
    double price;
    is >> s.bookNo >> s.units_sold >> price;
    if (is) {
        s.revenue = price * s.units_sold;
    }
    else {
        s = Sales_data();
    }
    return is;
}

```



- 算术运算符和关系运算符重载：

一般来说会定义成非成员函数以允许对左侧或右侧的运算对象进行转换。而且这些运算符一般不需要改变运算对象的状态所以形参都是常量的引用。

如果同时定义了算数运算符和相关的复合赋值运算符

定义相等运算符返回值一般是bool类型，return就直接return两个变量的等式即可，定义不等于：

```cpp
bool operator!=(const Sales_data &lhs,const Sales_data &rhs){
    return !(lhs==rhs);
}
```

一般如果定义了operator==，也需要定义operator！=；

```cpp
bool operator<(const StrBlob&lhs, const StrBlob&rhs)
{
	return lexicographical_compare(lhs.data->begin(), lhs.data->end(), rhs.data->begin(), rhs.data->end());
	/*lexicographical_compare()算法可以比较由开始和结束迭代器定义的两个序列。它的前两个参数定义了第一个序列，
	第 3 和第 4 个参数分别是第二个序列的开始和结束迭代器。默认用 < 运算符来比较元素，但在需要时，
	也可以提供一个实现小于比较的函数对象作为可选的第 5 个参数。如果第一个序列的字典序小于第二个，
	这个算法会返回 true，否则返回 false。所以，返回 false 表明第一个序列大于或等于第二个序列。*/
}
bool operator>(const StrBlob& lhs, const StrBlob& rhs)
{
	return lexicographical_compare(rhs.data->begin(), rhs.data->end(),lhs.data->begin(), lhs.data->end());
}
```



==和=要区分开来

- 赋值运算符operator=,返回类型也是左值的引用,传入参数类型是initializer_list

```cpp
StrVec &StrVec::operator=(initializer_list<string> il){
    auto data=alloc_n_copy(il.begin(),il.end());
    free();//销毁原本对象中的内存
    elements=data.first;
    first_free=cap=data.second;
    return *this;
}
```



- 下标运算符通常以访问元素的引用作为返回值，这样的好处是下标可以出现在赋值运算的任意一端。


如何区分前置版本的++和后置版本的++：后置版本接收一个额外的不被使用的int类型的形参（占位）：

```cpp
StrBlobPtr& operator++();//前置
StrBlobPtr& operator++(int);//后置
{
//后置在使用前需要记录当前对象的状态
	StrBlobPtr ret=*this;
	++*this;//后置里面调用前置
    return ret;
}
```



![image-20221201153050074](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221201153050074.png)

箭头运算符重载必须返回类的指针或自定义了箭头运算符的某个类的都西昂。

- 函数调用运算符的重载：也就是对（）的重载

如果重载了函数的调用运算符，则我们可以像使用函数一样使用该类的对象，最常见的：

```cpp
class MyCompare
{
public:
    bool operator()(int v1, int v2)//表示重载小括号
    {
        return v1 > v2;
    }
};
set <int,MyCompare>s2;
```

同时重载了（）的话，可以直接用一个类的对象来接受一个参数。

```cpp
class absInt{
    int opreator() (int val) const{
        return val<0?-val:val;
    }
};

int i=-42;
absInt abs;
int ui=abs(i);
```



**函数对象**：所以==重载小括号必须在类内作为类的成员函数==，如果类定义了调用运算符，则该类的对象称为**函数对象**。（有的时候也叫仿函数？）

**函数对象最常用做为泛型算法的实参。**

重载运算符函数的参数数量和该运算符作用的运算对象的数量一样多。函数调用运算符（）最多可以传256个参数，因此在重载时，最多也能接受256个参数用作运算。

```cpp
class PrintStr{
public:
  	PrintStr(istream& i) :is(i){}
  	string& operator()();
private:
    istream& is;
    string line;
};

string& PrintStr::operator()(){
    if(getline(is,line)){
        return line;
    }
    return line=string();//临时对象表示空字符串
}
```



怎么让输入的每一行保存到一个vector里面作为一个元素保存：

```cpp
string s;
while (getline(is, s))
{
    svec.push_back(s);
}
```



- lambda就是一个函数对象

可以代替上述的重载的函数对象

lambda表达式产生的类不含默认构造函数、赋值运算符和默认析构函数。

还有一种是标准库定义好的关系仿函数：

![image-20221202195420425](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221202195420425.png)



有关于lambda的使用：

```cpp
#include <iostream>
#include<functional>
#include<algorithm>
#include<vector>
using namespace std::placeholders;
using namespace std;
int main()
{
    vector<int>ivec{ 1,10,100,1111,2048,4096 }; 
    int count = count_if(ivec.begin(), ivec.end(), bind(greater<int>(), _1, 1024));
    cout << count << endl;
    vector<string>svec{ "pooh","pooh","pooch","pooh" ,"poog" };
    auto iter=find_if(svec.begin(), svec.end(), bind(not_equal_to<string>(), _1, "pooh"));
    cout << *iter << endl;
    vector<int>ivec2{ 1,2,3,4,5 };
    transform(ivec2.begin(), ivec2.end(),ivec2.begin(), bind(multiplies<int>(), _1, 2));
    for (auto i : ivec2)
        cout << i << " ";
}

```



- C++可以调用的对象有：函数、函数指针、lambda表达式、bind创建的对象、以及重载了函数调用运算符的类。

调用形式：`int(int,int);`这种调用形式表现的是：一种函数形式，接受两个int、返回一个int。

容器存入的类型或、map的键值对形式可以存入这种函数的调用形式：`map<string,int(*)(int,int)> binops;`

```cpp
binops.insert({"+",add});//这种情况是允许的 add是一个函数的名称，相当于传入函数指针。
```



- 标准库function类型：

function也是一个模板，可以把函数的调用形式放进来。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221203193425091.png" alt="image-20221203193425091" style="zoom: 33%;" />



然后重写map的传入参数，第二个参数变成function<int(int,int)>类型传入。

![image-20221203193717299](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221203193717299.png)

对于重载的版本的函数不能直接放到function中，因为直接把函数名字给编译器编译器分辨不出来，可以使用lambda表达式来消除二义性，也可以用指针类型传入消除二义性：

```cpp
int(*fp) (int,int) =add;
binops.insert({"+",fp});
```

例子：

```cpp
#include <iostream>
#include<functional>
#include<map>
using namespace std;
class add
{
public:
    int operator()(int n1,int n2)
    {
        return n1 + n2;
    }
};
class division
{
public:
    int operator()(int n1, int n2)
    {
        return n1 / n2;
    }
};
class  subtraction
{
public:
    int operator()(int n1, int n2)
    {
        return n1 - n2;
    }
};
class multiplication
{
public:
    int operator()(int n1, int n2)
    {
        return n1 * n2;
    }
};
class module
{
public:
    int operator()(int n1, int n2)
    {
        return n1 % n2;
    }
};
void  Calculator()
{
    map<string, function<int(int,int)>>binops;
    binops.insert({ "+", add() });//类重载（），作为临时对象传入必须要+（）
    binops.insert({ "/",division() });
    binops.insert({ "-",subtraction() });
    binops.insert({ "*",multiplication() });
    binops.insert({ "%",module() });
    int num1, num2;
    string ope;
    if (cin >> num1 >> ope >> num2)
    {
        cout << num1 << ope << num2 << " = " << binops[ope](num1, num2) << endl;
    }
    else
    {
        cout << "Please enter the correct expression" << endl;
    }
}

```

显示的类型转化运算符：

形式一般是：`operator type() const`

```cpp
explicit operator int() const{return val};
```



也可以通过调用时候的形式判断是什么函数：

```cpp
a.operatorsym(b);//a有一个成员函数
operatorsym(a,b);//那operatorsym是一个普通函数。
```



### 15.面向对象程序设计

面向对象程序设计（object-oriented programming）的核心思想是数据抽象、继承和动态绑定。

在C++中，基类将类型相关的函数与派生类不做改变直接继承的函数区分对待，对于派生类需要各自定义适合版本的函数就声明为虚函数

```cpp
class Quote{
public:
    std::string isbn() const;
    virtual double net_price(std::size_t n) const;
}
```

派生类在重写的时候可以不写virtual。

在C++11的新标准中允许派生类显式地著名它将使用哪个成员函数改写基类的虚函数，具体是在该函数后面加一个override（覆盖）

```cpp
class quote:public Quote{
public:
    double net_price(std::size_t) const override;
}
```



在C++语言中，当我们使用基类的引用（或指针）调用一个虚函数的时候将会发生动态绑定。

一般在继承关系的根结点的累通常会定义一个虚析构函数。任何除了构造函数之外的非静态函数都可以是虚函数。

==protected和private的主要区别是在于继承中。父子关系，子类可以访问protected，私有子类不能访问。==

proteceted为受保护的访问标号.protected成员可以被该类的成员.友元和派生类成员(非友元)访问,而不可以被该类型的普通用户访问.而private成员只能被基类的成员和友元访问.派生类不能访问.



以下就是一个动态绑定的实例：根据传入的指针类型不同，来选择自己对应的调用类型。

```cpp
class Quote {
public:
	Quote() = default;
	Quote(const string& book, double sales_price) : bookNo(book), price(sales_price) {}
	string isbn() const { return bookNo; }
	//返回给定数量的书籍的销售总额,派生类改写并使用不同的折扣计算方法
	virtual double net_price(size_t n)const { return n * price; }
	virtual ~Quote() = default;
private:
	string bookNo;				//书籍的ISBN编号
protected:
	double price = 0.0;			//代表普通状态下不打折的价格
};
double print_total(ostream& os, const Quote& item, size_t n) {
	//根据传入item形参的对象类型调用Quote::net_price
	//或者Bulk_quote::net_price
	double ret = item.net_price(n);
	os << "ISBN: " << item.isbn() << " # sold:" << n << " total due:" << ret << endl;
	return ret;
}

```



在一个对象中，继承自基类的部分和派生类自定义的部分不一定是连续存储的。

![image-20221204151233083](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221204151233083.png)

可以用父类的指针指向子类的对象，指向的过程中会发生隐式的转化。原因在于派生类对象中含有于其基类对应的组成部分，这就是继承的关键所在。

从父类继承过来的成员在子类的构造函数中调用父类的构造函数进行初始化，而子类自己的数据成员则在自己的析构函数中构造。

派生类可以访问基类中公有成员和受保护的成员。

派生类也可以访问基类中的静态成员，但是不论从基类中派生出来多少个派生类，对于每个静态成员来说都只存在唯一的实例。

在C++11中给出了一种新的关键词防止一个类被继承：

```cpp
class NoDerived final {} //
```

在类名的后面直接跟一个final关键字，可以防止类被继承。

 

- 类型转化对于存在继承关系的类是一个重要的例外：

可以将基类的指针或者引用绑定到派生类对象上。

某一个指针或者引用的静态类型可能与其动态类型不一致，如果表达式既不是引用也不是指针，则它的动态类型永远与静态类型一致。

==不存在基类想派生类的隐式类型转化（基类作为右值）==

```cpp
Quote base;
Bulk_quote* bulkP=&base; //错误，不能将基类转换成派生类
Bulk_quote& bulkP=base;  //错误，不能将基类转换成派生类
```



派生类向基类的自动类型转换只针对指针或引用类型有效，类类型之间无效。

静态类型在编译时已经确定了,它是变量声明时的类型或表达式生成的类型.而动态类型则是变量或表达式表示的内存中的对象的类型.动态类型直到运行时才能知道.

对于虚函数来说，必须为每一个虚函数都提供定义，即使它后面不用被用到（那直接不定义是不是更好），==原因在于当某个虚函数通过指针或引用调用的时候，编译器产生的代码直到运行时才能确定应该调用哪个版本的函数，当使用普通类型（非引用和非指针）的表达式调用虚函数的时候，在编译的时候就会将调用的版本确定好。==

这也时被称为OOP**的多态性**：

- 使用基类的引用或指针调用基类中定义的一个函数时，我们不知道该函数的真正作用对象的类型，可能是：基类对象，也可以是派生类对象
- 如果该函数是虚函数，直到运行的时候才知道到底执行哪个版本，判断的依据是引用或指针所绑定的对象的真实类型。
- 派生类中的继承自基类的虚函数，返回值也要和父类中的返回值相同。当类返回的是类本身的指针或引用的时候可以有例外。



回避虚函数的机制，强制调用指定的版本，不发生动态绑定：

```cpp
double undiscounted= baseP->Quote::net_price(42);
```

强行调用基类中定义的函数版本，不管baseP的动态类型是什么，直接用->调用类型。一般只有虚函数需要调用基类的虚函数版本的时候才要这么做。



- 抽象基类：含有纯虚函数的类就是抽象基类

纯虚函数（pure virtual）：直接将基类中的虚函数定义为纯虚函数，没有实际意义，无需定义

纯虚函数语法：`virtual int(返回值类型) getResult()（函数名） （参数列表） = 0`，

就是把大括号去掉，变成=0；

==如果一个类是抽象基类，那么就不能直接创建一个抽象基类的对象。==

继承自抽象基类的派生类如果没有重写自己的虚函数的话，也被认作为是一个抽象基类，也不可以定义自己的对象。

```cpp
class Disc_quote :public Quote {
public :
	Disc_quote(const string& book = " ", double sales_price = 0.0, size_t  qty = 0, double disc = 0.0) :
		Quote(book, sales_price), quantity(qty), discount(disc) {}
	double net_price(size_t cnt) const = 0;
protected:
	size_t quantity;
	double discount;
};
class Bulk_quote :public Disc_quote {
public:
	Bulk_quote(const string& book = "", double sales_price = 0, size_t qty = 0, double disc_rate = 0) :
		Disc_quote(book, sales_price, qty, disc_rate) {}
	double net_price(size_t cnt)const {
		if (cnt > quantity)	return cnt * (1 - discount) * price;
		else return cnt * price;
	}
};

```





protected关键字来声明那些类希望与派生类共享，但是不想被其他公共访问使用的成员。

派生类的成员或友元只能通过派生类对象来访问基类的受保护成员。只有通过这个对象你来才能访问基类受保护的对象，你直接在派生类中无法访问：

```cpp
class base{
protected:
	int m;    
};
class derive:public base{
  	void clobber(derive&);//这个函数可以访问m
    void clobber(base&);//这个就不可以
    int j;
};
void clobber(derive &d) {d.j=d.m=0;}//允许
```

**不同的继承关系的不同作用：**

- 比如说公有继承：public继承和private继承对于派生类的成员是否能访问其直接基类的成员并没有什么影响，访问权限只和基类中成员的访问说明有关。而继承关系中的权限是干嘛用的呢？比如你private继承的，那么在派生类中，基类继承过来的东西即使是public的也会变成private的。

- 如果一个类被作为另外一个类的友元，那么被作为友元的那个类的派生类无法继承它的继承关系。

- 可以一个类被private继承了，但是你又想让个别成员改变课访问性，可以使用：`using Base::size;`这样的方式让继承而来的成员变成派生类的公有成员，从而可以使用。

struct默认public，class 默认private，同样继承的时候如果不说明继承方式，也是按照前面的类型继承的。



派生类的作用域是嵌套在基类的作用域内的。也正是因为了这种作用域的嵌套，才使得我们的派生类可以自由地使用基类的成员。如果派生类中重新定义了和基类名字相同的成员，那么会覆盖原本基类中的成员，用派生类中的代替它。一般来说都是在自底向上查找，现在自己的类里面找，然后向上找它的基类。



- 现在可以理解为什么基类与派生类中的虚函数必须拥有相同的形参列表了，加入接受的参数不同，就无法通过基类的引用或指针调用派生类的虚函数。

```cpp
class Animal
{
public:
	//在函数前面加virtual
	virtual void speak()
	{
		cout << "动物在说话" << endl;
	};
};

class Cat:public Animal 
{
public:
	void speak()
	{
		cout << "喵喵喵" << endl;
	};
};

//原因在于：地址早绑定，在编译阶段就确定了地址。
//如果想执行让猫说话，那么函数地址就不能提前绑定，需要在运行阶段绑定。
void doSpeak(Animal &animal)//Animal & animal = cat;
{
	animal.speak();
}


void test() 
{
	Cat cat;
	doSpeak(cat);
}
```



继承关系对于基类拷贝控制最直接的影响在于基类通常应该定义一个虚析构函数。

通过在基类中将析构函数定义成虚函数以确保执行正确的析构函数版本，保证子类可以重写，析构的时候可以析构正确的版本。

```cpp
class Quote{
public:
    virtual ~Quote()=default;
};
```

派生类的构造函数会先调用父类的构造函数之后，再用自己的类型调用赋值派生类中别的元素。

对于派生类的析构函数来说，它除了销毁派生类自己的成员之外，**还负责销毁派生类的直接基类**，该直接基类又销毁它自己的直接基类，一次类推直至继承链的顶端。

对于派生类的拷贝/移动构造函数，除了要拷贝/移动自己的成员，还需要拷贝和移动基类部分的成员。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221205193441900.png" alt="image-20221205193441900" style="zoom: 33%;" />



**而派生类的析构函数与上述二者不同**：派生类对象基类的部分是隐式销毁的，因此，派生类的析构函数与构造函数和赋值运算符不同的是，派生类的析构函数值需要负责销毁由派生类自己分配的资源。

创建派生类时，是按照先创建相应基类部分，然后对应派生类自己的成员初始化。而析构是反过来的，先销毁自己的，再销毁基类的。

- 在C++11中，派生类能过重用其直接基类的构造函数，但他并不是从基类继承过来的，这几个bigfive函数都不能直接继承过来，而唯独构造函数可以用using构造声明：

  ```cpp
  class Bulk_quote : public Disc_quote{
  public:
      using Disc_quote::Disc_quote;//继承Disc_quote的构造函数
  }
  ```

  讲道理using声明语句只是令某个名字在当前作用域内可见，而当作用于构造函数的时候，using声明语句将令编译器产生代码。

- 向容器中放基类可以，放派生类也可以，但是它的派生部分将被忽略掉。因此，容器和存在继承关系的类型是无法兼容的。

```cpp
vector<Quote> basket;
basket.push_back(Quote("0-201-82470-1",50));
```

所以为了解决上述的问题，方法就是：==希望再容器中存放具有继承关系的对象的时候，实际存放的通常是基类的智能指针。==这些指针所指的对象的动态类型可能是基类类型，也可能是派生类类型。

```cpp
vector<shared_ptr<Quote>> basket;
basket.push_back(make_shared<Quote>("0-201-8",50));//直接基类
basket.push_back(make_shared<Bulk_quote>("0-22-11",50,10,0.25));//调用基类的
cout<<basket.back()->net_price(15)<<endl;//由于传入指针要解引用
```

当传入子类的智能指针对象时，在调用的时候会自动转换为父类的智能指针对象。



### 16.模板与泛型编程

OOP和泛型编程：

相同：都能处理在编写程序时不知道类型的情况，

不同：OOP能处理类型在程序运行之前都未知的情况，而在泛型编程中，在编译的时候就能直到类型了。



- 类型参数前面必须使用关键字class或typename

```cpp
template<typename T>
class A{};

template<typename T,U>//错误，正确应该是：template<typename T,typename U>
class A{};

```

==当编译器遇到一个模板定义的时候，它并不生成代码，只有当实例化出模板的一个特定版本的时候，编译器才会生成代码==

自己定义一个find函数：

```cpp
template<typename Iterator, typename Value>
Iterator find(Iterator first, Iterator last, const Value& v)
{
	for ( ; first != last && *first != value; ++first);
	return first;
}
```

constexpr和inline说明符放在模板参数列表之后，返回类型之前。

因为大多数类只定义了 `!=` 操作而没有定义 `<` 操作，使用 `!=` 可以降低对要处理的类型的要求。



类模板与函数模板的不同在于：==不能为类模板推断模板参数的类型，也就是不能自动推导，要用<>显示声明类型==

![image-20221206144828406](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221206144828406.png)



- 可变参数模板（variadic template）：接受可变数目参数的模板函数或模板类。可变数目的参数被称为**参数包**，参数包可以用在函数中，也可以用在模板中。和initializer_list的区别在于，它可以放各式各样不同类型的参数，而initializer_ list只能放一种类型的多个参数。
- 用`...`来表示，

```cpp
template<typename T, typename... Args> //Args 是一个模板参数包，表示零个或多个模板类型参数，说明后面可能会出现多个类型
void foo(const T&t, const Args& ... rest)//rest表示0个活多个函数参数

//使用：
int i=0;double d=3.14;string s="666";
foo(i,s,42,d);
```

如果想知道包中有多少元素的时候，可以使用sizeof...运算符，返回值是一个常量表达式。

``` cpp
template<typename T, typename ...Args>
void foo(T t, Args ...args)
{
    std::cout << sizeof...(Args) << std::endl;//输出类型参数的数目
    std::cout << sizeof...(args) << std::endl;//输出函数参数的数目
}
```



可变参数的函数一般都是递归实现的。第一步调用处理包中的第一个实参，然后用剩余的实参调用自身。为了终止递归，最后还需要定义一个非可变参数的最终的同名重载函数：如下

![image-20221207141041508](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221207141041508.png)

当定义可变参数版本的函数时，非可变参数版本的声明必须在作用域中，否则会无线递归，因为本来可变参数版本也是可以被单一参数调用的，只是说写了一个单一参数的版本更特例化。



- 定义特例化函数模板：特例化一个函数模板的时候，必须位原模版中的每个模板参数都提供实参。应用关键字template后直接跟一对空的<>,指明我们将为原模板的所有模板参数提供实参：

```cpp
template<>
int compare(const char* const &p1,const char* const& p2){
    return strcmp(p1,p2);
}
```

==特例化的本质是实例化一个模板，而非一个重载。==



- 类模板的特例化：特例化类模板的时候，也需要在原模板定义所在的命名空间中特例化它。

同时类模板的特例化可以是部分的，它本身也是一个模板而不是重载，使用它的时候，用户还必须为那些在特例化版本中未指定模板参数的成员提供实参：

![image-20221207144518901](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221207144518901.png)

###后面几章的知识补充

### 随机数

- 原本在C中生成随机数（伪随机数的方法）：

Rand（）%100 表示生成随机数为0-99的随机数

Int num=rand（）%100+1；表示生成1-100的随机数

Rand生成的是伪随机数，如果要使随机数随时间变化必须添加随机数种子，防止每次随机数每次都一样

Srand（（unsigned int）time（NULL））  同时在一开始要包含一个头文件#include<ctime>



- C++不应该使用库函数rand，而应该使用default_random_engine类和恰当的分布类对象。

随机数引擎和分布的使用：随机数引擎是函数对象类，他们定义了应该调用运算符，该运算符不接受参数并返回应该随机unsigned的整数：

```cpp
default_random_engine e;//生成随机无符号数，不接受参数
for(size_t i=0;i<10;i++){
    cout<<e()<<" ";
}
```



为了得到一个在指定范围内的数，我们使用一个分布类型的对象：

```cpp
uniform_int distribution<unsigned> u(0,9);
default_random_engine e;
for(size_t i=0;i<10;i++){
    cout<<u(e)<<" ";
}
```

所以说随机数发生器的时候，是指分布对象和引擎对象的组合。

==一个给定的随机数发生器已知会生成相同的随机数序列，如果一个函数定义了局部的随机数发生器，应该将其（包括引擎和分布对象）定义为static的。否则，每次调用函数都会生成相同的序列==

```cpp
vector<unsigned> good_randVec(){//一个函数
    static default_random_engine e;
    static uniform_int_distribution<unsigned> u(0,9);
    vector<unsigned> ret;
    for(size_t i=0;i<100;i++){
        ret.push_back(u(e));
    }
    return ret;
}


//调用的时候：
vector<unsigned> v1(good_randVec());
```

设置随机发生器的种子：

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221207164052436.png" alt="image-20221207164052436" style="zoom: 67%;" />

种子是由随机数引擎产生的，比如`e.seed(3634);`

相同的种子数会生成相同的序列。

可能更常用的方法是利用time系统函数，它返回一个特定时刻到当前经过了多少秒

```cpp
default_random_engine e(time(0));
```

但是由于：**time返回以秒计时，因此这种方式只适用于生成种子的间隔为秒级或更长，如果间隔很短就无效了。**

生成一个随机均匀分布的函数：

```cpp
#include <random>
#include <iostream>

unsigned random_func()
{
	static std::default_random_engine e;
	static std::uniform_int_distribution<unsigned> u;
	return u(e);
}

int main()
{
	
	std::cout << random_func() << std::endl;

	return 0;
}
```



允许指定最大最小值，同时指定随机种子的哈数：

```cpp
unsigned random_func(unsigned i, unsigned min, unsigned max)
{
	static std::default_random_engine e(i);
	static std::uniform_int_distribution<unsigned> u(min, max);
	return u(e);
}
```

- 生成随机浮点数：

同样的，也是用上面的`std::uniform_int_distribution<double> u(min, max);`来对随机引擎做一个映射。

```cpp
std::default_random_engine e;
std::uniform_int_distribution<double> u(0, 1);
cout<<u(e)<<" ";
```



- 生成非均匀分布的随机数：

其实新的版本有20种分布方式，如果想细究的话见书本附录，这里只说一下正态分布的方法：

```cpp
default_random_engine e;
normal_distribution<unsigned> n(4,1.5);
cout<<n(e)<<endl;
```

定义在cmath头文件中的lround函数可以将每个浮点数摄入到最近的整数。



### 异常处理

异常处理能够让程序拥有在独立开发的子系统之间协同处理错误的能力。

通过**抛出（throwing）**一条表达式来**引发（raise）**一个异常。被抛出的表达式的类型以及当前的调用链共同决定了那段处理代码将被用来处理该异常。

- throw语句：

```cpp
//throw后面紧跟一个表达式，其中表达式的类型就是抛出的异常类型
throw runtime_error("***");
```

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221208155502358.png" alt="image-20221208155502358" style="zoom: 67%;" />

上述是C++标准可以提供的标准异常，必须用一个string对象来初始化，一般就是直接在后面+（“”），输入你想给用户的提示。

- try与catch语句

![image-20221208155950392](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221208155950392.png)

![image-20221208160023871](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221208160023871.png)



当执行一个throw时，跟在throw后面的语句将不再被执行。程序的控制权直接从throw转移到与之匹配的catch模块。因为跟在throw后面的语句将不再被执行，所以throw语句的用法有点类似于return，通常作为条件语句的一部分或者作为某个函数的最后一条语句。当throw出现在一个try语句内时，检查与该try块关联的catch子句，找不到退出这个函数继续找。这个过程被称为**栈展开**过程，栈展开过程沿着嵌套函数的调用链不断查找，知道找到了与异常匹配的catch子句为止。如果一个异常没有被捕获，则它将终止当前的程序。

栈展开的过程中某些对象会被自动销毁，比如栈展开的过程中推出了某个块，那么这个块里面的局部对象或者说是类对象就会被销毁。

为了一次性捕获所有的catch，我们使用省略号作为异常声明，这样的处理代码可以捕获所有的异常：

```cpp
void mainip(){
    try{
        
    }
    catch(...){
        throw;
    }
}
```

noexcept跟在函数最后面可以防止异常抛出。

![image-20221208162355509](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221208162355509.png)

异常情况的catch的时候需要按照这个顺序自顶向下。



###虚继承









### 18.大型程序的工具

18.2命名空间

可以把每一块代码放在一个命名空间里面，然后每个空间互不干扰

```cpp
namespace **命名空间的名字**{
    
}//最后面不用；和块一样。
```

想要指定某一个命名空间里面的东西，需要和写类一样，用::把命名空间说清楚

命名空间可以是不连续的，如果之前定义了一个namespace nsp，后面又来一个namespace nsp，那么就是对前面那个命名空间做一些修改。

如果有#include "**.h"的操作的话，一定要在打开命名空间之前。而且一般不把#include放在命名空间内部。
