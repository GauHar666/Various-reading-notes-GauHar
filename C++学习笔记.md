# C++学习笔记

1.hello world 的书写

```cpp
#include<iostream>

using namespace std;

 

int main()

{

  cout << "hello world" << endl;

  system("pause");

 

  return 0;

 

}

 
```

2.//单行注释  `/*多行注释*/`

3.变量 int 整形（int 变量名=变量初始值；）

4.常量：宏常量#define 一般写在main函数前面 常量：const修饰变量 可以写在main函数里面

Const int **=**；

5.变量只能由字母、数字、下划线构成，第一个字符必须为字母或下划线，区分大小写。

6.<< **** << 内部是可以自己定义输出的变量

7.C++编程中一定要注意

8.整型：==short（短整型/2字节） int（4字节）  long（4字节）  longlong(8字节)==

9.sizeof（数据类型/变量） 用于统计数据类型所占内存大小

10.实型（浮点型）：用于表示小数：float（单精度）7位有效数字、double（双精度）15-16位有效数字。

11.字符型：char ch =‘a’；单引号里面只有一个字母

==a-97 A-65==

水平制表符\t  一般用于对齐

12.字符串：char 变量名[ ]=”字符串值”  或  string 变量名=“字符串值”，前提是要在头文件定义#include <string>

13.布尔类型bool

bool flag=true/false  true=1 false=0；

14.数据的输入：==cin>>变量，相当于定义好了一个数据类型，但是你要给定一个输入值。==（注意后面是大于号。）  int num=0； cin>>给定值； 如果想看到给定值再输出。

15.运算符：%表示取余数（10%3=1）  前置递增：a=2；b=++a a=3，b=3

  后置递增：a=2；b=a++  a=3，b=2；

16.幅值运算符：+=、-=、*=、/=  a+=2相当于a=a+2；

17.比较运算符：==（相等于），！=（不等于），输出结果只有可能是0，1即真或者假两种。

18.逻辑运算符：！非，&&与，||或

19.if（条件），同时if后面不要加分号！！  If（条件）{ }  else（）……

If（）  else if（）  ……else（）

20.嵌套if语句：if里面再来个if

21.三目运算符  表达式1？表达式2：表达式3 如果表达式1为真，执行表达式2，并输出表达式2的结果。如果表达式1为假，则执行表达式3，并返回表达式3的值。

例如c=（a>b?a:b），同时返回值是变量。

22.选择结构：switch语句

Switch（表达式）

{

Case 1:break;

Case 2:break;

………

Default 表示不符合上面任何一个case。

**Case 后面要加冒号！！！同时每个case要加break！！！**

 

23.循环结构：

While（循环条件）{循环语句}

满足循环条件 就一直执行循环语句内的东西

退出循环要写个break！！！

 

Do{循环语句}while（循环条件）

与while的区别：会先进行一次循环，然后再判断循环条件。

 

For循环for（起始表达式；条件表达式；末尾循环体）{循环语句；}

For（int i=0;i<100;i++）

{ 你要在循环中做什么

}

24.生成随机数的指令

Rand（）%100 表示生成随机数为0-99的随机数

Int num=rand（）%100+1；表示生成1-100的随机数

Rand生成的是伪随机数，如果要使随机数随时间变化必须添加随机数种子，防止每次随机数每次都一样

Srand（（unsigned int）time（NULL））  同时在一开始要包含一个头文件#include<ctime>

 

 

25.获取一个数字的个位、十位和百位的方法

如153：个位：153%10=3

​       十位153/10=15 15%10=5（先整除，再取模）

​       百位153/100=1

 

26.嵌套循环：

For中for

外层循环（i） 内层（j）

 

27.跳转语句：continue，表示跳过本次循环中未执行的语句，继续下一次循环。

到了continue 后面的循环不执行了，直接执行下一次的代码。

Break是直接退出循环。  如：输出基数的代码

For（int a=0；a<100;a++）

{ if(a%2=0) {continue;}  cout<<i<<endl;}

28.跳转语句中的：goto  可以无条件的跳转代码

语法：goto 标记；  如果标记的名称存在，执行到goto语句时，会跳转到标记的位置。

标记一般是纯大写，  比如说在第二行代码写了一个goto FLAG; 就会去找FLAG

第五行前面写了FLAG: 则会直接跳到第五行。（一般不用，不好维护代码）

 

29.数组定义的方式

（1）数据类型  数组名[ 数组长度 ]；

（2）数据类型  数组名[ 数组长度 ]={ 值1，值2，…}；

（3）数据类型  数组名[ ]={ 值1，值2，…}；

数组中每个元素都是相同的数据类型

数组中第一个数据a[0],第二个a[1] ……  特别注意：数组元素的下标是从0开始的

 

取址符号&a[0]

 

30.换值 不能直接换，会覆盖，所以要通过一个临时变量，a=c，b=a，c=b；这样的

交换代码示例：

int temp=arr[j+1];

arr[j]=arr[j+1];

arr[j+1]=temp;

 

31.冒泡排序：每一轮把最大的找出来，排序总轮数=元素个数-1

内层每次对比次数：j<元素个数-当前轮数-1

 

32.二维数组

（1）数据类型  数组名[ 行数 ][ 列数 ]；

（2）数据类型  数组名[ 行数 ][ 列数 ]={ {值1，值2}，{值3，值4}…}；

（3）数据类型  数组名[ 行数 ][ 列数 ]={ 值1，值2，值3，值4…}；

（4）数据类型  数组名[ ][ 列数 ]={ 值1，值2，值3，值4…}；

 

String names[ ]={“张三”，”李四”，“王五”}  定义输入名字数组时的写法。

同时头文件要包含include <string>



```c++
//冒泡排序法
#include <iostream>
using namespace std;
int main()
{
	int arry[9] = { 10,8,47,9,7,4,6,41,99 };
	for (int i = 0; i < 9-1; i++)
	{
		for (int j = 0; j < 9-1 - i; j++)
		{
			if (arry[j] > arry[j+1])
			{
				int temp = arry[j];
				arry[j] = arry[j + 1];
				arry[j + 1] = temp;
			}
		}
		
	}
	cout << "排序后" << endl;
	for (int i = 0; i < 9; i++)
	{
		cout << arry[i] << " ";
	}
	cout << endl;
	system("pause");
	return 0;


}
```

cout<<这里可以放输出值<<后面放endl表示换行。

```c++
cout<<***<"";  //表示不换行输出
//还可以
cout<<"第"<<i+1<<"个人的总分为："<<sum<<endl;//表示连续输出 
```

```cpp
返回值类型 函数名 （参数列表）
{
    函数体语句
    return表达式
}
```



### 函数的定义

```cpp
#定义一个加法，并使用
#include <iostream>
using namespace std;
int add(int a, int b)
{
	int sum = a + b;
	return sum;
}

int main()
{
	int a = 1;
	int b = 3;
	int c=add(a, b);
	cout << c << endl;
	system("pause");

}
```

### 6.5函数的常见样式

1.无参无返 2.有参无返 3.无参有返 4.有参有返

```cpp
void test01(){}//这种就是无参无返，不需要输入也不需要返回值
```

### 6.6函数的声明

函数的声明可以很多次,但是函数的**定义只能有一次**

如果把自己定义的函数写在main函数的后面,那么需要在main函数之前先声明,比如`int max(int a,int b);`要先声明一下

### 6.7函数分文件编写

创建.h的头文件,创建.CPP的源文件,

==在头文件中写声明,在源文件中写定义==

如何在源文件中引入头文件,一般是

==#include  "swap.h"==

,一般都是""表示自己写的头文件.

### 7.指针

作用:通过指针间接访问内存,从零开始记录,采用十六进制,可以利用指针变量保存地址

定义方法:`数据类型 * 变量名`

```cpp
int a=10;
int *p;
p = &a;
//通过解引用的方式来找到指针指向的内存,指针前加*表示解引用,找到指针指向的内存中的数据
*p = 1000;
//重新定义a=1000,可以对它进行读写
```

指针在32位操作系统下占4个字节,在64位系统下占8个字节

**空指针**:指针变量指向内存中编号为0的空间,**一般用于初始化指针变量**,空指针的内存不可以访问.`int *p = NULL;  0-255之间的内存编号是系统占用的不可以访问` `如果定义了一个空指针,不可以*p=100;  会报错`

**野指针**:指针变量指向非法的内存空间,例如`int *p =(int *)0x1100;`这种指针就是不可以的,没有提前申请使用0x1100这块地址,读取范围权限会出问题,所以千万不可以使用野指针.

### const 修饰指针

1. const修饰指针---**常量指针**:`const int *p =&a;`==指针的指向可以修改,但是指针的指向值不可以修改==,即值被限定,但是地址可改.![image-20220403103838124](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220403103838124.png)
2. const修饰常量---**指针常量**:`int * const p = &a;`,特点:==指针的指向不可以改,指向的值可以改==,
3. const既修饰指针也修饰常量:`const int * const p=&a;`,表示都不可以改

### 7.6 数组和指针

```cpp
int arr[]={1,2,3};
int *p =arr;//数组名就是首地址
//如果对这个指针进行解引用得到的值就是数组的第一个值,即arr[0];
cout<<*p<<endl;//得到的就是1
//如果想要获得第二个值,那么只需要让指针向后移动四个字节,这里只需要让p++就可以,不用p+4.
p++;
再输出就是第二个值.
利用指针做遍历的话就是:
int *p2 =arr;
for(int i=0;i<10;i++)
{
    cout<<*p2<<endl;
    p2++;
}
```

对于一个数组的地址指针进行：//如果对这个指针进行解引用得到的值就是数组的第一个值,即arr[0];如果想要获得第二个值就是p++；

### 7.7 指针与函数

指针作为函数的形参的时候会发生什么?==经典中的经典==,值传递和地址传递,swap函数

```cpp
#include <iostream>
using namespace std;

void swap(int* a, int* b)
{
	int temp = *a;
	*a = *b;
	*b = temp;
	cout << *a << *b << endl;
}

int main()
{
	int a = 10;
	int b = 20;
	swap(&a, &b);
	cout << a << b << endl;
	system("pause");

}
```

地址传递

```cpp
#include<iostream>
using namespace std;

void swap(int *a,int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp
}
int main()
{
    a = 1;
    b = 10;
    swap(&a,&b);
    cout<<*a<<*b<<endl;
    system("pause");
}
```



### 7.8指针综合案例

封装一个函数,实现冒泡升序(bubbleSort)排列:传入数组,用int *arr,求长度:`int len =sizeof(arr)/sizeof(arr[0]);`//求一个数组的长度

## 8 结构体

结构体属于用户自定义的数据类型,允许用户储存不同的数据类型

用法:`struct 结构体名{结构体成员列表};`

在应用 时struct可以省略.用点的方式来进行赋值.name,.age

```cpp
#include <iostream>
#include<string>
using namespace std;
//定义结构体学生
struct Student
{
	string name;
	int age;
	int score;
	//实际上就是很多数据类型的集合，把很多数据集合在一起，形成自己的新的数据类型
}s3;

int main()
{
	//通过结构体学生来创建具体学生,方法1
	/*struct*/ Student s1;//这个struct可以省略
	s1.name = "小张";
	s1.age = 18;
	s1.score = 150;
	cout << s1.name << s1.age << endl;
	
	//通过结构体学生来创建具体学生,方法2
	struct Student s2 = { "小高",18,150 };
	//通过结构体学生来创建具体学生,方法3,在创建结构体之后直接在后面定义s3,很少用
	s3.name = "lbw";
	s3.age = 99;
	s3.score = 999;

	system("pause");


}
```

### 8.3结构体数组

`struct 结构体名 数组名[元素个数]={{},{},{},{}}`

```cpp
#include <iostream>
#include<string>
using namespace std;
//定义结构体学生
struct Student
{
	string name;
	int age;
	int score;
	//实际上就是很多数据类型的集合，把很多数据集合在一起，形成自己的新的数据类型
}s3;

int main()
{
	//创建结构体数组
	Student stuArray[3] = { {"小高",18,150},{"lbw",100,666},{"xz",99,66} };
	//重新定义结构体内的值
	stuArray[0].name = "xiaoliuzouqilai";
	//遍历
	for (int i = 0; i < 3; i++)
		{
		cout << "名字： " << stuArray[i].name << endl;
		}
	system("pause");
	return 0;
}
```

定义结构体的时候要加struct，

定义结构体变量的时候可以不加struct。

==创建结构体变量：==

```cpp
stu3.name = "王五";
stu3.age = 18;
stu3.score = 80;
```

==创建结构体数组==：

```cpp
	struct student arr[3]=
	{
		{"张三",18,80 },
		{"李四",19,60 },
		{"王五",20,70 }
	};
```

输出结构体数组中的值：

```cpp
for (int i = 0; i < 3; i++)
	{
	cout << "姓名：" << arr[i].name << " 年龄：" << arr[i].age << " 分数：" << arr[i].score << endl;
	}
```



### 8.4结构体指针

结构体指针数组要通过->才可以访问内部元素。

利用操作符`->`可以通过结构体指针访问结构体属性,指针必须通过箭头才可以访问.

```cpp
student s={"小高",18,100};
student *p=&s;
p->name;//可以直接访问
```

### 8.5嵌套结构体

![image-20220403160737479](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220403160737479.png)

调用结构体内结构体的属性,用两个点,比如`teacher.stu.score=50;`这样的

==使用指针作为传入的优点在于可以大大减小占用的内存空间==,因为一个指针在64位中只占8个字节,但是如果一个结构体中有多个特征,那么它占用的内存就会很大,而且不会复制出新的副本.

const的作用就是限定这个变量不会被修改,为一个常量,常常用在结构体用指针传入时,用const修饰某个特征,不会引起误操作.

```cpp
//const使用场景
void printStudent(const student *stu) //加const防止函数体中的误操作
{
	//stu->age = 100; //操作失败，因为加了const修饰
	cout << "姓名：" << stu->name << " 年龄：" << stu->age << " 分数：" << stu->score << endl;

}
int main() {

	student stu = { "张三",18,100 };

	printStudent(&stu);//传入地址
}
```



如果不想修改主函数中的数据，用值传递，反之用地址传递



==创建结构体最后面要有分号==

###8.8结构体案例1

```cpp
#include <iostream>
#include<string>
#include<ctime>
using namespace std;

//定义结构体学生
struct Student
{
	string sname;
	int age;
	int score;
	//实际上就是很多数据类型的集合，把很多数据集合在一起，形成自己的新的数据类型
};

struct  Teacher 
{
	string tname;
	Student sarr[5];
};

void allocateSpace(Teacher tarr[],int len)
{
	string nameseed = "ABCDE";
	for (int i = 0; i < len; i++)
	{
		tarr[i].tname = "teacher";
		tarr[i].tname += nameseed[i];
		for (int j = 0; j < 5; j++)
		{
			tarr[i].sarr[j].sname = "student";
			tarr[i].sarr[j].sname += nameseed[i];
			int random = rand() % 61 + 41;
			tarr[i].sarr[j].score = random;
			tarr[i].sarr[j].age = 18;
		}
	
	}
}

void printinform(Teacher tarr[], int len)
{
	for (int i = 0; i < len; i++)
	{
		cout  <<"老师姓名：" << tarr[i].tname << endl;
		//再来一个for循环，输出学生姓名
		for (int j = 0; j < 5; j++)
		{
			cout <<"学生姓名：" << tarr[i].sarr[j].sname << "考试成绩" <<tarr[i].sarr[j].score << endl;
		}
	}
}


int main()
{
	srand((unsigned int)time(NULL));
	Teacher tarr[3] ;
	int len = sizeof(tarr) / sizeof(tarr[0]);
	allocateSpace(tarr, len);
	printinform(tarr, len);
	system("pause");
	return  0;
}
```

结构体中的结构体赋值用两个for循环。



### 项目1：通讯录管理系统

需要创建一个项目来做

`system("pause");`//表示按任意键继续

`sys("cls");`执行到这里清屏

判断性别时：`cout<<"性别："<<(abs->personArray[i].m_Sex == 1 ? "男" ："女")<<"\t"`

`case:`代码中如果有一段很长的代码，会报错，要拿{}扩起来

==如何做一个删除联系人的操作==：所谓的删除，其实可以理解为数据的覆盖，把3-2的位置，直接覆盖，然后把人数-1

```cpp
//删除联系人
if(ret != -1)
{
    for (int i = ret;i<abs->m_Size;i++)
    {
        abs->personArray[i] = abs->personArray[i+1];//每一项的后面向前覆盖
    }
    abs->m_Size--;//updata
}
```



# C++核心编程

主要讲解C++的==面向对象==

### 1.内存的分区模型

- 代码区：存放函数体的二进制代码，由操作系统进行管理
- 全局区：存放全局变量和静态变量以及常量
- 栈区：由编译器自动分配释放，存放函数的参数值，局部变量
- 堆区：由程序员分配和释放，如果程序员不释放，那么程序结束的时候由操作系统回收

**内存四个区的意义**：

不同区域存放数据，赋予不同的生命周期，给我们更大的灵活编程。

####1.1程序运行前：

在程序编译后，生成exe可执行程序，为执行之前，分为两个区域

1. 代码区：

   ​	存放CPU执行的机器指令（二进制）

   ​	代码区是共享的，对于频繁的执行程序，只需要一份代码在内存中就可以

   ​	代码区可读，防止程序意外修改其指令，不可改

2. 全局区：内部有全局变量，静态变量，常量

   ​	全局变量和静态变量存放在这里

   ​	全局区还包含了常量区，里面有字符串常量和其他常量（const修饰）

   ​	==该区域的数据在程序后由操作系统释放。==

   在函数体内的变量都称为局部变量，在函数体外的值，都称之为全局变量。两个地方不放在一块内存中。

   ```cpp
   	int a = 10;
   	cout << "变量的地址为：" << (int)&a << endl;
   ```

   静态变量：`static int s_a`,加个static就是静态，也会 放在全局区

   字符串常量："hello world"

   const修饰全局常量：==不包括局部const常量！！==

   ![image-20220407200904029](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220407200904029.png)

### 1.2程序运行后：

**栈区**：由编译器自动分配释放，存放函数的参数值，局部变量等

在编程的时候不要返回局部变量的地址，会被自动释放。

```cpp
#include <iostream>
#include<string>
#include<ctime>
using namespace std;

int* func(int b)
{
	b=400;
    //栈区数据注意事项 --不要返回局部变量的地址
	int a = 10;//局部变量，存放在栈区，栈区的数据在函数执行完自动释放
	return &a;
}

int main()
{
	
	int* p = func();
	cout << *p << endl;
	cout << *p << endl;
	system("pause");
	return  0;

}
```

形参和局部变量放在栈区，不要用局部变量的地址作为返回值。

**堆区**

由程序员分配和释放，如果程序员不释放，那么程序结束的时候由操作系统回收

在CPP中用new来开辟新

内存：`new 数据类型`，常常是`int *p=new int(10)`

```cpp
int* func()
{
	//
	int *p=new int(10);
	return p;
}

int main()
{
	int* p = func();
	cout << *p << endl;
	system("pause");
	return  0;

}
```

new开辟后得到的是一块地址，可以把变量存放到堆区，获得的是堆区存放内容的对应的地址，不是值！！！！

==指针本质也是局部变量，放在栈上，指针保存的数据放在了堆区==

#### 1.3new 操作符

释放堆区数据：delete p；p是地址

==释放数组时：`delete[] arr;`要加个中括号==

new 的基本用法

\1. **new( )** 分配这种类型的一个大小的内存空间,并以括号中的值来初始化这个变量;没加括号则表示随机初始化，加了（）初始化为0

\2. **new[ ]** 分配这种类型的n个大小的内存空间,并用默认构造函数来初始化这些变量;  ，后面加（）表示初始化为0，（5）表示初始化为5

```cpp
int *a = new int[5];
class A {...}   //声明一个类 A
A *obj = new A();  //使用 new 创建对象
delete []a;
delete obj;
```

这里我们注意，new int[5] 仅仅分配了空间， 但是 new A()，不仅仅为对象obj在队上分配了空间， 而且还调用了 A的构造函数，生成了这个对象。
所以 new A() 这样方式的功能如下:

- 在堆上分配空间
- 在分配的空间上调用对象的构造函数
（这也是 new 和 malloc的主要区别，是否调用构造函数）

## 2.引用

#### 2.1 引用的基本使用

作用是给变量起别名，语法：`数据类型 &别名 = 原名`

例如：int a=10； int &b = a； b=20；  那么a也变成了20，相当于地址，用了同一块内存。

#### 2.2引用的注意事项

==引用必须初始化，一开始就要指定是谁的别名，int &b；这种是错误的。==

引用一旦初始化就不可以更改。只能做赋值，如果b=c，c=30，那么a也会变成30.

#### 2.3引用做函数参数

可以用引用来做传递，来简化指针传递

```cpp
//地址传递
void mySwap(int* a,int* b){
    int temp=*a;
    *a = *b;
    *b =temp;
}
//调用时
mySwap（&a，&b）; //传入地址


//引用传递
void mySwap（int &a，int &b）{
    int temp = a；
    a = b；
    b = temp；
}
//调用时
mySwap（a，b）；
//效果和地址传递是一样的
```

####2.4引用做函数返回值

==不要返回局部变量的引用==

```cpp
int& test(){
    int a =10;
    return a;
}
int &ref = test();
//这样第一个值可以，第二个值会报错
```

==函数的调用可以作为左值==

如果函数的返回值是引用，那么可以作为等式的左值。

![image-20220410160618788](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220410160618788.png)

![image-20220410160700521](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220410160700521.png)

#### 2.5 引用的本质

==在cpp内部实现的就是一个指针常量（指向不可改，指向的值可以改）==

相当于 int* const ref = &a；

只是相对于指针常量在码字的时候更方便一点。

#### 2.6 常量引用

```cpp
int main()
{
	//int a = 10;
	//int& ref = 10;//必须引用合理的内存空间，10这块空间随机不合理，不能引用
	//const int& ref = 10;//这样就没问题了，引用合法。引用了一块合理的内存。
}
```

## 3函数的提高/高级

函数的默认参数：`返回值类型 函数名 （参数=默认值）{}`

==如果某个位置已经有了默认参数，那么从这个位置往后，从左到右都必须有默认值==

==如果函数声明有默认参数，那么函数实现就不能有默认参数==，要不然会发生，简单点来说就是声明里面定义了默认参数之后，在函数定义内不能再有默认参数了。

```cpp
int func(int a,int b=20,int c=30)
{
	return a + b + c;
}

int main()
{
	cout << func(10,30) << endl;
	system("pause");
	return 0;
}
```

#### 3.2函数占位参数

C++中函数的形参列表里可以有占位参数，用来做占位，**调用函数时必须填补该位置**。

语法;`返回值类型 函数名 （只填一个数据类型）{}`

```cpp
void func(int a,int)//占一个位置，这里要传一个参数进来,占位参数还可以有默认值：int = 10；
{
	cout << "lbwnb" << endl;
}

int main()
{
	func(10,50);
	system("pause");
	return 0;
}
```

####3.3函数重（chong）载

函数名可以相同来提高复用性。根据参数不同，来调用不同函数。

**函数重载满足条件**

- 同一个作用域（不在main函数下，在全局下定义就可以）
- 函数名称相同
- 函数参数类型不同，或者个数不同或者顺序不同

返回值不同不可以作为函数重载的条件。例如别的条件都一样，一个是void，一个是int是不可以的。

![image-20220410184020343](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220410184020343.png)

#### 3.4 函数重载----注意事项

1、利用引用作为重载条件

2、当函数重载碰到默认参数时会出现二义性，报错，尽量避免。



#### 关于引用的补充：

语法格式：类型名 &外号 = 变量名;

1 引用的实质是对一个[内存](https://so.csdn.net/so/search?q=内存&spm=1001.2101.3001.7020)空间起别名
2 引用的东西与原来的东西就是完全一样的东西。不管是变量对应的值，还是地址，还是地址的偏移量，都是一样的。

```cpp
#include<iostream>                                                                          
using namespace std;

void mySwap03(int& a, int& b){ //使用引用交换
    int temp = a;
    a = b;
    b = temp;
}


int main()
{

    int a = 10;
    int &b = a; //引用必须初始化 且初始化后不能改变

    cout << "a = " << a << endl;
    cout << "b = " << b << endl;

    int c = 20;

    b = c; // //这是赋值操作，不是更改引用 同时把a和b都改为10

    cout << "a = " << a << endl;
    cout << "b = " << b << endl;
    cout << "c = " << c << endl;


    int d = 50;
    int e = 10;

    cout << "d = " << d << "e = " << e << endl;

    mySwap03(d,e);

    cout << "d = " << d << " e = " << e << endl;
}
```



int& ref = a;
自动转换为 int* const ref = &a; 指针常量是指针指向不可改，也说明为什么引用不可更改
ref = 20;
自动帮我们转换为: *ref = 20;



常量引用主要用来修饰形参，防止误操作

在函数形参列表中，可以加const修饰形参，防止形参改变实参

```c
void show(const int &val)//避免传入的值被改                                       
{
//  val = 100; 防止误操作
    cout << val << endl;
}
```

## 引用与指针的区别

1 引用必须初始化 指针不必初始化
2 引用初始化后不能改变 但是指针可以改变所指的对象
3 不存在空值的引用 但是存在空值的指针







# 4. 类和对象

C++面向对象的三大特性为：==封装、继承、多态==

万事万物皆对象，对象上有其属性和行为。

具有相同性质的对象，我们可以抽象称为类，人-人类，车-车类

###4.1封装

#### 4.1.1封装的意义

- 将属性和行为作为一个整体，表现生活中的事物
- 将属性和行为加以权限控制

语法：`class 类名{ 访问权限： 属性/行为}；`

创建圆类实例：

```cpp
#include <iostream>
#include<string>
#include<ctime>
using namespace std;
#define PI 3.14

//设计一个⚪类，求圆的周长
class Circle 
{
	//访问权限	
public://公共权限
	//属性
	int r;
	//行为,获取圆的周长
	double calculateZC() 
	{
		return 2 * PI * r;
	}
};

int main()
{
	//通过圆类，创建具体的圆（对象）
	Circle c1;//对象c1，相当于是一个实例化的过程
	c1.r = 10;
	cout << "zhouchang=" << c1.calculateZC() << endl;
	system("pause");
	return 0;
}
```

可以通过行为来给属性赋值

```cpp
class Student 
{
	//访问权限	
public://公共权限
	//属性
	int ID;
	string m_name;
	//行为,获取圆的周长
	void setName(string name) 
	{
		m_name = name;
	}//通过行为来赋值
};
```

类中的属性和行为，我们统一称为==成员==，属性也称之为==成员属性和成员变量==，行为称为==成员函数或者成员方法==。



**封装的意义2：**

类设计时，可以把属性和行为放在不同权限下，加以控制：

- public 公共权限           成员在类内可以访问，类外也可以访问
- protected 保护权限        成员在类内可以访问，类外不可以访问
- private 私有权限          成员在类内可以访问，类外不可以访问

==protected和private的主要区别是在于继承中。父子关系，子类可以访问protected，私有子类不能访问。==



#### 4.1.2struct和class的区别

==在C++中struct和class的唯一区别就在于***默认的访问权限不同***==

区别：

- struct默认权限为公共public
- class默认权限为私有private
  - ==相当于在class的开头啥呀没有写权限，那么默认是私有权限==

#### 4.1.3成员属性设置为私有

优点：将成员属性私有之后，自己可以控制读和写权限。同时对于写权限，我们可以检测数据的有效性。

但是如果属性设置为私有只能通过类内部才可以访问，所以在类的内部需要利用一些public的方法来调用，完成只读、读写、只写等操作。

实例：

![image-20220411152247546](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220411152247546.png)

![image-20220411152306606](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220411152306606.png)

![image-20220411152314355](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220411152314355.png)

设置年龄是还检验了其有效性，防止过大过小。



**封装案例1：立方体类**

```cpp
#include <iostream>
#include<string>
#include<ctime>
using namespace std;
#define PI 3.14




class Cube 
{
public:
	void SetLWH(int L,int W,int H) 
	{
		m_L = L;
		m_W = W;
		m_H = H;
	}
	void GetLWH() 
	{
		cout << "m_L=" << m_L << "m_W=" << m_W << "m_H=" << m_H;
	}
	int Mianji() 
	{
		int S = 2 * (m_L * m_H + m_L * m_W + m_W * m_H);
		return S;
	}
	//用成员函数判断就卸载这里

	bool isSameClass(Cube &C)
	{
		if (m_L,m_W,m_H == C.GetLWH()//这里我写的优点问题，上面的GetLWH要设成int类型，有返回值才可以
		{
			return true;
		}
		return false;
	}
private:
	int m_L;
	int m_W;
	int m_H;
};


//用全局函数来判断两个立方体是否一样
bool isSame(Cube& C1, Cube& C2)
{
	if (C1.GetLWH() == C2.GetLWH())//这里我写的优点问题，上面的GetLWH要设成int类型，有返回值才可以
	{
		return true;
	}
	return false;
}

int main()
{
	Cube C1;
	C1.SetLWH(10,10,10);
	C1.GetLWH();
	int S=C1.Mianji();
	cout << "面积为：" << S	<<endl;

	Cube C2;
	C2.SetLWH(10, 10, 10);

	bool ret = isSame(C1, C2);
	if (ret)
	{
		cout << "xiangdeng" << endl;
	}
	else 
	{
		cout << "buxiangdeng" << endl;
	}


	//调用时：
	ret = C1.isSameClass(C2);//用已知的来调用未知的，只要一个就可以
	system("pause");
	return 0;
}
```

一般设置一个值为void返回类型。

获取一个值是int返回类型。

**案例2，判断点和圆的关系**

核心内容：在一个类中，类的属性/方法，可以是另外一个类的成员

==如何系统的进行工作：==

1.将类封装到别的文件中，现在头文件中创建.h文件

```cpp
#pragma once
#include <iostream>
using namespace std;//标准命名空间

//把类复制进来
只需要做声明，各种return和各种{}都删掉，补全分号
//例如：
void setX(int X);//把内容都删除，留下声明，补全分号。
```

==只需要留下方法的声明和变量的声明==

2.在源文件中，就是.cpp文件中

```cpp
#include "point.h"
在使用时不需要声明类，也不需要权限声明
void Point::setX(int X)
{
    m_X = x;
}
```

==只需要声明作用域，作用域的声明`类名::方法`==

shift+tab整体缩进

然后在主函数中，就可以只留下创建类和调用方法的函数，==详细见P106==；



## 4.2对象初始化和清理：

C++中每个对象都要有初始设置以及对象销毁前的清理数据设置。

#### 4.2.1构造函数和析构函数

利用构造函数和析构函数来解决初始化和清理的问题。这两个函数**由编译器自动调用**，初始化和清理是编译器强制要求完成的，如果我们不提供，***那么编译器会提供构造和析构函数***，但是系统提供的构造和析构函数是**空实现**的。

- 构造函数：主要作用在于创建对象时为对象的成员属性赋值，构造函数由编译器自动调用，无需手动。
- 析构函数：主要作用在于对象销毁前系统自动调用，执行一些清理工作。

**构造函数语法：** `类名（）{}`

1.不需要返回值，也不用写void

2.函数名称与类名相同

3.构造函数可以有参数，因此可以发生重载

4.自动调用，无需手动，且只会调用一次

**析构函数语法：** `~类名（）{}`

1.不需要返回值，也不用写void

2.函数名称与类名相同，在名称前有~

3.析构函数不可以有参数，因此不可以发生重载

4.自动调用，无需手动，且只会调用一次

```cpp
#include <iostream>
#include<string>
#include<ctime>
using namespace std;


class Person {
public:
	//构造函数初始化
	Person()
	{
		cout << "构造函数的调用" << endl;//如果不写，里面就是空的
	}
	//析构函数清理
	~Person() {
		cout << "析构函数的调用" << endl;
	}
};

void test()
{
	Person p;//会自动调用，由于是在栈上的数据，所以调用完会自动释放，所以会调用析构函数,如果写在main里面就不显示
}
int main()
{
	test();
	system("pause");
	return 0;
}
```

#### 4.2.2构造函数的分类以及调用：

两种分类方式：

​	    按参数：有参构造和无参构造，无参构造也可以被称为默认构造

就是上面那个代码中，Person（）内有没有参数，比如Person（int a），则称为有参

​	    按类型：普通构造和拷贝构造==重点是拷贝构造写法==

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
```

拷贝构造的目的是为了：拷贝一份和自身类一模一样的东西所以需要传入一个固定的自身的引用。 

==注意事项是：传进来必须是一个不变值，同时要以引用的方式传进来。==



三种调用方式：

​	**括号法**：调用默认构造Person p1；Person p（10）//调用有参；  Person p2（p）//调用拷贝构造；

​	注意事项==调用默认构造时不需要加小括号==，如果加了小括号就变成了函数的声明。

​	**显示法**：默认构造Person p1；Person p2 = Person（10）//这个就显示法调用有参构造；Person p3 = Person（p2）；

==如果单纯的Person（10），那么他是一个匿名对象，执行结束，马上消除，只有放在等号右边指定对象了才可以保存。==

​	**隐式转换法**：Person p4 = 10；//相当于Person p4 = Person（10）

​							Person p5 = p5；//拷贝构造

#### 4.2.3拷贝构造函数调用时机

- 使用一个已经创建完毕的对象来初始化一个新对象（相当于复制和克隆）
- 值传递的方式给函数参数传值**理解为复制时都会产生拷贝构造**
- 以值方式返回局部对象
- ![image-20220412155536204](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220412155536204.png)

####4.2.4构造函数的调用规则

只要你创建了一个类，那么C++默认会创建3个函数：析构，构造，拷贝构造

 规则如下：

- 如果用户定义了一个有参构造：那么C++不再提供默认无参构造，但是会提供默认拷贝构造
- 如果用户定义了拷贝构造，那么C++不再提供其他构造函数

![image-20220412160944586](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220412160944586.png)

默认的拷贝构造函数会做一个简单的所有的值拷贝工作。

#### 4.2.5==深拷贝与浅拷贝==

深拷贝是面试常考题

浅拷贝：简单的赋值操作就是浅拷贝

深拷贝：在堆区重新申请空间，进行拷贝操作

在编译器中，如果你默认没有写拷贝构造，那么编译器会做一个默认的浅拷贝。

而我们在堆区申请的new开辟空间，正好需要在析构函数中进行释放

```cpp
if(m_Height != NULL)
{
    delete m_Height;
    m_Height = NULL;
}
```

![image-20220412195058689](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220412195058689.png)

![image-20220412195108588](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220412195108588.png)

浅拷贝带来的问题就是堆区的内存会重复释放，导致系统崩溃。



所以面对上述问题要利用深拷贝来解决：要实现自己的拷贝函数：

```cpp
Person(const Person &p)
{
    cout<<"拷贝构造函数调用"<<endl;
    //深拷贝
    m_Height = new int(*p.m_Height);
    
}
```

![image-20220412200619948](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220412200619948.png)

要构造自己的拷贝函数，利用new开辟堆区内存



![image-20220412200743993](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220412200743993.png)

在析构函数中要释放内存



![image-20220412200810875](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220412200810875.png)



#### 4.2.6初始化列表

作用：给属性初始化，用的是列表语法

语法：`构造函数():属性1(值1)，属性2(值2)，...{}`

原本初始化属性可以在构造函数中

接下来通过初始化列表初始化属性,==要特别注意我们冒号的位置==

```cpp
class Person
{
    //Person(int a,int b,int c)
    //{
      //  m_A = a;
      //  m_B = b;
      //  m_C = c;
    //}
    另外一个方法：
    Person(int a,int b,int c):m_A(a),m_B(b),m_C(c)
    {
        
    }
    int m_A;
    int m_B;
    int m_C;//下面还要让自身的属性去记录一下
    
};

void test()
{
    Person p(10,20,30);
    
}
```

####4.2.7类对象作为类成员

 C++类中的成员可以是另一个类的对象

```cpp
class A{}
class B
{
    A a;
}
```

a称为对象成员。

那么先有B还是先有A？肯定先有A

#### 4.2.8静态成员

静态成员就是在成员变量和成员函数前加上关键字static，称为静态成员

- 静态成员变量   
  - ==所有对象共享一份数据==
  - 在编译阶段分配内存
  - 类内声明，类外初始化
- 静态成员函数
  - ==所有对象共享一个函数==
  - 静态成员函数只能访问静态成员变量

类外访问不到私有的静态成员函数

### 4.3C++对象模型和this指针

#### 4.3.1成员变量和成员函数分开存储

C++中类内成员变量和成员函数分开存储，==只有非静态成员变量才属于类的对象上。==

空对象，Person p； sizeof（p）=1.空对象占用内存空间为1.

会给空对象分配一个字节的空间，目的是为了区分空对象占内存的位置。所以每个空对象必须有一个独一无二的位置。

==如果这个类不是空的：里面有int a； 那么就会取消原本的1个字节，总字节数变成4；==

如果里面是static int b；不属于类的对象上，不占对象内存。

非静态成员函数也不属于类对象上。

静态成员函数也不属于类对象上。

#### 4.3.2this指针：

一个类的成员函数可以被很多个对象调用，可以是p1，p2，p3.如何区分哪个是哪个调用的呢。这里就用了this指针。

**this指针指向被调用的成员函数所属的对象**，谁调用它this指针就指向谁。

==this指针是隐含在每一个非静态成员函数内的一种指针==，不需要定义，直接调用。



this指针的作用：

- 当形参和成员变量同名时，可以用this指针区分
- 在类的非静态成员函数中返回对象本身，可以使用return *this

```cpp
#include <iostream>
#include<string>
#include<ctime>
using namespace std;

class Person
{
public:
	Person(int age)
	{
		//通过this指针，来明确变量
		this->age = age;
	}
	int age;
	Person& PersonAddPerson(Person &p) {//上面的返回值必须是Person&，用引用的形式。如果不加引用，返回是一个值，那么就有问题了。
		this->age += p.age;
		int age;
		return *this;//返回原本的对象
	}
};
//1.解决名称冲突：
void test() {
	//通过对象访问
	Person p1(18);
	cout << "nianlin:" << p1.age << endl;
}
//2.返回对象本身用*this
void test2()
{
	Person p2(10);
	Person p3(22);
	//链式编程
	p2.PersonAddPerson(p3).PersonAddPerson(p3);
	cout << "p2年龄" << p2.age << endl;

}

int main()
{
	test();
	test2();
	system("pause");
	return 0;
}
```

#### 4.3.3空指针访问成员函数

![image-20220413112324015](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220413112324015.png)

#### 4.3.4==const修饰成员函数==

==函数后面==加上const之后变成了**常函数**：`void showPerson() const{}`

- 常函数内不可以修改成员属性。
- 成员属性声明时加关键字==mutable==后，在常含数中任然可以修改。

原因是this指针它的本质是一个指针常量，指向是不可以修改的。如果在成员函数后面再加一个const，相当于把指向值也给定死，那么指向和值都不可以修改。

但是你要是想改const下的，你可以在声明变量时，前面+mutable。

常对象：`const Person p;`

- 声明前加const
- 常对象只能调用常函数

### 4.4友元

在程序内部，有一些私有的属性，也想让类外特殊的一些函数或者一些类进行访问，那么就需要用到友元的技术。

友元的目的就是让一个函数或者类 访问另一个类中的私有成员

友元的关键字：==friend==



友元的三种实现：

- 全局函数做友元
- 类做友元
- 成员函数做友元



####4.4.1全局函数做友元

​	friend void goodGay(Building* building);//让这个全局函数可以访问私有成员

在类中声明全局函数的友元

```cpp
#include <iostream>
#include<string>
#include<ctime>
using namespace std;

class Building {
	friend void goodGay(Building* building);//让这个全局函数可以访问私有成员
public:
	string m_SittingRoom;
	Building() {
		m_SittingRoom = "客厅";
		m_BedRoom = "卧室";

	}
private:
	string m_BedRoom;
};

void goodGay(Building *building)
{
	cout << "好基友正在访问：" << building->m_SittingRoom << endl;

	cout << "好基友正在访问：" << building->m_BedRoom << endl;
}

void test() {
	Building building;
	goodGay(&building);
}

int main()
{
	test();
	system("pause");
	return 0;
}
```

####4.4.2类做友元

同理

==	friend class GoodGay;==

```cpp
#include <iostream>
#include<string>
#include<ctime>
using namespace std;

class Building {
	friend class GoodGay;
public:
	string m_SittingRoom;
	Building() {
		m_SittingRoom = "客厅";
		m_BedRoom = "卧室";

	}
private:
	string m_BedRoom;
};

/*类外写成员函数：
Building::Building() {
	m
}*/

class GoodGay 
{
public:
	GoodGay();
	void visit();
	Building* building;
};

//类外写成员函数：
GoodGay::GoodGay()
{
	//创建建筑物对象
	building = new Building;
}

void GoodGay::visit() {
	cout << "好基友正在访问：" << building->m_SittingRoom << endl;
	cout << "好基友正在访问：" << building->m_BedRoom << endl;
}

void test() {
	GoodGay gg;
	gg.visit();
}

int main()
{
	test();
	system("pause");
	return 0;
}
```

#### 4.4.1成员函数做友元

friend void GoodGay::visit



### 4.5运算符重载

运算符重载概念：对已有的运算符重新定义，赋予另一种功能，以适应不同的数据类型。+-*/

#### 4.5.1加号运算符重载

对不同的数据类型进行加号

![image-20220417205012090](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220417205012090.png)

利用特殊函数名：==operator+==

就可以让两个特殊类型的东西相加了。

运算符重载也可以发生函数重载：Person p3 = p1+10；

直接还是Person operate+ （Person &p1，int num）{

里面写加法的东西就可以。}

同一个函数名，不同参数，就可以重载



**注意事项：**

1.对于内置的数据类型的表达式的运算符是不可能改变的

2.不要滥用运算符重载



#### 4.5.2==左移运算符==

作用：可以输出自定义数据类型  `<<`就是两个小于号

只能利用全局函数才可以重载左移运算符。

==cout属于的类型是ostream，表示输出流对象==

```cpp
#include <iostream>
#include<string>
#include<ctime>
using namespace std;

class Person 
{
public:


	int m_A;
	int m_B;
};

ostream & operator<<(ostream &cout ,Person &p)
{
	cout << "m_A = " << p.m_A << "m_b = " << p.m_B;
	return cout;
}


void test01() 
{
	Person p;
	p.m_A = 10;
	p.m_B=20;
	cout << p<<endl;
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

#### 4.5.3==递增运算符重载==

递增运算符：++

**注意事项：**

- 前置运算符返回的是引用
- 后置运算符返回是值

```cpp
#include <iostream>
#include<string>
#include<ctime>
using namespace std;

class MyInteger 
{
	friend ostream& operator<<(ostream& cout, MyInteger myint);
public:
	MyInteger() 
	{
		m_Num = 10;
	}

	//重载前置++运算符  返回引用为了一直对应该数据进行递增操作
	MyInteger& operator++()
	{
		m_Num++;
		return *this;
	}

	//重载后置递增 这里的占位符可以用来区分前置还是后置递增,后置递增返回值，因为是返回局部变量。
	MyInteger operator++(int)
	{
		MyInteger temp = *this;
		m_Num++;
		return temp;
	}

private:
	int m_Num;
};

//重载<<运算符
ostream& operator<<(ostream& cout, MyInteger myint) 
{
	cout << myint.m_Num;
	return cout;
}

void test() 
{
	MyInteger myint;
	cout << ++myint << endl;
}

int main()
{
	test();
	system("pause");
	return 0;
}
```

#### 4.5.4赋值运算符重载

C++至少会给一个类增加四个函数：

1. 默认构造函数（无参，空）
2. 默认析构函数（无参，空）
3. 默认拷贝构造函数，对属性进行值拷贝
4. 赋值运算符operator=，对属性进行值拷贝

==如果类中有属性指向堆区，做赋值操作时也会出现深浅拷贝的问题==

具体见P125代码。



#### 4.5.5关系运算符重载

作用：可以让两个自定义类型对象进行对比

判断a==b,和a ！= b。两个关系运算符。

```cpp
//重载关系运算符
bool operator==(Person &p)
{
    if(this->m_Name == p.m_Name && this->m_Age == p.m_Age)
    {
        return true;
    }
    return false;
}
```

`! =` 的做法是一样的。

#### 4.5.6函数调用运算符重载（仿函数）

- 函数调用运算符（）也可以重载
- 由于重载后使用的方法非常像调用，所以也称为仿函数
- 仿函数没有固定写法，比较灵活

在STL中用的比较多。

![image-20220418162037405](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220418162037405.png)

![image-20220418162103054](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220418162103054.png)

这里的括号就是重新定义过后的调用运算符。



另一个例子：

![image-20220418162840807](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220418162840807.png)

匿名函数对象：

![image-20220418162913235](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220418162913235.png)



## 4.6 继承

![image-20220419154931902](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220419154931902.png)

拥有上一级的共性，还有自己的特征。

 基本语法：

`class CPP : public BasePage`,           ==class  子类   ：继承方式   父类==

好处：减少重复代码。

```cpp
class BasePage
{
public:
	//比如说把头、左边、右边的,放在这里。
	void head() { cout << "头" << endl; }
};

//像设计一个CPP界面，要继承上面的功能
class CPP : public BasePage
{
public:
	void content()
	{
		cout << "CPPniubi" << endl;
	}
};
```

子类又被称为：**派生类**

父类也被称为：**基类**



#### 4.6.2继承方式

`class  子类   ：继承方式   父类`

三种继承方式：

1. 公共继承 public
2. 保护继承 protected
3. 私有继承 private

![image-20220419161747898](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220419161747898.png)

公共继承，父类中什么属性，子类也什么属性，但是私有成员不能访问。

保护继承：父类的公共和保护，都变成子类的保护，私有成员不可以访问。

私有继承：父类的公共和保护，都变成子类的私有，私有成员不可以访问。



在类外，保护权限不可以访问。



####4.6.3继承中的对象模型

从父类继承过来的成员，哪些属于子类对象中？

sizeof（son）的结果是父类所有的==非静态==成员都被继承，称为了新的属性，然后+自己的成员

私有属性被继承了，但是访问不到

 

可以在VS的：开发人员工具里面，进入这个终端

![image-20220419164654978](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220419164654978.png)

查看类的构图：

1. 先进入相应的路劲
2. 指令：`c1 /d1 reportSingleClassLayout类名  "类所在的文件名称.cpp"`

就可以查看类的模型。



#### 4.6.4继承中构造和析构的顺序

子类继承父类后，当创建子类对象，也会调用父类的构造函数

那么父类和子类的构造和析构顺序是谁先谁后？

```cpp
//公共、复用率很高的代码
class Base
{
public:
	Base() { cout << "Base的构造函数" << endl; }
	~Base()
	{
		cout << "base的析构函数" << endl;
	}
};
class son :public Base
{
public:
	son() { cout << "son的构造函数" << endl; }
	~son()
	{
		cout << "son的析构函数" << endl;
	}
};

void test() 
{
	//Base b;
	son s;
}

int main()
{
	test();
	system("pause");
	return 0;
}
```

![image-20220419170710222](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220419170710222.png)

最后 运行结果。先父类的构造，然后子类构造析构，最后释放父类的析构。



#### 4.6.5继承同名成员处理方式

- 如果想访问子类同名成员： 直接访问即可
- 访问父类同名成员：需要加作用域

`s.Base::m_A`

加个作用域就可以。



#### 4.6.6继承同名静态成员的处理方式

和非静态的处理方法一模一样

静态成员属性的特点：1.编译阶段分配内存 2.所有对象共享同一份数据 3.==类内声明、类外要初始化==

```cpp
class Base
{
public:
	static int m_A;
};
int Base::m_A = 100;
```

![image-20220419173330604](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220419173330604.png)



#### 4.6.7多继承语法

可以允许一个子类继承多个父类

语法：`class 子类 : 继承方式 父类1, 继承方式 父类2{}；`

多继承有可能会引发父类中同名成员出现，需要加作用域区分。

**在实际使用中不推荐使用多继承**



#### 4.6.8菱形继承

两个派生类同时继承一个基类，又有某个类同时继承两个派生类。称为菱形继承。

![image-20220421154028305](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220421154028305.png)

利用虚继承可以解决菱形继承的问题。

```cpp
class sheep :virtual public Animal{};

class Tuo :virtual public Animal {};
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

其实质是虚基础指针，指向同一块需基础表，用的是同一块地址。





## 4.7 多态

多态分为两类：

- 静态多态：函数重载 和 运算符重载属于静态多态，复用函数名
- 动态多态：派生类和虚函数实现运行时多态。

静态多态和动态多态的区别：

- 静态多态的函数地址早绑定 -编译阶段确定函数地址
- 动态多态的函数地址晚绑定 -运行阶段确定函数地址



动态多态的满足条件：

1. 有继承关系

2. 子类要重写父类的虚函数。函数返回值类型  函数名  参数列表  完全相同

   ```cpp
   //父类中有一个virtual void speak（）
   //子类中也有一个void speak（）
   ```



动态多态的使用：

父类的指针或者引用 执行子类对象

`void doSpeak(Animal &animal)//Animal & animal = cat;`

```cpp
#include <iostream>
#include<string>
#include<ctime>
using namespace std;

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

int main()
{
	test();
	system("pause");
	return 0;
}
```



在class Animal中 如果没有加virtual，则占一个字节

如果是：`	virtual void speak()`,则占四个字节，原因是：这里面变成了一个虚拟指针（虚函数指针vfptr）

virtual function  pointer，虚函数（表）指针。

![image-20220422195001871](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220422195001871.png)





##### 多态原理底层剖析

实质是vfptr被子类中的覆盖了。

当弗雷的指针或者引用指向子类对象的时候，就发生了多态。

![image-20221008135807103](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221008135807103.png)



#### 4.7.2多态案例——计算器类

在真实的开发工作中，实施开闭原则：对扩展进行开发、对修改进行关闭。

```cpp
#include <iostream>
#include<string>
#include<ctime>
using namespace std;

//利用多态来实现计算器。
//实现计算器的抽象类
class AbstractCalculator
{
public:

	virtual int getResult()
	{
		return 0;
	}

	int m_Num1;
	int m_Num2;
};

class AddCalculator :public AbstractCalculator
{
public:
	virtual int getResult()
	{
		return m_Num1 + m_Num1;
	}
};

class SubCalculator :public AbstractCalculator
{
public:
	virtual int getResult()
	{
		return m_Num1 - m_Num1;
	}
};

class MulCalculator :public AbstractCalculator
{
public:
	virtual int getResult()
	{
		return m_Num1 * m_Num1;
	}
};

class ChuCalculator :public AbstractCalculator
{
public:
	virtual int getResult()
	{
		return m_Num1 / m_Num1;
	}
};

void test() 
{
	//多态使用
	AbstractCalculator* abc = new ChuCalculator;
	abc->m_Num1 = 10;
	abc->m_Num2 = 10;

	cout << abc->m_Num1 << "/" << abc->m_Num2 << "=" << abc->getResult() << endl;
	//用完后释放
	delete abc;
}

int main()
{
	test();
	system("pause");
	return 0;
}
```

多态的好处：

1.组织结构清晰

2.可读性强

3.对于后前前期的扩展和维护性强

#### 4.7.3 纯虚函数和抽象类

在多态中，通常父类中虚函数的实现都是毫无意义的，主要都是调用子类重写的内容。

所以可以把父类中这个函数改成纯虚函数。

纯虚函数语法：`virtual int(返回值类型) getResult()（函数名） （参数列表） = 0`，

就是把大括号去掉，变成=0；

**当类中有了纯虚函数，那么这个类也可以称为抽象类**

抽象类特点：

- 不允许实例化对象
- 子类必须重写抽象类中的纯虚函数，否则也属于抽象类

#### 4.7.4多态案例二——饮品制作

![image-20220422212606852](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220422212606852.png)

![image-20220422212625743](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220422212625743.png)

![image-20220422212642161](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220422212642161.png)

![image-20220422212747171](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220422212747171.png)



#### 4.7.5虚析构和纯虚析构

多态使用时，如果子类中有属性开辟到堆区，那么父类指针在释放时无法调用到子类的析构代码。

从而带来==内存泄漏的影响==

**解决方法：**将父类中的析构函数改为虚析构或者纯虚析构



虚析构和纯虚析构的共性：

- 可以解决父类指针释放子类对象
- 都需要有具体的函数实现

虚析构和纯虚析构的区别：

- 如果是纯虚析构，该类属于抽象类，无法实例化对象

```cpp
//之前的释放过程是
void test()
{
    Animal *animal = new Cat;
    animal->speak();
    delete animal;
}
```

子类的析构函数没有调用！！！

```cpp
void test()
{
    Animal *animal = new Cat;//父类的指针指向子类的对象
    animal->speak();
    delete animal;
}
```

原因在于：父类的指针指向子类的对象，父类指针在析构时，不会调用子类中的析构函数。导致子类如果有堆区的数据，会导致内存泄漏。

```cpp
//虚析构
virtual ~Animal()
{
    cout<<"nb"<<endl;
}

//纯虚析构
virtual ~Animal = 0;
```

但是纯虚析构需要代码的实现，在类的外面，需要在类外声明，与纯虚函数不同。

```cpp
Animal::~Animal()
{
	cout<<"Animal的纯虚析构"<<endl;
}
```

只要有纯虚析构，这个类就会变成抽象类，无法实例化对象。



### 5 文件操作

程序运行时产生的数据都属于临时数据，程序一旦运行结束都会被释放。

通过**文件可以将数据持久化**



C++在对文件操作需要包含头文件==<fstream>==



文本类型分为两种：

1.**文本文件** -文件以文本的**ASCII码**形式储存在计算机中

2.**二进制文件** -文件以文本的**二进制形式**存储在计算机中。



操作文件的三大类：

1. ofstream：写操作
2. ifstream：读操作
3. fstream：读写操作



#### 5.1文本文件

##### 5.1.1写文件

![image-20220423150100550](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220423150100550.png)

```cpp
#include <fstream>
ofstream ofs;
ofs.open("文件路劲",打开方式);
ofs<<"写入数据";
ofs.close();
```

文件的打开方式：

![image-20220423150432306](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220423150432306.png)

ios::in 表示读文件

ios::out 表示写文件



如果想要配合使用打开方式，可以利用|操作符

`ios::binary|ios::out`

如果没有指定文件路径，那么会自动创建在同级的代码文件目录下。



#### 5.1.2读文件

```cpp
#include <fstream>
ifstream ifs;
ifs.open("文件路劲",打开方式);
//判断是否打开成功：
if (!ifs.is_open())
{
    cout<<"文件打开失败"<<endl;//文件名不存在，或者路径写错了
    return；
}
四种读取方式
ifs.close();
```

四种读取方式

1. 利用ifs>>buf,将文本一行一行读出来。

```cpp
char buf[1024]={0};
while(ifs>>buf)
{
    cout<<buf<<endl;
}
```

2.还是通过while循环

```cpp
char buf[1024]={0};
while(ifs.getline(buf,sizeof(buf)))
{
    cout<<buf<<endl;
}
```

3.利用string字符串：

```cpp
string buf;
while (getline(ifs,buf))
{
    cout<<buf<<endl;
}
```

4. char c

```cpp
char c;
while(c=ifs.get() !=EOF)//每次只读一个字符,EOF  end of file,表示督导文件尾部
{
    cout<<c;
}
```



### 5.2二进制文件

打开方式要指定为：ios::binary

#### 5.2.1写文件

`ostream& write(const char * buffer,int len);`

字符指针buffer指向内存中一段存储空间。len是读写的字节数。

```cpp
#include <iostream>
#include<string>
#include<ctime>
#include<fstream>
using namespace std;

class Person
{
public:
	char m_Name[64];
	int m_Age;
};

void test()
{
	ofstream ofs;
	ofs.open("penson.txt", ios::out|ios::binary);
	Person p = { "小张",22 };
	ofs.write((const char*)&p, sizeof(Person));//必须两个参数，用write
	ofs.close();
}

int main()
{
	test();
	system("pause");
	return 0;
}
```



#### 5.2.2读文件

主要利用流对象调用成员函数read

`istream& read (char *buffer,int len);`

```cpp
#include <iostream>
#include<string>
#include<ctime>
#include<fstream>
using namespace std;

class Person
{
public:
	char m_Name[64];
	int m_Age;
};

void test()
{
	ifstream ifs;
	ifs.open("penson.txt", ios::in|ios::binary);
	if (!ifs.is_open())
	{
		cout << "文件打开失败" << endl;
		return;
	}
	Person p;
	ifs.read((char*)&p, sizeof(Person));//必须两个参数，用write
	cout << "姓名" << p.m_Name << "age" << p.m_Age;
	ifs.close();
}

int main()
{
	test();
	system("pause");
	return 0;
}
```





## 职工管理系统

基于多态，功能如下：

 ![image-20220425204629645](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220425204629645.png)

exit（0）；函数功能是不管哪个程序调用到这个函数就直接退出。





增加职工：

不同的职工返回的指针不同，但是可以用多态统一返回的指针，返回Worker *  数组

![image-20220426152444753](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220426152444753.png)

开辟数组指针要Worker **，二级指针



在完成了上一个工作之后，没有能把之前的文件保存下来，所以要和文件进行交互。



构造函数初始化数据分为三种

1.第一次使用，文件未创建

2.文件存在，但是数据被用户清空

3.文件存在，并且保存职工的所有数据



如何判断一个文件是否为空文件，利用ch字符一个一个读，如果第一个读就读到ifs.eof，表示读到文件尾部，那么就为空文件。

```cpp
char ch;
	ifs >> ch;
	if (ifs.eof())
	{
		cout << "文件为空" << endl;
		this->m_EmpNum = 0;
		this->m_Emp_Array = NULL;
		this->m_FileIsEmpty = true;
		ifs.close();
		return;
	}
```



#### 显示职工的功能

 如何删除数组中某一个特定编号的人？

利用顺序表，向前移动，然后覆盖数据的方法进行删除。

![image-20220427153236339](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220427153236339.png)

按照姓名来查为止，没做P164

按照名字来查，要在外面加一个判断标志：bool flag = false；

如果找到了，让flag = true；

然后if （flag==false），输出查无此人。



==选择排序算法：==

![image-20220427204213252](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220427204213252.png)

一轮一轮找，每一轮找一个最小的。



删除文件操作：`ofstream ofs(FILENAME, ios::trunc);          ofs.close();`

如果存在这个文件就把它删了并且宠幸创建。

![image-20220427210530216](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220427210530216.png)





# C++提高编程

主要针对C++==泛型编程==和==STL==技术

泛型编程主要是利用**模板**的方法进行的。

#### 1模板

模板就是建立通用的模具，大大提高复用性。

特点：

- 不可以直接使用，只是一个框架。
- 模板的通用不是万能的。



#### 1.2函数模板

- C++的主要编程思想：面向对象、泛型编程，而泛型编程主要利用的技术就是模板
- C++提供两种模板机制：**函数模板**和**类模板**

#### 1.2.1函数模板的语法

建立一个通用的函数，其函数返回值和形参类型可以不具体指定，用一个**虚拟的类型**来表示。

**语法：**

```cpp
template<typename T>
函数声明或定义
```

![image-20220503152119015](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220503152119015.png)

相当于返回值类型先不定义，形参的类型也先不定义，都设为T。

template --声明创建模板，后面**要用尖括号**
typename --- 表面其后面的符号是一种数据类型， 可以用class代替。typename和class没有区别。建议一直用==class==

T --- 通用的数据类型，名称可以替换，通常为大写字母（习惯用T，换成任何大写都可以）



模板最简单的例子：

```cpp
template<typename T> //声明一个模板，告诉编译器后面代码中紧跟的T不要报错，T是一个通用数据类型
void mySwap(T& a, T& b)
{
	T temp = a;
	a = b;
	b = temp;	
}

void test()
{
	int a = 12;
	int b = 23;
	//两种方式使用函数模板
	//1.自动类型推导
	//mySwap(a, b);
	//2.显示指定类型
	mySwap<int>(a, b);
	cout << "a = " << a << endl;
	cout << "b = " << b << endl;
}
```

- 函数模板利用关键字template
- 使用函数模板的两种方式：**自动推导类型**和**显示指定类型**

#### 1.2.2函数模板的注意事项

1. 自动推导的时候必须给出一致的数据类型T，才可以使用。
2. 模板必须要确定出T的数据类型才可以使用



#### 1.2.3函数模板案例

利用选择排序的方法来对不同数据类型的数组进行排序，分别用**char数组和int数组**进行测试。



#### 1.2.4 普通函数与函数模板之间的区别

●普通函数调用时可以发生自动类型转换(==隐式类型转换==)
●函数模板调用时，==如果利用自动类型推导，不会发生隐式类型转换==
●如果利用显示指定类型的方式，可以发生隐式类型转换，***但是在VS2022中好像会报错***

总结就是普通函数可以发生自动类型转换。模板函数中自动类型推导不发生，显示指定类型会发生类型转换。



隐式类型转换就是，比如你定义了一个加法函数，两个int类型相加，现在你用这个函数来做10+c，也可以转换，会把c变成ASCII码，a-97。



建议在使用的过程中均使用显示指定类型的方法。



#### 1.2.5普通函数和函数模板的调用规则

调用规则如下: 
1.如果函数模板和普通函数都可以实现，==优先调用普通函数==
2.可以通过**空模板参数列表**来强制调用函数模板。==如何强制调用模板函数==

```cpp
myPrint<>(a,b);//就是里面什么也不写，写个空模板。这样就强制调用模板函数。
```

3.函数模板也可以发生重载
4.如果函数模板可以产生更好的匹配优先调用函数模板：比如你的普通函数是int类型，但是我传入string，那么就是用函数模板。



#### 1.2.6模板的局限性

![image-20220503172921635](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220503172921635.png)

对模板进行具体化 ：

```cpp
template<> bool myCompare(Person &p1,Person &p2)
{
    if(p1.m_Name == p2.m_Name && p1.m_Age == p2.m_Age)
    {
        return true;
    }
    else
    {
        return false;
    }
}
```



学模板的目的不是为了写模板，为了能在STL在能运用系统提供的模板。



### 1.3 类模板

#### 1.3.1 类模板语法

类模板的作用：

- 建立一个通用类，类中的成员数据类型可以不具体制定

```cpp
template<typename T>
类
```

就是在下面把函数改成了类。

```cpp
template<class NameType, class AgeType>
class Person
{
public:
    Person(NameType name,AgeType age)
    {
        this->m_Name = name;
        this->m_Age = age;
    }
    NameType m_Name;
    AgeType m_Age;   
};

//通过类模板来创建对象

Person<string,int> p1("孙悟空",999);
```



####==1.3.2类模板与函数模板的区别==

1.类模板没有自动类型推导的使用方式

```cpp
 //Person p("孙悟空",1000); 错误，无法用自动类型推导
Person<string, int> p1("孙悟空", 999);
只能用显示指定类型
```

2.类模板在模板参数列表中可以有默认参数

```cpp
template<class NameType, class AgeType = int>
在template里面指定某一个的类型，后续则不需要单独指定
    Person<string>p2("xxx"，28);
第二个就可以不指定了
```



#### 1.3.3类模板中成员函数创建时机

与普通类中的成员函数创建时机是有所区别的：

- 普通类中成员函数一开始就可以创建
- 类模板中的成员函数在==调用时才创建==



#### 1.3.4类模板对象做函数参数

- 类模板实例化出的对象，向函数传参的方式



一共有三种方式

1.指定传入的类型--- 直接显示对象的数据类型
2.参数模板化---将对象中的参数变为模板进行传递
3.整个类模板化---将这个对象类型模板化进行传递

```cpp
//1.指定传入类型：

void printPerson01(Person<string, int>&p)//传入的都是地址。
{
    p.showPerson();
}

void test01()
{
    //Person p("孙悟空",1000); 错误，无法用自动类型推导
    Person<string, int> p("孙悟空", 999);
    printPerson01(p);
}
 
//2.参数模板化
template<class T1, class T2>
void printPerson02(Person<T1, T2>& p)
{
    p.showPerson();
    cout << typeid(T1).name() << endl;//2017可以显示类型，但是2022不行
}

void test02()
{
    //Person p("孙悟空",1000); 错误，无法用自动类型推导
    Person<string, int> p("猪八戒", 1000);
    printPerson01(p);
}
```

![image-20220508163803892](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220508163803892.png)



一般常用第一种



#### 1.3.5类模板与继承

当类模板碰到继承时，需要注意以下几点:
●当子类继承的父类是一个类模板时，==子类在声明的时候，要指定出父类中T的类型==
●如果不指定，编译器无法给子类分配内存
●如果想==灵活指定出父类中T的类型，子类也需变为类模板==

![image-20220509112941645](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220509112941645.png)



子类也想灵活继承：

![image-20220509113413074](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220509113413074.png)

T2是父类中的类型指定，T1是继承中的子类指定。

在后续实例化的过程中：`Son2<int,char>S2;`

#### 1.3.6类模板成员函数类外实现

```cpp
//构造函数类外实现
template<class T1, class T2>
Person<T1, T2>::Person(T1 name, T2 age)
{		
	this->m_Name = name;
	this->m_Age = age;
}

//成员函数的类外实现：
template<class T1, class T2>
void Person<T1, T2>::showPerson()
{
	cout << "姓名： " << this->m_Name << "  年龄：" << this->m_Age << endl;
}

```

类模板在成员函数类外实现是，需要加上模板参数列表



#### 1.3.7类模板分文件编写

学习目标:
●掌握类模板成员函数分文件编写产生的问题以及解决方式
问题:
●==类模板中成员函数创建时机是在调用阶段。导致分文件编写时链接不到==
解决:
●解决方式1:直接包含.cpp源文件

​			原本是包含person.h头文件，直接改成person.cpp源文件即可。原因：因为类模板的成员函数一开始编译的时候没有编译到函数，会报错。**但是很少用**。



●解决方式2:将声明和实现写到同一个文件中,并更改后缀名为.hpp, hpp是约定的名称，并不是强制

​			将.h和.cpp中的内容写到一起，将后缀名改为.hpp（约定俗称的，一看就知道是类模板）

#### 1.3.8 类模板与友元

掌握类模板配合友元函数的类内和类外实现
全局函数类内实现-直接在类内声明友元即可
全局函数类外实现-需要提前让编译器知道全局函数的存在

```cpp
//全局函数 类内实现
class Person
{
    friend void printPerson(Person<T1,T2>p)
    {
       	cout<<""<<p.m_Name<<endl; 
    }
private:
    T1 m
}
```

#### 1.3.9类模板案例

 ![image-20220604160857784](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220604160857784.png)

通用数组构造图。

![image-20220604163826798](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220604163826798.png)



P185：

# 2.STL初识

- 为了建立数据结构和算法的一套标准,诞生了STL.
- STL(Standard Template Library,标准模板库)
- 广义上分为:**容器(container),算法(algorithm),迭代器(iterator)**

**容器和算法之间通过迭代器进行无缝连接**,STL几乎所有代码都采用了模板类或模板函数.

 #### 2.3STL六大组件

![image-20220605172523835](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220605172523835.png)

#### 2.4 STL中容器\算法\迭代器

STL容器就是将运用最广泛的一些数据结构实现出来.

类似于:数组,链表,树,栈,队列,集合,映射表等.

容器分为:**序列式容器**和**关联式容器**两种:

​	![image-20220605173307697](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220605173307697.png)

关联式,会给你排序.



算法(Algorithms):质变算法,非质变算法

![image-20220605183203388](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220605183203388.png)

==算法要通过迭代器才可以访问容器中的数据！==

每个容器都有自己专属的迭代器，迭代器狠类似于指针。

![image-20220607103715907](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220607103715907.png)

最强大的是双向迭代器、随机访问迭代器，一般用后两种。



#### 2.5容器算法迭代器初始

##### 2.5.1vector存放内置数据类型

容器：`vector`

算法：`for_each`  遍历操作。

迭代器：`vector<int>::iterator`



第一种方法：

```cpp
#include <iostream>
#include<string>
#include<ctime>
#include<fstream>
#include<vector>
using namespace std;
//vector容器存放内置数据类型
void test()
{	//创建了一个容器数组
	vector<int> v;
	//向容器中插入数据
	v.push_back(10);
	v.push_back(20);
	v.push_back(30);
	v.push_back(40);

	//通过迭代器来访问数据
	vector<int>::iterator itBegin = v.begin();//初始迭代器 指向容器中第一个元素。
	vector<int>::iterator itEnd = v.end();//指向容器中最后一个元素的下一个位置

	while (itBegin != itEnd)
	{
		cout << *itBegin << endl;
		itBegin++;
	}

}

int main(


)
{
	test();
	system("pause");
	return 0;
}
```



第二种方法，比较常用：

![image-20220607113306344](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220607113306344.png)





```cpp
#include<vector>
void test(){
    vector<int> v;
	v.push_back(10);
    for(vector<int>::iterator it = v.begin();it != v.end; it++){
        cout<< *it << endl;
    }
}
int main(){
    test();
	system("pause");
	return 0;
}
```





第三种方法：使用STL标准库的遍历功能。

要引入标准算法头文件：`include<algorithm>`

```cpp
//先创建一个函数
void myprint（int val）
{
    cout<<val<<endl;
}

for_each(v.begin(),v.end,myprint());//三个参数，begin，end，函数
```



##### 2.5.2 Vector存放自定义数据类型

![image-20220607152557113](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220607152557113.png)

```cpp
//遍历（使用for实现）
for(vector<Person>::iterator it = v.begin(); it != v.end();it++)
{
    cout<<"姓名："<<(*it).m_Name<<"年龄："<<(*it).m_Age<<endl;
}
```

存放地址：

![image-20220607160111234](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220607160111234.png)

![image-20220607160239222](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220607160239222.png)

##### 2.5.3Vector 容器嵌套容器

容器中嵌套容器

```cpp
#include <iostream>
#include<string>
#include<ctime>
#include<fstream>
#include<vector>
using namespace std;
//vector容器存放内置数据类型
void test()
{	//创建了一个嵌套容器
	vector<vector<int>>v;
	//创建小容器
	vector<int>v1;
	vector<int>v2;
	vector<int>v3;
	for (int i = 0; i < 3; i++)
	{
		v1.push_back(i+1);
		v2.push_back(i + 2);
		v3.push_back(i + 3);
	}
	//将小容器放入大容器中
	v.push_back(v1);
	v.push_back(v2);
	v.push_back(v3);
	//通过大容器遍历：
	for (vector<vector<int>>::iterator it = v.begin(); it != v.end();it++)
	{
		for (vector<int>::iterator vit = (*it).begin(); vit != (*it).end();vit++)
		{
			cout << *vit << "  ";

		}
		cout << endl;
	}
}

int main()
{
	test();
	system("pause");
	return 0;
}
```

==*it 是什么数据类型只要看尖括号中间是什么数据类型就可以知道==

###P189 String容器

**本质：**

- string是C++风格的字符串，而string本质上还是一个类

**string和char*的区别**

- char*是一个指针（C语音中字符串的风格）
- string是一个是一个类，类内部封装了`char*`，管理整个字符串，是一个`char*`型的容器

![image-20220608101857274](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220608101857274.png)

##### 3.1.2string构造函数

实例

- `string();`                                    //创建一个空的字符串 例如：string str；
- `string(const char* s);`        //使用字符串s初始化

![image-20220608102909442](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220608102909442.png)

- ` string(const string& str);`  //拷贝构造，使用一个string对象初始化另一个string
- `string(int n,char c);`           //使用n个字符c初始化

![image-20220608102955700](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220608102955700.png)

##### 3.1.3string赋值操作

![image-20220608103810758](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220608103810758.png)

方法1：string& operate=（）；一般用等号。

方法2：string& assign（）；

```cpp
1.
    string str1;
	str1 = 'hello world';
2.
    string str2;
	str2 = 'a';
3.
    string str4;
	str4.assign("hello C++");
4.
    string str5;
	str5.assign("hello c++",5);//表示前5个赋值操作

```

#####3.1.4string字符串拼接

1.![image-20220608112546981](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220608112546981.png)

2.![image-20220608112641281](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220608112641281.png)

3.append 追加 

![image-20220608113156783](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220608113156783.png)

4.![image-20220608113308117](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220608113308117.png)

==str3.append(追加字符串名，起始位置，追加长度）；==

##### 3.1.5 string查找和替换

![image-20220608200339813](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220608200339813.png)

```cpp
//查找功能
string str1 = 'abcdef';
int pos = str1.find("de");//返回值是一个下标

```

如果没查到，返回-1 ，查到了返回所在下标值。

rfind和find的区别：rfind是从右往左查找，find是从左往右查找。但是输出结果还是下标。

替换：str.replace（1,3,'1111'）;  //从1开始的三个字符，替换为1111.

![image-20220608203104056](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220608203104056.png)

##### 3.1.6 string字符串比较

字符串的比较方式是按照字符的ASCII码进行比较：==compare==

`=`     返回0（主要是用来比两个字符串是否相等 ）

`>`     返回1

`<`     返回-1（当成前面剪后面为-）

![image-20220608203612673](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220608203612673.png)

#####3.1.7 字符串提取

![image-20220608204248647](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220608204248647.png)

如何改：

str[0] = 'x';可以直接改

##### 3.1.8 string插入和删除

插入通过：`insert`

```cpp
string str = "hello";
str.insert(1,"111");//h111ello
```

删除通过：`erase()`

```cpp
str.erase(1,3);//表示从第一个位置往后删3个
```

##### 3.1.9 string子串

从字符串中获取想要的子串

```cpp
string str = "abcdef";
string subStr = str.substr(1,3);
//bcd
```

![image-20220609110906668](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220609110906668.png)



### 3.2vector 容器

##### 3.2.1 vector基本概念

vector数据结构和数组非常相似，也称为**单端数组**。

vector和普通数组之间的区别：==不同在于数组是静态空间，而vector是动态扩展==（不会限定死又多少个数，可以一直动态扩展）

-  动态扩展：

![image-20220615103033365](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220615103033365.png)

并非在原有的空间后面开辟新空间，而是找一块更大的空间。

v.begin（），v.end（），分别指向第一个和最后一个的后一位。

- vector容器的迭代器是支持随机访问的迭代器，可以叠加好几个.begin（）.begin（）这种

![image-20220615104242963](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220615104242963.png)

![img](https://img-blog.csdnimg.cn/img_convert/26494408bf8516ed012409f0a0127f2b.png)

第二个函数是前闭后开。

```cpp
//容器打印接口：
void printVector(vector<int>&v)
{
    for(vector<int>::iterator it = v.begin(); it != v.end(); it++)
    {
        cout<<*it<<"";
    }
    cout<<endl;
}
```

```cpp
//vector容器构造
void test()
{
    vector<int>v1//默认无参构造
    for(int i = 0;i<10;i++)
    {
        v1.push_back(i);
    }
    printVector(v1);
}

//通过区间方式进行构造

```

![image-20220615110919693](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220615110919693.png)

拷贝构造：

```cpp
vector<int>v4(v3);
```



##### 3.2.3 vector赋值操作

方法1：上面那种

方法2：等号赋值法

```cpp
vector<int>v2;
v2 = v1;
```

方法3：assign

```cpp
vector<int>v3;
v3.assign(v1.begin(),v1.end());//选择区间
```

方法4：assign，几个几的方式

```cpp
vector<int>v4;
v3.assign(10,100);选择10个100
```



##### 3.2.4 vector容量和大小

![image-20220615155911668](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220615155911668.png)

capacity（）的值一定大于size（）

```cpp
if(v1.empty())
{
    cout<<"v1为空"<<endl;
}
else
{
    cout<<"v1 no kong"<<endl;
    cout<<"容量为："<<v1.capacity()<<endl;
}

v1.resize(15);//重新指定的比原来长了，后面用0填充
```

##### 3.2.5 vector的插入和删除

![image-20220615170058205](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220615170058205.png)

尾插：push_back(ele);

尾删：pop_back();

迭代器插入法：v1.insert（v1.begin（），100）；==注意第一个参数要是一个迭代器==

按个数插入：v1.insert（v1.begin（），2，1000）；//在begin的位置插入两个1000

删除：v1.erase（v1.begin（），v1.end（））；

清空：v1.clear（）；

##### 3.2.6 vector数据存取

```cpp
//利用[]的方式来访问数组中的元素
for(int i=0;i<v1.size();i++)
{
    cout<<v1[i]<<" ";//或者使用：cout<<v1.at[i]<<“ ”
}
cout<<endl;

```

获取第一个元素: v1.front()

获取最后一个元素： v1.back（）

##### 3.2.7 vector互换容器

- 实现两个容器内元素进行互换

```cpp
v1.swap(v2)//将自身进行交换
```

巧用swap可以收缩内存空间

![image-20220616163206630](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220616163206630.png)

会出现，容量比大小多很多的情况。 

利用swap，可以将容量和大小匹配起来

![image-20220616164405029](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220616164405029.png)

vector<int>(v)   这个部分的作用是创建一个匿名对象

.swap(v)

##### 3.2.8 vector预留空间

**功能**：减少vector在动态扩展容量时的扩展次数

- `reserve(int len);`//容器预留len个元素长度，预留位置不初始化，元素不可访问

和resize的区别是，resize会开辟空间之   后初始化为0，reserve不会。

==统计开辟内存次数的方法：==

![image-20220617104619148](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220617104619148.png)

利用reserve预留空间：

```cpp
vector<int>v;
v.reserve(100000);
直接预留了这么多空间，不用反复kai'p
```



##3.3deque容器

##### 3.3.1deque容器的基本概念

功能：

- 双端数组（双端队列），可以对头端进行插入删除操作。（两端都可以）

deque和vector的区别：

- vector对于头部的删除插入操作效率低，数据量大（要先挪动后删除）
- deque而言，对于头部的插入和删除快
- vector访问元素时的速度会 比deque快

![image-20220630225302345](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220630225302345.png)

前插：`push_front()`

前删：`pop_front()`

尾插：`push_back()`

尾删：`pop_back()`

原因时deque内部有**中控区**，维护每段缓冲区中的内容，缓冲区中存放真是数据：

![image-20220630230145946](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220630230145946.png)

中控区记录缓冲区的地址，通过中控区访问缓冲区



```cpp
#include<deque>
//遍历接口
void printDeque(const deque<int>&d)//const 限定只读
{
    for(deque<int>::const_iterator it=d.begin();it!=d.end();it++)//只读迭代器
    {cout<<*it<<" ";}
    cout<<endl;
}

void test()
{
    deque<int>d1;
    for(int i=0;i<10;i++)
    {
        d1.push_front(i)
    }    
}
```

![image-20220630231041557](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220630231041557.png)

四种构造形式如上所示。

和vector的构造方式基本一样

#### 3.3.3 deque赋值操作

```cpp
//1.等号赋值
deque<int>d2;
d2=d1;
//2.assign赋值
deque<int>d3;
d3.assign（d1.begin（），d1.end（））;//选择区间
deque<int>d4;
d4.assign(10,100);
```

#### 3.3.4deque大小操作

![image-20220701110321864](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220701110321864.png)

```cpp
if(d1.empty())
{
    cout<<"d1为空"<<endl;
}
d1.size();//表达出大小
d1.resize();
```

#### 3.3.5deque的插入和删除

头插尾插，头删尾删（push_back(),push_front(),pop_front(),pop_back()）//括号内无东西，一次只删一个

指定位置插入：![image-20220701113353245](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220701113353245.png)

```cpp
//按照指定位置插入： 
d1.insert(d1.begin(),1000)//表示在begin处插入一个1000
```

![image-20220701114331050](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220701114331050.png)

删除：

```cpp
d1.erase(d1.begin());

//想删别的位置的数据，用迭代器
deque<int>::iterator it = d1.begin();
it++;
d1.erase(it);

//按区间删除
d1.erase(d1.begin(),d1.end());
//清空：
d1.clear（）
```



#### 3.3.6deque数据存取

```cpp
//通过中括号来访问元素和at一个效果
for(int i = 0;i<d.size();i++)
{
    cout<<d[i]<<"";
}
cout<<endl;
```

d.front（），d.back（）

#### 3.3.7deque排序

```cpp
#include<algorithm>
运用sort()排序算法就可以
sort(d.begin(),b.end());
```

所有算法迭代器必须加上标准算法头文件

`#include<algorithm>`



### 3.4案例-评委打分

#### 3.4.1案例描述

有5名选手，ABCDE，10个评委分别对每一名选手打分，去除最高分，去除评委中最低分，取平均分。

```cpp
#include <iostream>
#include<string>
#include<ctime>
#include<fstream>
#include<vector>
#include<algorithm>
#include<deque>
using namespace std;
class Person 
{
public:
	Person(string name, int score)
	{
		this->m_name = name;
		this->m_score = score;
	}
	string m_name;
	int m_score;
};


void createPerson(vector<Person>&v)
{
	string nameseed = "ABCDE";
	for (int i = 0; i < 5; i++)
	{
		string name = "选手";
		name += nameseed[i];
		int score = 0;
		Person p(name, score);
		//将创建Person推入
		v.push_back(p);
	}
}

void setscore(vector<Person>& v)
{
	for (vector<Person>::iterator it = v.begin(); it != v.end(); it++)
	{
		deque<int>d;
		for (int i = 0; i < 10; i++)
		{
			int score = rand() % 40 + 61;
			d.push_back(score);
		}
		sort(d.begin(), d.end());
		d.pop_back();
		d.pop_front();

		int sum = 0;
		for (deque<int>::iterator dit = d.begin(); dit != d.end(); dit++)
		{
			sum += *dit;
		}
		int agv = sum / d.size();
		it->m_score = agv;
	}
}

void showscore(vector<Person>&v)
{
	for (vector<Person>::iterator it = v.begin(); it != v.end(); it++)
	{
		cout << "姓名： " << (*it).m_name << " 得分： " << (*it).m_score << endl;
	}
}

int main()
{
	//创建5名选手
	vector<Person>v;
	createPerson(v);
	//for (vector<Person>::iterator it = v.begin(); it != v.end(); it++)
	//{
	//	cout << "姓名： " << (*it).m_name << "分数： " << (*it).m_score << endl;
	//}
	//给5名选手打分：
	setscore(v);
	showscore(v);
	system("pause");
	return 0;
}

```



## 3.5stack容器

#### 3.5.1stack基本概念

概念：stack是一种先进后出的数据结构，他只有一个出口                                                                                                                                

![image-20220702105458671](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220702105458671.png)

栈中只有顶端的元素才可以被外界使用，因此栈不允许有遍历行为。上面是栈底，下面是栈顶

栈中进入数据称为--**入栈**`push`

出栈`pop`

### 3.5.2stack常用接口

```cpp
#include<stack>
void test()
{
    stack<int>s;
    s.push(10);
    s.push(20);
    //只要栈不为空，查看栈顶，并且执行出栈操作
    while(!s.empty())
    {
        cout<<"zhanding"<<s.top()<<endl;
        s.pop();
        
    }
}
```



## 3.6queue容器

#### 3.6.1queue基本概念

queue是一种先进先出的数据结构，他有两个出口

![9](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220702120439139.png)

队尾只能进数据（push（）），对头只能出数据（pop（））

队列容器允许一端新增元素，从另一端移除元素

队列中只有队头和队尾才可以被外界使用，因此队列不允许有遍历行为

队列中进数据的称为：入队`push（）`

出队：`pop（）`



#### 3.6.2 queue常用接口

![image-20220706155438515](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220706155438515.png)

queue队列：

```cpp
#include  <queue>
class Person
{
public:
	Person(string name,int age)
    {
        this.m_Name = name;
        this.m_Age = age;
    }
    string m_Name;
    int m_Age;
};
    
void test()
{
    queue<Person>q;
    Person p1("sun",30);
    Person p2("sun2",300);
    Person p3("sun3",3000); 
    q.push(p1);
    q.push(p2);
    q.push(p3);
    
    while(!q.empty())
    {
        cout<<"队头元素"<<q.front().m_Name<<"年龄："<<q.front().m_Age<<endl;
        //队尾就是q.back（）
        //出队
        q.pop();
    }
} 
```



### 3.7 list容器

####list基本概念：

链表：由许多结点组成，结点是独立的，不会连接起来，通过指针域连接，指针域指向下一个结点

![image-20220706164339459](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220706164339459.png)

链式结构。

上面叫数据域，下面叫指针域。

因为删减数据可以直接改变指针域的指向，就可以直接删减

优点：可以对任意位置进行互换，可以快速插入或删除元素。

缺点：对于list容器遍历的速度，没有数组快（原因是因为指针域还要去寻找地址，就很慢），占用空间比数组大。

STL中的链表是一个双向循环链表：

 ![image-20220706195528035](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220706195528035.png)

既有向前指的指针，又有向后指的指针。如果是循环结点的话，第一个结点的指针域前结点指向最后一个结点，最后一个结点的后指针域指向第一个结点。

可以头部插入，头部删除，也可以尾部插入也可以尾部删除。

![image-20220706200924131](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220706200924131.png)



#### 3.7.2 list构造函数

 ```cpp
 //构造方式：
 list<int>L1;
 L1.push_back(10);
 L1.push_back(20);
 
 //区间方式构造
 list<int>L2(L1.begin(),L1.end());
 
 //拷贝构造
 list<int>L3(L2)
     
 //n个elem
 list<int>L4(10,1000);
 ```

#### 3.7.3 list赋值和交换

赋值：`L1=L2;`  `L3.assign(L2.begin(),L2.end())`

交换：`L1.swap(L2)`

####3.7.4 list大小操作

size（）、resize（）、empty（）

注意：L1.resize(10,10000),表示重新设置容器的大小，多出来的值用10000来填充

#### 3.7.5 list插入和删除

![image-20220707185830480](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220707185830480.png)

和别的迭代器相比多了一个L1.remove（elem）；比如说L1.remove（10）；代表删除整个容器中所有的10元素。

```cpp
void printList(const list<int>&L)
{
    for(list<int>::const iterator it = L.begin(); it != L.end();it++)
    {
        cout<<*it<<" ";
    }
    cout<<endl;
}
```

![image-20220707190319086](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220707190319086.png)

表示迭代器在移动，，一开始是在begin位置，然后向后移动以为++之后在第二位+1000

##### 3.7.6 list数据存取

就两个函数：

`front();`        //返回第一个元素

`back()；`      //返回最后一个元素

不能直接利用[]，也不可以使用at来跳跃访问，原因是list本质是链表，不是用连续性空间存储数据，迭代器也不支持随机访问 

如何验证一个迭代器支不支持随机访问：

![image-20220712151920322](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220712151920322.png)

##### 3.7.7 list反转和排序

反转链表：`reverse();`   //vector容器中有一个reserve是用来预留储存空间的

排序：`sort()；`

所有不支持随机访问的迭代器，都不可以用：sort（L1.begin（），L1.end（））；来排序

内部提供成员函数sort可以用：L1.sort（）；//默认是升序

降序：

要提供一个函数在括号内部

![image-20220712155534241](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220712155534241.png)

然后：L1.sort（myCompare）；//就可以实现降序



对于自定义的数据类型必须指定他的排序规则，比如我自己写了一个类，想让他用身高或者年龄来排序

![image-20220712162416734](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220712162416734.png)

同理把这个放到L1.sort（comparePerson），的括号里面

![image-20220712162952320](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220712162952320.png)





### 3.8 set/multiset容器（集合容器）

特点：所有元素在插入时会被自动排序

本质：属于关联式容器，底层结构用的二叉树实现

- set不允许容器中有重复的元素
- multiset允许容器中有重复的元素

==并没有multiset和multimap这两个头文件，再使用的时候直接#include<set>，就可以，再下面创建的时候用`multiset<int>s；`==



##### 3.8.2 set构造和赋值

构造：`set<T> st;`

==注意set容器在插入数据的时候只有st.insert(),没有什么push_back和push_front==

set容器重复的值会归成一个

```cpp
#include <iostream>
#include<string>
#include<set>
using namespace std;

void printSet(set<int>&s)
{
	for (set<int>::iterator it = s.begin(); it != s.end(); it++)
	{
		cout << *it << " ";
	}
	cout << endl;
}

void test()
{
	set<int>s1;
	s1.insert(10);
	s1.insert(40);
	s1.insert(20);
	s1.insert(30);
	s1.insert(30);

	//遍历容器
	//printSet(s1);
	//拷贝构造
	set<int>s2(s1);
	//赋值
	set<int>s3;
	s3 = s2;
}

int main()
{
	test();
	system("pause");
	return 0;
}
```



#####3.8.3 set大小和交换

`size();`//返回容器中元素的数目

`empty();`//判断容器是否为空

`swap(st);`//交换两个集合容器

set容器不允许resize重新指定大小，因为用0填充会重复



##### 3.8.4 set插入和删除

![image-20220724153626928](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220724153626928.png)

每个传入的东西都必须是==迭代器==，重载的版本可以在erase（）中传入一个指定元素，然后把这个元素全删了。

除了可以指定位置删除，还可以传一个参数进去和参数一样的全部删掉。



##### 3.8.5 set查找和统计

对set容器进行查找数据以及统计数据

- `find(key);`   //查找key是否存在，若存在，返回该键元素的迭代器(位置)；若不存在，返回set.end（）；
- `count（key）;`   //

```cpp
//查找
set<int>::iterator pos = s1.find(30);
if(pos != s1.end())
{
    cout<<"找到元素"<<*pos<<endl;
}
else    
{
   cout<<"没找到元素"<<<<endl; 
}
```

##### 3.8.6 set和multiset的区别

set不允许插入重复的元素，multiset可以插入重复元素

原因是insert插入时实质是一个Pairib数据类型，pair其实是返回一个==对组==元素：<iterator,bool>,返回插入的位置和是否重复插入

![image-20220726110120353](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220726110120353.png)

判断插入是否成成功



而multiset返回的是一个迭代器iterator。



##### 3.8.7 pair队组创建

成对出现的（类似python中的字典）：`pair<type,type> p (value1,value2);`

或者：`pair<type,type> p = make_pair(value1,value2);`

![image-20220726114714743](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220726114714743.png)



#####3.8.8 set容器排序

set容器默认排序规则为从小到大，掌握如何改变排序规则

- 主要利用仿函数，可以改变排序规则

 ```cpp
  //如何改变排序规则变成从大到小
 //利用仿函数
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

迭代规则：

![image-20220726120908789](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20220726120908789.png)

##### set存放自定义数据类型

```cpp
set<Person，comparePerson>s;
Person p1("刘",24);
Person p2("关",24);
s.insert(p1);
s.insert(p2);

//无法输出，因为不知道怎么排序

//仿函数
class comparePerson
{
public:
    bool operator()(const Person&p1, const Person&p2)//表示重载小括号
    {
        return p1.m_Age > p2.m_Age;//按年龄降序
    }
};

```

### 3.9map/multimap容器

#### 3.9.1map基本概念

使用率极高，仅次于vector和list。性能高，效率高。

- map中所有元素都是pair
- pair第一个元素为key，起到索引作用，第二个元素为value（实值）
- 所有元素按key排序

本质：

map/multimap属于关联式容器，底层结构是用二叉树容器。

可以通过key快速查找value。



和multimap区别也是不可以有重复的**key值**。value值是可以重复的。

默认构造：`map<T1,T2>mp;`

```cpp
#include<map>
void test(){
    map<int,int> mp;//创建的时候要有两个元素类型。
    m.insert(pair<int,int>(1,10));//创建一个匿名对象，没有对象名，插入到m中
}

//遍历的另外一种方法：
for(auto i:mp)
    cout<<i->first<<endl;//cout<<(*it).first<<endl;
```



#### 3.9.3map大小和交换

size（）；

empty（）；

swap（st）；

####3.9.4 map插入和删除

函数名都和前面一样

插入：大部分用这种：`m.insert(make_pair(2,20));`

==make_pair()==，的关键字；

```cpp
#include<map>
void test()
{
    map<int,int>m;
    m.insert(pair<int,int>(1,10));//同样是匿名对象插入。
    //或
    m.insert(make_pair(2,20));
}
```

map的遍历：

```cpp
for(auto it=m.begin();it!=m.end();it++)
    cout<<it->first<<it->second<<endl;
```

可以用[]，来利用key访问value

比如：**`cout<<mp[4]<<endl;`**就可以输出key为4的value值。

删除

m.erase(key)；

是按照key来删除，或者可以按照迭代器来删除

#### 3.9.5map查找和统计

`find(key)`;//返回迭代器，若不存在返回==map.end（）==

#### 3.9.6 map排序

默认按key从小到大排，如果想改还是用仿函数

```cpp
incluede<iostream>
include<map>
using namespace std;(using std:: cin)

class myCompare{
public:
  	bool operator()(int v1,int v2){
        return v1>v2;
    }  
};

 //然后把仿函数放到容器中去
map<int,int,myCompare>m;


//自定义数据仿函数：
//仿函数
class comparePerson
{
public:
    bool operator()(const Person&p1, const Person&p2)//表示重载小括号
    {
        return p1.m_Age > p2.m_Age;//按年龄降序
    }
};
```



#### map和set区别

set和map特性和区别
set是一种关联式容器，其特性如下：

set以RBTree作为底层容器
所得元素的只有key没有value，value就是key
不允许出现键值重复
所有的元素都会被自动排序
不能通过迭代器来改变set的值，因为set的值就是键
map和set一样是关联式容器，它们的底层容器都是红黑树，区别就在于map的值不作为键，键和值是分开的。它的特性如下：

map以RBTree作为底层容器
所有元素都是键+值存在
不允许键重复
所有元素是通过键进行自动排序的
map的键是不能修改的，但是其键对应的值是可以修改的

#### STL案例2：员工分组

要求：

![image-20221012193039383](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221012193039383.png)

```cpp
#include<iostream>
#include<string>
#include<vector>
#include<map>
#include<ctime>

using namespace std;

class Worker
{
public:
	string m_Name;
	int m_Salary;

private:

};

void createWorker(vector<Worker> &vWorker) {
	string a = "ABCDEFGHIJ";
	for (int i = 0; i < a.size();i++) {
		Worker worker;
		worker.m_Name = "员工";
		worker.m_Name += a[i];
		worker.m_Salary = rand() % 10000 + 10000;
		vWorker.push_back(worker);
	}
}

void setGroup(vector<Worker>&vWorker,multimap<int,Worker>&mWorker) {
	for (vector<Worker> ::iterator it = vWorker.begin(); it != vWorker.end(); it++)
	{
		int ID = rand() % 3 + 1;
		mWorker.insert(pair<int, Worker>(ID, *it));
	}
}

void show(multimap<int, Worker>& mWorker) {
	cout << "策划部门" << endl;
	auto pos = mWorker.find(1); 
	int count = mWorker.count(1);
	int index = 0;
	for (; pos != mWorker.end() && index < count; pos++, index++)//可以这么写的原因是因为map容器会自动排序
		cout << pos->second.m_Name << " 薪水" << pos->second.m_Salary << endl;
}


int main()
{
	srand((unsigned int)time(0));
	vector<Worker>vWorker;
	createWorker(vWorker);
	//测试
	//for (auto s : vWorker) cout << s.m_Name << endl;
	multimap<int, Worker> mWorker;
	setGroup(vWorker, mWorker);
	show(mWorker);
	system("pause");
	return 0;
}
```



#### 补充：左值和右值的内容

引用和指针的主要区别如下：

- 引用不能为空，引用任何时候都要指向一块合法的内存；指针可以为空；
- 引用一旦初始化完成，就不能再指向另一个变量；指针可以；
- 引用必须在创建的时候初始化，指针可以在任何时候初始化；



左值引用是对具名变量的引用，右值引用是对不具名变量（匿名变量）的引用。

形如 `const T&`的常量左值引用是个万金油的引用类型，其可以引用非常量左值，常量左值和右值。而形如`T&`的非常量左值引用只能接受非常量左值对其进行初始化。



```cpp
int &a = 2;       # 非常量左值引用绑定到右值，编译失败
int b = 2;        # 非常量左值变量
const int &c = b; # 常量左值引用绑定到非常量左值，编译通过
const int d = 2;  # 常量左值
const int &e = c; # 常量左值引用绑定到常量左值，编译通过
const int &b =2;  # 常量左值引用绑定到右值，编程通过
```

右值引用通常不能绑定任何左值，如果要绑定左值，需要使用std::move()将左值转换为右值；



```cpp
int a;
int&& r1 = a; //非法，a是左值；
int&& r2 = std::move(a); //合法，通过std::move()将左值转换为右值；
```

下面来看一个例子：



```cpp
void foo(int& a) {
    cout << "lvalue reference " << a << endl;
}

void foo(int&& a ) {
    cout << "rvalue reference " << a << endl;
}

int main() {
    int a = 0;
    foo(a);
    foo(1);
}

输出：
lvalue reference 0
rvalue reference 1
```

上面的demo重载了foo函数，使其既可以接受左值引用，也可以接受右值引用。从结果可以看出，变量是作为左值处理的，而字面常量（临时对象）是作为右值处理的。



###4 STL-函数对象

#### 4.1.1函数对象概念

- 重载**函数调用操作符**的类，其对象常称为**函数对象**
- 函数对象使用重载的（）时，行为类似函数调用，也叫仿函数

本质：

函数对象（仿函数）是一个类，不是一个函数。

特点：

- 在使用时可以像普通函数那样调用，可以有参数，可以有返回值
- 函数对象超出普通函数概念，函数对象可以有自己的状态
  -  可以在类内部再定义变量，从而完成类似于计数等功能
  - ![image-20221013144555659](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221013144555659.png)

- 函数对象可以作为参数传递
  - <img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221013144619409.png" alt="image-20221013144619409" style="zoom:80%;" />

实例：

```cpp
class myAdd{
public:
	int operator()(int v1,int v2)//括号重载
        return v1+v2;
};
//在使用时可以像普通函数那样调用，可以有参数，可以有返回值,不用.（）这种方式，就可以直接和一个函数一样拿来用
void test(){
    myAdd md;
    cout<<md(10,10)<<end;
}
```

#### 4.2谓词

- 返回bool类型的仿函数称为谓词
- 如果operator（）接受一个参数，那么叫做一元谓词，两个参数叫二元谓词

```cpp
#include<iostream>
#include<string>
#include<vector>
#include<map>
#include<ctime>
#include<algorithm>
using namespace std;

class GreaterFive {
public:
	bool operator() (int val)
	{
		return val > 5;
	}
};

void test() {
	vector<int>v;
	for (int i = 0; i < 10; i++) {
		v.push_back(i);
	}
	auto it = find_if(v.begin(), v.end(), GreaterFive());
	cout << *it << endl;
}

int main()
{
	test();
	system("pause");
	return 0;
}
```

##### 4.2.3二元谓词

```cpp
 //如何改变排序规则变成从大到小
//利用仿函数
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

#### 4.3内建函数对象

STL中内建了一些函数对象，包括：

- 算数仿函数
- 关系仿函数
- 逻辑仿函数

这些仿函数产生的对象、用法和一般函数完全相同

使用这些内建函数对象必须包含头文件：`#include<functional>`

使用标准算法必须包含头文件：`#include<algorithm>`



==使用的时候都用模板的形式==



##### 4.3.2算术仿函数

实现四则运算，其中negate是一元运算，其他都是二元运算。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221013151531601.png" alt="image-20221013151531601" style="zoom:80%;" />

```cpp
#include<functional>
void test(){
    negate<int>n;//
    cout<<n(50)<<endl;
    //相当于对50取反操作
    plus<int,int>p;//一般不用输入两个，因为会默认两个类型一样才能相加或后面的其他操作
    cout<<p(50,50)<<endl;  
}
```

##### ==4.3.3关系仿函数==

用模板形式来传入`gerater<int>()`

![image-20221013154024842](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221013154024842.png)

大于用的最多，谁他妈以后还自己写compare啊

用`sort(v.begin(),v.end(),greater<int>());`

```cpp
//大于
class MyCompare
{
public:
    bool operator()(int v1, int v2)//表示重载小括号
    {
        return v1 > v2;
    }
};
set <int,MyCompare>s2;


//对于上述这个Mycompare我们之前都写过
//现在不用写了
sort(v.begin(),v.end(),greater<int>());//这里的仿函数直接用greater<int>()来创建一个匿名对象。
//默认的sort()，相当于第三位放了一个less<int>（）

```

#####4.3.4逻辑仿函数（基本不怎么用）

![image-20221013155020900](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221013155020900.png)



### 5 STL-常用算法

算法主要是由头文件：`<algorithm>`,`<function>`,`<numeric>`,组成

![image-20221013155642277](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221013155642277.png)

#### 5.1常用的遍历算法

- `for_each` //遍历容器算法
- `transform` //搬运容器到另一个容器

##### 5.1.1for_each

函数原型：`for_each(iterator beg,iterator end,_func);`

起始迭代器，终止迭代器，==函数/仿函数，也可以放函数==

==普通函数放函数名，仿函数放对象，要加（）；==

```cpp
//函数
for_each(v.begin(),v.end(),print);
//仿函数
for_each(v.begin(),v.end(),print());//print函数需要自己定义，实质就是把里面内容cout出来，从开始到最后，执行后面那个函数功能。
```



 ##### 5.1.2transfrom

 把一个容器搬运到另一个容器中，搬运过程可以做一些操作。

函数原型：`transform(iterator beg1, iterator endl,iterator beg2, _func);`

原容器起始终止，和新容器的开始，还有函数，func可以对搬运过程中数做一些运算。

唯一注意点：==需要提前resize好新容器的大小==

```cpp
#include<algorithm>
vector<int>v;
for(int i=0;i<10;i++){
    v.push_back(i);
}
vector<int>v2;
v2.resize(v.size())
transform(v.begin(),v.end(),v2.begin(),Transform());
```

#### 5.2 常用查找算法

常用查找算法：

![image-20221014192508563](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221014192508563.png)

##### 5.2.1find （具体查找）

查找元素，找到返回指定元素的迭代器，找不到则返回结束迭代器end（）

`auto iterator = find(v.begin(),v.end(),5);`

对于自定义的数据类型，比如类中人的名字和年龄，要想查找必须重载==，让底层find知道如何对比Person数据类型。

==//如果查找自定义数据类型，一定要重载`==`==

```cpp
class Person{
public:
    Person(string name, int age){
        this->m_Name = name;
        this->m_Age = age;
    }
    
    bool operator==(const Person& p){
        if(this->m_Name == p.m_Name && this->m_Age == p.m_Age){
            return true;
        }
        else{
            return false;
        }
    }
private:
    int m_age;
    string m_Name;
};
```

返回值是**迭代器**

重载的时候的重要点：`bool operator==(const Person& p)`

- 传入要按照const
- 传入的时候要地址传入

##### 5.2.2 find_if （按条件查找）

按条件查找：`find_if(iterator beg,iterator end,_Pred);//Pred表示一个谓词`

![image-20221014200830368](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221014200830368.png![image-20221014200916080](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221014200916080.png)

注意：

- 传入的时候谓词的时候不能少了括号
- 创造谓词重载的时候要引用的方式传入



##### 5.2.3adjacent_find

查找**相邻重复**元素

函数原型：`adjacent_find(iterator beg,iterator end);`

如果找到会返回相邻元素的第一个位置的迭代器



##### 5.2.4 binary_search （二分查找法）

**查找指定元素是否存在**

存在返回ture，不存在返回false；

注意：==在无序序列中不可用==，可以和sort（），配合使用

 如果在无序中使用，默认找不到。

```cpp
bool ret = binary_search(v.begin(),v.end(),9);
if(ret){
    cout <<"zhaodaole "<<endl;
}
```



##### 5.2.5 count

统计元素个数。

`int num = count(v.begin(),v.end(),40);`

返回值是整数



##### 5.2.6 count_if

按条件统计元素

最后面也是给一个谓词。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221014204448068.png" alt="image-20221014204448068" style="zoom:80%;" />

```cpp
class AgeGreater20{
public:
    bool operator()(const Person &p){
        return p.m_Age>20;
    }
};
```



#### 5.3 常用排序算法

![image-20221014205032721](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221014205032721.png)

##### 5.3.1sort

`sort(iterator beg, iterator end,_Pred)`

不填谓词默认从小到大排序。

和greater<int>()常常搭配使用。（要#include<functional>）



##### 5.3.2 random_shuffle（洗牌算法）

功能：指定范围内的元素随机调整次序 

- `random_shuffle(v.begin(),v.end());`

- 也需要加随机种子来每次随机不一样
- `srand((unsigned int)time(0));`  要包含一下`#include<ctime>`

##### 5.3.3merge (合并存新)

注意：两个容器必须是有序的，合并完知乎还是有序的。

![image-20221014212250036](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221014212250036.png)

`merge(v1.begin(),v1.end(),v2.begin(),v2.end(),vTarget.begin());`



==特别注意点，合并后的这个容器在创建前要申明好他的大小，resize（）==，和搬运容器的transfrom一样。



##### 5.3.4 reverse（反转容器元素）

- reverse（v.begin（），v.end（））



#### 5.4 常用的拷贝和替代算法

`copy`    //将容器指定范围的元素拷贝到另外一个容器中

`replace`  //将容器内指定范围的旧元素修改为新元素

`replace_if`  //容器内指定范围满足条件的元素替换为新元素

`swap `    //互换两个容器的元素



##### 5.4.1 copy

 `copy(iterator beg, iterator end, iterator dest);`

**返回值是一个迭代器**

同样也需要先v2.resize（v1.size（））



##### 5.4.2 replace

`replace(iterator beg, iterator end, oldvalue, newvalue);`

```cpp
//将20替换成2000
replace(v.begin(),v.end(),20,2000);
```

##### 5.4.3replace_if

`replace_if(v.begin(),v.end(),_Pred,newvalue);`

```cpp
class Greater30{
public:
    bool operator()(int val){
        return val>=30;
   }
};

replace_if(v.begin(),v.end(),Greater30(),3000);
```

##### 5.4.4 swap

swap(v1,v2);

**长度也可以不相同。**

**但是容器的类型要相同。**



####5.5 常用算数生成算法

算数生成算法属于小型算法，使用时要包含头文件：`#include<numeric>`

主要包含以下两个：

- `accumulate` //计算容器元素累计总和
- `fill` //向容器中添加元素



##### 5.5.1accumulate

作用：计算区间内元素累计总和

```cpp
#include<numeric>
void test(){
    vector<int>v;
    for(int i=0;i<=100;i++){
        v.push_back(i);
    }
    int total = accumulate(v.begin(),v.end(),0);
}
```

主要实现过程：

`int total = accumulate(v.begin(),v.end(),0);`

最后面那一位的作用是起始的累加值设置，0表示一开始累加初值为0，相当于int total=0；



##### 5.2.2fill

`fill(iterator beg,iterator end,value);`

value表示的是填充的值

![image-20221015133045861](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221015133045861.png)



#### 5.6常用的集合算法

这个很好用！！！

都要包含头文件`#include<algorithm>`

主要包含三个：

- `set_intersection`   //求两个容器的交集
- `set_union`                  //求两个容器并集
- `set_difference`        //求两个容器的差集

##### 5.6.1set_intersection

返回的还是一个容器：

```c++
void test(){
    vector<int>v1;
    vector<int>v2;  
    for(int i=0;i<10;i++){
        v1.push_back(i);
        v2.push_back(i+5);
    }
    vector<int>vTarget;
    vTarget.resize(v1.size()>v2.size() ?v2.size():v1.size());//min(v1.size(),v2.size() )
}

auto itEnd = set_intersection(v1.begin(),v1.end(),v2.begin(),v2.end(),vTarget.begin());

for_each(vTarget.begin(),itEnd,myPrint);
 
```

返回的是交集end的这个迭代器，不要用vTarget.end（）这个迭代器，原因是原本这个容器可能容量会太大，最后会输出别的东西。 

==两个容器必须是有序才行==



##### 5.6.2set _union

求两个集合的并集

![image-20221015141454880](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221015141454880.png)

和set_intersection的用法类似

##### 5.6.3set_difference

差集有一个要注意的点就是，谁和谁的差 V1和V2，V2和V1是不同的。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221015142204166.png" alt="image-20221015142204166" style="zoom:80%;" />

![image-20221015142536586](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221015142536586.png)

1. 必须有序容器
2. 返回的是差集容器的最后一个位置的迭代器





### 项目1：演讲比赛管理系统

要求：

![image-20221019192618021](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221019192618021.png)

需求：

![image-20221019192751027](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221019192751027.png)

用.csv文件的好处是可以用excel打开。

随机小数：

```cpp
double score = (rand() %401+600)/10.f;
d.push_back(score);

sort(d.begin(),d.end(),greater<double>());
```

数据写入：

![image-20221019204911468](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221019204911468.png)

csv是以，为 分割的，所以要手动加入逗号。

`ifs.putback(ch);`//读取单个字符放回去









### 项目2：机房预约

![image-20221103141002986](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221103141002986.png)

![image-20221103141019503](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221103141019503.png)

![image-20221103141038026](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221103141038026.png)



看到P301

![image-20221103192638383](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20221103192638383.png)



# 刷题过程中的知识补充

1. return要在一个方法的内部，返回类型要和定义类型相同

2. 可以直接调用swap（a，b）交换两个vector类型元素

3. substr（a，b），复制字符串函数，要求从指定位置开始，并具有指定的长度。如果没有指定长度_Count或_Count+_Off超出了源字符串的长度，则子字符串将延续到源字符串的结尾

4. string可以直接当作栈数据类型，可以直接pop_back(),也可以push_back()。

5. 最大整数：`INT_MAX `,最小整数：`INT_MIN`

6. 面对多个标签指的类型，建议使用map，这里用unorder_map，表示无序map，不会按键值排序。`unordered_map` 就是哈希表（字典）

7. atoi()函数将数字格式的[字符串](https://so.csdn.net/so/search?q=字符串&spm=1001.2101.3001.7020)转换为整数类型。例如，将字符串“12345”转换成数字12345。里面要放一个地址。

   

