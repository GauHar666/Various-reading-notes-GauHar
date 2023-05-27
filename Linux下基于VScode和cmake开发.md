# Linux下基于VScode和cmake开发

## 1.Linux基础知识的补充

linux下一些基础文件夹是干嘛的

![image-20230317111006434](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230317111006434.png)

bin：全称binary，含义是二进制文件，里面的文件都是可以被运行的

dev：主要存放外接设备，如盘这种，不能直接被使用需要挂载

etc：存储配置文件

home：家目录

proc：process表示进程，存储的是Linux运行时候的进程。

root：家目录（管理员权限）

sbin：super binary，要有super权限的用户才能执行的

tmp：临时文件

usr：存放用户自己安装的软件

var：存放系统/程序的日志文件的目录



vim的三种模式：命令行模式，输入模式，底线命令模式。



## 3.编译过程

g++的编译过程

VScode本质上也是通过调用gcc来实现C/C++的编译工作的。在实际开发中一般使用gcc指令编译C代码，使用g++指令编译C++代码

编译过程分为下面四步：.i .s .o  最后生成可执行文件

![image-20230317130145500](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230317130145500.png)

```cpp
//一步到位
g++ test.cpp -o test
```

不一步到位：

```cpp
g++ -E test.cpp -o test.i

g++ -S test.i -o test.s

g++ -c test.s -o test.o
    
g++ test.o -o test
```



g++中重要的编译参数

- -g  加上-g之后才可以生成被GDB调试的可调试文件。

 ```cpp
 # -g 选项告诉gcc产生能被GNU调试器GDB使用的调试信息，以调试程序
 
 g++ -g test.cpp -o test
 ```

- -O[n]:主要作用是利用编译器来优化源代码：

![image-20230317132102286](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230317132102286.png)

```cpp
//一般都是-O2来二次优化
g++ test.cpp -O2 -o test
```

- 如果要统计一个程序运行花了多少时间：

```cpp
time ./test
```

- 指定库文件或者指定库文件的路径：`-l  和   -L`

注意：**-l 查找的是在/lib和/usr/lib和/usr/local/lib里的库直接用-l就能连接。而且-l后面直接加库名**

```cpp
#连接一个glog的库
g++ -lglog test.cpp
```

如果库文件没放在上面的三个目录里面的话，就需要使用 -L参数来指定库文件所在的目录

```cpp
#比如链接mytest库，这个库在/home/bing/mytestlibfolder目录下
g++ -L/home/bing/mytestlibfolde -lmytest test.cpp
```

- -I  指定头文件搜索目录:**针对头文件不再/usr/include 里面的头文件要自己指定**（爱）

```cpp
g++ -I/myinclude test.cpp
```

- -Wall  打印警告信息

```cpp
g++ -Wall test.cpp
```

- -w 关闭警告信息

```cpp
g++ -w test.cpp
```

- **-std=c++11** 设置编译标准

```cpp
g++ -std=c++11 test.cpp
```

- -o 指定输出文件名

```cpp
g++ test.cpp -o test
```

- -D 定义宏

常见的就是-DDEBUG

![image-20230317134124620](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230317134124620.png)

```cpp
在编译的时候想定义一个宏就使用 gcc -DDEBUG main.cpp
```



生成静态库：

一定要先生成.o的二进制文件才可以生成静态库。**原理是归档，把.o文件归档到静态库。**

```cpp
g++ swap.cpp -c -I../include //生成汇编的 swap.o文件
ar rcs libswap.a swap.o  //利用.o文件生成静态库 swap.a
    
g++ main.cpp -lswap -Lsrc -Iinclude -o static_main
```

生成动态库：

```cpp
g++ swap.cpp -I/include -fpic -shared -o libswap.so
    
#链接动态库
g++ main.cpp -Iinclude -Lsrc -lswap -o sharedmain
```



如果想运行动态库生成的可执行文件要怎么做？

```cpp
# 运行可执行文件
./staticmain
//这样的话会报错，因为动态库没有直接添加到可执行文件中
```

需要这样运行：

```cpp
LD_LIBRARY_PATH=src ./sharemain  //指定动态库的位置再去运行就可以。
```



## 4.GBD的调试

GDB全名：GNU Debugger，是一个用来调试C/C++程序的功能强大的调试器 

VSCode也是内嵌了GDB调试器来实现C/C++的调试工作的。

GDB的主要功能：

- **设置断点（表达式断点）**
- 单步执行程序，便于调试
- 使程序在指定的代码行上暂停执行，便于观察
- 查看程序中变量值的变化
- 动态改变程序的执行环境
- 分析崩溃程序的**core文件**



想用gdb做文件调试的话：`gdb [exefilename]` 就可以进入gdb调试程序，exefilename为要调试的可执行文件名。

![image-20230317142043051](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230317142043051.png)

- 单步执行：start
- 直接运行：run
- **单步调试：next（逐过程，函数会直接直接，不会一步一步跳到函数里面）**
- **单步调试：step（逐语句，会跳入自定义函数的内部进行执行）**

- info：查看函数内部局部变量的数值
- finish：结束当前函数，返回到函数调用点

![image-20230317142830086](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230317142830086.png)

display和info的区别在于：display会在整个过程中一直打印你追踪的那个变量的值，而info只会打印一次。

print 变量名，也可以查看目前变量的值

继续调试continue

在vim中：`set nu`可以设置显式行号



没有加上-g生成的可执行文件比加了-g生成的可执行文件要小很多很多。原因在于-g生成的可以用gdb调试，里面可以包含很多别的调试信息。



## 5.IDE -VSCode

如何从终端打开vscode：

直接打开你要打开的文件夹，然后执行：

```cpp
code .
```

![image-20230317162704373](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230317162704373.png)

CRLF: \r\n

LF: \n



Linux下C++开发需要的重要插件：

- C/C++
- CMake
- CMake Tools



**CMake工具的概述：**

CMake是一个**跨平台**的编译(Build)工具,可以用简单的语句来描述所有平台的编译过程。

CMake能够输出各种各样的makefile或者project文件，能测试编译器所支持的C++特性,类似UNIX下的automake。

原作者只需要生成一份**CMakeLists.txt文档**，框架的使用者们只需要在下载源码的同时下载作者提供的CMakeLists.txt，就可以利用CMake，在”原作者的帮助下“进行**工程的搭建**。

makefile文件定义了一系列的规则来指定，那些文件需要先编译，哪些文件需要后编译，哪些文件需要重新编译，甚至进行更复杂的功能操作。

makefile就好像一个shell脚本一样，可以执行操作系统的命令，好处就是自动化编译，一旦写好，只需要一个make命令，整个工程就完全自动编译，极大提高了软件开发的效率。

Cmake是用来makefile的一个工具，读入所有源文件后自动生成makefile

![image-20230318135409937](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230318135409937.png)







VScode常用快捷键

![image-20230318135828838](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230318135828838.png)

![image-20230318140726618](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230318140726618.png)



`ctrl+[` 和`ctrl+]`进行左右缩进，`ctrl+H`替换单词

格式化文档可以把格式调整好



单击是斜体，斜体表示可能等等打开新文件就被覆盖掉了，而非斜体不会被覆盖。双击打开就是非斜体。



## 6.CMake

是一个跨平台的安装编译工具，可以用简单的语句来描述所有平台的安装。

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230318145501838.png" alt="image-20230318145501838" style="zoom:80%;" />

![image-20230318145545132](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230318145545132.png)



CMake基础语法：

语法格式：**指令（参数1 参数2 ....）**

- 参数使用括弧括起来
- 参数之间使用空格或者分号分开

指令是大小写无关的，参数和变量是大小写相关的。

```cpp
set(HELLO hello.cpp)
add_executable(hello main.cpp hello.cpp)
ADD_EXECUTABLE(hello main.cpp ${HELLO})
```

**变量使用${}方式取值，但是在IF控制语句中是直接使用变量名 `IF(HELLO)`**



CMake的重要指令：

- **cmake_minimum_required**: 指定Cmake的最小版本要求

```cpp
cmake_minimum_required(VERSION 2.8.3)
```

- **project** :定义工程名称，并可指定工程支持的语言

语法：`project（prpjectname [CXX][C][Java]）`

```cpp
#指定工程名为HELLOWORLD
project(HELLOWORLD)
```

- set - 显式的定义变量

```cpp
#定义SRC变量，其值为main.cpp hello.cpp
set(SRC main.cpp hello.cpp)
```

- ![image-20230318152337871](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230318152337871.png)

- ![image-20230318152401094](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230318152401094.png)

- 生成库文件：**add_library** -生成库文件

![image-20230318152753200](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230318152753200.png)

- 添加编译参数：add_compile_options()

![image-20230318152905560](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230318152905560.png)

- 生成可执行文件：add_executable ()

![image-20230318153003030](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230318153003030.png)

- 为target添加需要链接的共享库 -----》相同于g++中的 -l参数

![image-20230318153207048](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230318153207048.png)

- ![image-20230318153321780](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230318153321780.png)

- 临时构建源文件列表的命令：aux_source_directory 

![image-20230318153413666](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230318153413666.png)

相当于说SRC里面包含了当前目录中所有的.c和.cpp文件。





![image-20230318153547401](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230318153547401.png)

![image-20230318153630848](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230318153630848.png)



cmake的目录结构：项目主目录存在一个CMakeLists.txt文件

**两种方式设置编译规则：**

1. 包含源文件的子文件加**包含**CMakeLists.txt文件，主目录的CMakeLists.txt通过add_subdirectory添加子目录即可
2. 包含源文件的子文件夹**未包含**CMakeLists.txt文件，子目录编译规则体现在主目录的CMakeLists.txt中。



**Linux平台下使用CMake构建C/C++工程的流程：**

- 手动编写CMakeLists.txt
- 执行命令cmake PATH生成Makefile（PATH是顶层CMakeLists.txt所在的目录）
- 执行命令make进行编译



推荐使用的构建 CMake的方法：外部构建

将编译输出文件与源文件放到不同目录中

```cmake
#1.在当前目录下，创建build文件夹
mkdir build 
    
cd build
#编译上级目录的CMakeLists.txt，生成Makefile和其他文件
cmake ..
#执行make命令，生成target
make
```



## 7.使用VSCode进行完整项目开发

示例一个CMakeLists.txt文件

```cmake
cmake_minimum_required(VERSION 3.0)

project(SWAP)
    
#如果想加一些其他的选项：
set(CMAKE_CXX_FLAGS "${CAMKE_CXX_FLAGS} -g -O2 -Wall") #追加选项，不覆盖。


include_directories(include)

add_executable(main_cmake main.cpp src/swap.cpp)
```



![image-20230319133229229](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230319133229229.png)



**调试json文件**

![image-20230319141013196](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230319141013196.png)

program：可执行文件的路径

一般这样调试：`${workspaceFolder}`表示的是当前的工作路径。

```cpp
"program": "${workspaceFolder}/build/my_cmake_exe"
```

![image-20230319141347769](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230319141347769.png)

打个断点，按F5就可以进入调试模式

配置task.json

![image-20230319142005217](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230319142005217.png)
