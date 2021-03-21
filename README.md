# Note-for-C-Plus
## 2020年12月13日学习笔记
### String 用法小结 
对string类的思考源于最近做的leetcode中栈相关的题目，针对844题  
>给定 S 和 T 两个字符串，当它们分别被输入到空白的文本编辑器后，判断二者是否相等，并返回结果。 # 代表退格字符。
>注意：如果对空文本输入退格字符，文本继续为空。

官方解答给出了这样一段代码：
```cpp   
class Solution {
public:
    bool backspaceCompare(string S, string T) {
        return build(S) == build(T);
    }

    string build(string str) {
         string ret;
         for (char ch : str) {
             if (ch != '#') {
                ret.push_back(ch);
             } else if (!ret.empty()) {
                ret.pop_back();
             }
         }
         return ret;
    }
};
```
这段代码有两个不懂的地方：  
1.string原来可以和stack类似，有在尾部添加元素的操作   
2.C++的for可以进行类似python的操作

#### 1.数组元素访问方式

```cpp  
//string种的所有元素可通过数组下标的形式访问
sting s = "test";
print(s[1]);
//输出：e  
```

#### 2.size()和length()
```cpp  
string s = "dasddasd";
printf("size()返回的长度为:%lu\nlength()返回的长度为:%lu",s.size(),s.length());
```
#### 3. find()函数和rfind()函数 

这两个函数用于查找字串在母串中的位置，并且返回该位置，当然如果找不到就会返回一个特别的标记string::nops,而find()函数是从字符串开始指针向后进行查找,rfind()函数是从字符串的结束指针开始向前查找，其使用及输出如下：  

```cpp
string s = "hello worldh";
int index = s.find("h");     // 从串首向后查找
int index2 = s.find("h",2)   // 固定位置后子串在母串的位置
int index1 = s.rfind("h");  // 从串尾向前查找
```
#### 4.assign()函数

该函数用于将目标串的值复制到该串上，并且只复制值，其使用及输出如下：  

```cpp
string s = "hello worldh";
s.clear();
s.assign("hello world");
```
#### 5.clear()函数

把当前字符串清空，这时候如果调用string::size()函数或string::length()函数将返回0，其使用及输出如下：  

```cpp
string s = "hello worldh";
s.clear();
cout<<"clear后的串的长度"<<s.size()<<endl;
```
#### 6. resize()函数

该函数可以将字符串变长到指定长度，若小于原本字符串的长度，则会截断原字符串；这个函数的一个重载形式是str.resize(length,'s') 可以用该输入字符's'来对字符串进行扩充至length的长度，该函数的使用及输出如下：  

```cpp
string s = "hello worldh";
s.resize(5);       // s会变为 hello
cout<<s<<endl;
s.resize(10,'C'); // s 会变为 helloCCCCC
cout<<s<<endl;
```
#### 7.replace(pos,len,dist)函数

该函数用于将该串从pos位置开始将长度为len的字串替换为dist串,值得注意的是该函数只替换一次，这与市面上的py和java等语言不一样，需要留意，该函数的使用和输出如下：  

```cpp
string s = "hello worldh";
s.replace(s.find("h"),2,"#"); // 把从第一个h开始的两个字符变为一个字符 #
cout<<"替换后的字符串为: "<<s<<endl;
```
#### 8.erase(index,length)函数

该函数删除index位置后length长度的子串，其代码及输出如下:  

```cpp
string s = "hello worldh";
s.erase(s.find("h"),3);
cout<<"擦除过后的串"<<s<<endl; // 将会输出lo worldh
```
#### 9.substr(index,length)函数

该函数从index开始截断到长度为length并返回截断的子串；值得注意的是，该函数不改变母串的值，其使用及输出如下:  

```cpp
s = s.substr(0,5); 
cout<<"截断并赋值后的字符串为:"<<s<<endl; // 会输出hello
```
#### 10.push_back(char c)函数，pop_back()函数，append(string s)函数：
* push_back(char c)函数往该字符串的尾端加入一个字符;pop_back()函数从该字符串的尾端弹出一个字符;而apend(string s)函数将会在该字符串的末尾添加一个字符串，并且返回添加后字符串的引用。他们的使用及输出如下图所示:  
```cpp
string s = "hello worldh";
s.pop_back(); //弹出串的最后一个元素
cout<<"弹出串尾元素后的字符串为: "<<s<<endl;
s.push_back('s'); // 在串的最后添加一个字符
cout<<"往串尾添加字符后的字符串为: "<<s<<endl;
s.append("hhh"); // 在串的最后添加一个字符串
cout<<"往串尾添加字符串后的字符串为: "<<s<<endl;
```
#### 11. 迭代器

String 还包含一个迭代器用法,迭代器用法只用于访问元素，无法更改元素

```cpp
string类提供了向前和向后遍历的迭代器iterator，迭代器提供了访问各个字符的语法，类似于指针操作，迭代器不检查范围。
用string::iterator或string::const_iterator声明迭代器变量，const_iterator不允许改变迭代的内容。常用迭代器函数有：
const_iterator begin()const;
iterator begin();                //返回string的起始位置
const_iterator end()const;
iterator end();                    //返回string的最后一个字符后面的位置
const_iterator rbegin()const;
iterator rbegin();                //返回string的最后一个字符的位置
const_iterator rend()const;
iterator rend();                    //返回string第一个字符位置的前面
rbegin和rend用于从后向前的迭代访问，通过设置迭代器string::reverse_iterator,string::const_reverse_iterator实现
```
#### 12.  find_last_of()函数和find_first_of()函数：
* 从函数名我们也可以知道find_last_of()函数是找这个子串在母串中最后一次出现的位置并且将该位置返回；而find_first_of()函数是找这个子串在母串中最后一次出现的位置并将该位置返回，其使用及输出如下:  
```cpp
string s = "hello worldh";  
int index = s.find_first_of("h");
int index1 = s.find_last_of("h");
printf("(find_first_of()):字母h在母串中的位置为:%d\n", index);
printf("(find_last_of()):字母h在母串中的位置为:%d", index1);
```
#### 13.back()和front() 

除此之外还有string.back()/string.front()等返回最后一个元素和第一个元素的用法。

## 2020年12月17日学习笔记
### Vector 用法小结 
对Vector类的思考源于最近做的leetcode中栈相关的题目，针对1441题
>给你一个目标数组 target 和一个整数 n。每次迭代，需要从  list = {1,2,3..., n} 中依序读取一个数字。
>
>请使用下述操作来构建目标数组 target ：
>
>Push：从 list 中读取一个新元素， 并将其推入数组中。  
>Pop：删除数组中的最后一个元素。  
>如果目标数组构建完成，就停止读取更多元素。  
>题目数据保证目标数组严格递增，并且只包含 1 到 n 之间的数字。
>
>请返回构建目标数组所用的操作序列。
>
>题目数据保证答案是唯一的。

vector属于序列式容器(sequential containers)这个大类,可访问的形式有：
```cpp
iterator vector.begin(); //返回数组第一个元素的位置
iterator vector.end(); //返回数组最后一个元素的位置
size_type vector.size(); //获取数组大小
size_type vector.capacity(); //获取数组剩余容量
reference vector.front(); //访问数组的第一个元素
reference vector.back(); //访问数组的最后一个元素
vector.push_back(const T& x); //向数组的末尾压入一个新元素
vercot.pop_back(); //弹出最后一个元素
iterator vertor.erase(iterator position); // 清楚位于position位置的元素并返回position
vector.clear(); //清楚所有元素
vector.resize(); //重定义容器大小，小于当前容量时会截断
vector.insert(iterator position, size_type n, const T& x); //在指定位置插入n个x元素
bool vector.empty(); //判断是否为空
vector.emplace_back(); //emplace为C++11中的新增方法
```
## 2021年1月26日 Linux高性能服务器编程
#### 1.SIGTERM信号
SIGTERM信号是一个类似于中断的设置，可由外部触发，但具体机制还不清楚

## 2021年2月5日 
#### 1.Effictive C++ 条款03  
在进行Linux编程和c++特性的学习过程中，都出现了使用char* 指针代替字符串的样式  
```cpp
char greet[] = "Hello";
char* p = greet;

const char* p = greet;
char* const p  = greet;
```
这说明字符串是一段连续的内存，只需要指定头指针的位置就可以确定字符串的位置   
#### 2.linux Network Program    
* writev函数  
* sendfile函数   
#### 3.Data Structure
常见的stl必须有个大体的印象，甚至hashmap的实现也需要有个数，stl必须熟练运用   
* 堆排序：大顶堆和小顶堆使用priority_queue实现, 该标准库函数的使用以vector为基础，队列中的数据为有序数据，排序方式由第三个参数决定，无迭代器。  
* 还可以使用set排序：std::multiset允许有多个相同的元素 http://www.cplusplus.com/reference/set/multiset/?kw=multiset  
#### 4.InterView  
* java为单继承，C++为多继承   
* 虚函数表的概念

## 2021年2月6日
#### 1.Data Struct  
* sort函数存在于algorithm中，是c++的内置排序函数，详见 http://www.cplusplus.com/reference/algorithm/sort/?kw=sort  

## 2021年2月19日
#### 1.InterView add
* constexpr和常量表达式  
```cpp
const int sz = get_size();//正确，但sz直到运行时才能获取具体值，因此它不是个常量表达式
```
* 显式调用this指针的情况：1.类的非静态成员函数返回值为对象本身时; 2.类的链式调用时; 3.类成员变量和函数参数重名时  
* inline内联函数：函数将在被调用处直接展开  
#### 2.Data Structure
* 丑数/质数因数类问题，使用优先队列或k指针法解决

## 2021年2月20日
#### 1.LeetCode  
* 命名指针变量时，必须将其指向对应的原型，若没有，则需要new一个

## 2021年2月23日
#### 1.LeetCode  
* 题53，分治； 动态规划；二分查找
* 字节对齐：https://blog.csdn.net/sweetfather/article/details/78487563
* 位域，可以指定变量包含的字节数，通常用于向设备发送信息 https://www.cnblogs.com/balingybj/p/4681513.html
* c/c++中结构体的区别，c语言中不能直接使用结构体名来命名变量，因此需要使用typedef
* explicit关键字 https://www.cnblogs.com/gklovexixi/p/5622681.html
* enum 限定作用域 https://blog.csdn.net/craftsman1970/article/details/82986803
* 引用和右值引用，右值引用主要用于移动语义和完美转发 https://www.cnblogs.com/sunchaothu/p/11392116.html

## 2021年3月2日
#### 1.C++基础
* 右值引用和移动语义
#### 2.MySQL原理
* 事务与ACID特性：原子性，一致性，持久性，隔离性
* 并发一致性问题：丢失修改，读脏数据，不可重复读，幻影读
* 封锁，乐观悲观锁
    - 封锁粒度：行级锁和表级锁，锁会消耗资源，锁定的数据越少，系统并发程度越高；粒度越小开销越大
    - 封锁类型：1.读写锁，X锁可写可读，其他事务不能加锁；S锁可读，其他事务可以加S锁不能加X锁 2.意向锁：表锁，事务访问该表数据需要先检查意向锁，对任一结点加锁时，必须先对它的上层结点加意向锁。意向锁是放置在资源层次结构的一个级别上的锁，以保护较低级别资源上的共享或排它锁 3.乐观锁：4.悲观锁：
    ![意向锁](https://images2015.cnblogs.com/blog/643807/201606/643807-20160629154333827-125128781.png)
    - 封锁协议：


## 2021年3月6日
#### 1. 数据结构
* DFS的核心是递归，BFS的核心是队列；递归中递归时间严重依赖于递归的顺序
* 二叉树的重建有递归和迭代两种方式， 递归类问题应该考虑的是如何分割问题的粗粒度方式，而不是每一步都验证的细粒度方式。
#### 2. C++基础/interview
* istringstream定义的变量，将对数据以空格进行自动分段 https://www.cnblogs.com/wuchanming/p/3906176.html
   - 由于不明原因，string重载的+操作会耗费大量的时间。
   - C++还定义了用于插入数据ostringstream和读写均可用的stringstream流。
   - istringstream配合getline常用于字符串分割 https://blog.csdn.net/qq_24279775/article/details/107536238
* 智能指针由原来的auto_ptr演变而来，为了更细致的操作，产生了shared_ptr/unique_ptr/weak_ptr三类。
- shared_ptr实现较为简单，基本思想是每次复制对象时，都先将被复制对象的引用计数+1，再赋给当前对象的count，这里需要注意的是，对指针而言，p1 = p2;仅仅是将p1指向p2的对象，但p1原来指向的对象仍然存在，使用delete才是将其删除，这是不同的两个概念。
- unique_ptr不可被复制，但可以通过(C++Primer P418)unique_ptr::reset()和::release()函数进行转移或释放，unique_ptr存在一个特例，即我们可以拷贝或复制一个即将被销毁的unique_ptr,通常表现为函数可以返回一个unique_ptr https://blog.csdn.net/qq_38410730/article/details/105725663
  - unique_ptr的构造函数被声明为explicit，禁止隐式类型转换的行为。可避免将一个普通指针传递给形参为智能指针的函数。假设，如果允许将裸指针传给void foo(std::unique_ptr<T>)函数，则在函数结束后会因形参超出作用域，裸指针将被delete的误操作；
  - unique_ptr的拷贝构造和拷贝赋值均被声明为delete。因此无法实施拷贝和赋值操作，但可以移动构造和移动赋值；
  - 删除器是unique_ptr类型的一部分。默认为std::default_delete，内部是通过调用delete来实现；
  - unique_ptr可以指向数组，并重载了operator []运算符。
- weak_ptr可用于解决智能指针循环引用问题 https://blog.csdn.net/zhwenx3/article/details/82789537

- final和override
- 虚函数、纯虚函数、虚继承(https://www.cnblogs.com/BeyondAnyTime/archive/2012/06/05/2537451.html)和虚基类(http://c.biancheng.net/view/2280.html)，此外还有个虚析构函数的定义
  - 类中一旦声明了虚函数，就会相应的产生一个虚函数表指针；一旦进行了虚继承，同样也会产生一个虚基类表指针
  - 虚函数指针指向虚函数表，表中存放的是虚函数的地址，没有重写的虚函数具有相同的地址；虚函数表指针指向虚函数表，表种存放的是虚基类相对于虚基类表指针的偏移量。
## 2021年3月7日
#### 1.数据结构
* 动态规划/链表
#### 2.Interview
* new/operator new/placement new/概念仍然不清晰
* 如何定义一个只能在堆上（栈上）生成对象的类？
* 程序文件经过预处理器变为.i文件，输入编译器转换为汇编程序.s，进入汇编器生成可重定位目标程序.o，经过链接器生成可执行目标程序.out
* 编译步骤：词法分析，语法分析，语义分析，中间代码生成，优化，目标代码生成
* 函数调用过程：
* 并发多线编程，使用thread构造，线程一经创建即开始执行。
* 线程池

## 2021年3月8日
#### 1.数据结构
* 二叉树的重建/镜像/递归的三种方式/冒泡排序/选择排序/插入排序
  - 冒泡排序的完整版第二个循环是从后面向前的
  - 选择排序是在冒泡排序的基础上不断的交换序号值，每个内层循环最多只有一次交换，因此虽然都是o(n2)但实际上效率要高一些
  - 插入排序就是插扑克牌的方法，从第二个元素开始，不断的和之前的序列比较
  - 以上三种排序方法时间复杂度均为O(n2),但效率是越来越略高的
#### 2.Interview
* 对象复用与设计模式
* 优化程序的几种方法
  - 使用高效的数据结构和算法
  - 减少循环的使用次数和循环内部的操作
  - 减少存储器的引用，尽量使用临时变量存储多次使用的值
  - 结构体成员长的在前短的在后，保证一次性对齐
  - 循环展开
  - 提高并行性
* 类型安全
  - C++的新机制，new返回的指针类型严格于对象匹配，而不是返回void*
  - 提供了-cast的强制转换方式
* ifstream/ofstream: ifstream将数据从硬盘读入内存， ofstream将数据从内存读到硬盘

## 2021年3月10日
#### 1.数据结构
* 双指针
* “>>”运算符
* 使用递归控制矩阵的方向
* 双指针操作链表剑指offer22和24
* 快速幂
* 大数运算

## 2021年3月11日
#### 1.数据结构
* 大数运算

## 2021年3月12日
#### 1.数据结构
* 二叉排序树节点的公共祖先
* 二叉树节点的公共祖先，涉及到顺序递归的调用，同时公共祖先类问题还可以通过比较对两个节点的前序遍历的最后一个相同节点来完成。

#### 2. linux网络编程
* 阻塞和非阻塞的概念:在处理I/O的时候，阻塞和非阻塞都是同步IO，只有使用了特殊的API才是异步的I/O
* 服务器编程框架：I/O处理单元、逻辑单元和网络存储单元
* 事件处理模式：使用同步I/O模型的Reactor模式和使用异步I/O模型的Proactor模式
* 并发模式：半同步/半异步模式和领导者/追随者模式

## 2021年3月15日
#### 1.数据结构
* 二叉树的自上而下遍历
* 数字遍历和字母遍历

#### 2.Interview
* 操作系统的基本特征：并发和并行、共享、虚拟、异步
* 基本功能：进程管理、内存管理、文件管理、设备管理
* 用户态切换到内核态的步骤：涉及ss0和esp0、cs和eip
* 中断分类:外中断、异常、陷入
* 进程和线程：进程是资源分配的基本单位、线程是独立调度的基本单位
* 进程和线程的对比，区别联系等
* 进程调度算法
  - 批处理系统，没有大量的用户操作，仅需要快速执行完毕，因此要保证吞吐量
    - 先来先服务（FCFS），非抢占式调度算法，按照请求顺序进行调度，有利于长进程，不利于短进程
    - 短作业优先，非抢占式调度算法，按估计运行最短的顺序进行调度
    - 最短剩余时间优先， 短作业优先的抢占式版本，按剩余运行时间的顺序进行调度。
  - 交互式系统，交互式系统有大量的用户操作，因此需要快速反应
    - 时间片轮转，按照FCFS的的顺序进行调度，队首的进程执行一个时间片后转到队尾，重复该操作
    - 优先级调度， 为防止低优先级的进程永远得不到调用，可随着时间的推移提高优先级
    - 多级反馈队列，存在多个队列，每个队列的时间片类似于1，2，4，8...，进程在第一个队列没执行完就会被转入下一个队列，只有在上一个队列执行完后，下一个才开始执行
  - 实时系统，要求进程必须在一定的时间内得到响应
* 进程的互斥、同步和通信
* 进程同步：四个原则：空闲则入、忙则等待、有限等待、让权等待
* 进程通信的方式：管道、信号、信号量、FIFO管道、消息队列、共享存储、socket套接字
* fork函数　
* 线程通信
  - 锁机制
    - 互斥锁：防止结构被并发修改
    - 读写锁：允许同时读但不允许同时写
    - 自旋锁：与互斥锁相同，循环检测是否被释放
    - 条件变量：用条件阻塞进程
  - 信号量机制
  - 信号机制
  - 屏障
* 线程调度： 分时调度、FCFS、时间片轮转调度
* 协程： 一个线程可以拥有多个协程，协程不是进程也不是线程，而是一个特殊的函数，这个函数可以在某个地方挂起，并且可以重新在挂起处外继续运行。所以说，协程与进程、线程相比并不是一个维度的概念。

## 2021年3月15日
#### Interview
* Linux的四种锁，相对于线程而言，互斥锁、读写锁(共享-独占锁)、自旋锁、RUC锁
* 虚拟内存 https://www.jianshu.com/p/13e337312651
  - 存在的原因：1.如果直接使用物理内存，可能出现内存碎片化的状态并且32位数只能映射4GB内存，对8GB就无能为力了 2 进程间的安全性问题
  - 每个进程都默认拥有4GB的虚拟内存
  - 虚拟内存管理技术要求时间局部性和空间局部性

#### 数据结构
* 位运算， 异或有个特性，如果一个数组中只有一个数据不是跟其他数据成对的，这个数组的异或和一定是这个数据本身
* 数组中的数组成的字符，sort的compare表达式中，对string还可以写成a+b < b+a的形式,即表示组合后的数字最小的排在前面
* 表现良好的最长时间段可以用单调栈
* 股票买卖的最佳时机是个动态规划问题，动态规划问题一定要注意看题目条件

## 2021年3月15日
#### Interview
* 页面置换算法
  - 最优页面置换算法，将未来很长一段时间不会被访问到的页替换掉，理论性算法，因为未来无法预测，但通常被用来比较其他算法性能
  - 先进先出FIFO算法，选择在内存中驻留时间最长的页面换出，系统维护了一个链表记录该页面在内存中的驻留时间， head驻留时间最长
  - 最近最久未使用算法LRU: 是对最优置换算法的一个近似，它将内存中最长时间未被访问的算法替换掉。但该算法需要记录页面的访问顺序，开销较大，有两种方法
    - 链表：将最近访问的页存到链表的头，最久未使用的放到列表的尾，缺页中断发生时，淘汰链表的尾部。
    - 栈：访问某页时，将该页加入栈顶，检查栈内是否存在相同页面，如果有就把之前的抽出去，这样栈底就是最久未访问页面
  - 时钟页面置换算法：用到了页表中的访问位置，访问位由硬件设置，检测到访问位为0的直接替换掉，访问位为1的将其置0等待下一次访问，全是1就等第二圈。
  - 第二次机会算法： Enhance Clock算法，属于clock算法的改进型，增加了一个读写的访问位，记录了该页面是否被修改过，经常被写入的页由于被置换出去的同时需要修改内存，因此称为“脏页”，
  access bit：dirty bit 为00时置换出去，11时指针经过变为01再经过一次变为00， 有一个1的则指针经过一次将1位置0，通常使用一个环形列表。
  - 最不常用算法：替换访问次数最少的页面， 每个页面对应一个计数器， 可随着时间推移减小计数器值，这样在很久之前经常被访问的页面就会逐渐被替换掉
* 分段：防止覆盖现象发生
* 磁盘调度算法：调度受3个因素影响，旋转时间，寻道时间和实际数据的传输时间
  - 先来先服务：按照磁盘请求的顺序进行调度
  - 最短寻道时间优先
  - 电梯算法：按照一个方向进行磁盘调度，直到该方向上没有请求。
* linux常用命令
* linux文件系统
* 多核cpu如何保持数据的一致性，MESI机制，当多个cpu访问数据并进行缓存后，嗅探机制一旦探测到数据有变化，就会将缓存中的数据无效化。
* 每个进程访问临界资源的那段代码称为临界区
* 进程用来管理资源，它的执行单元被拆分成线程