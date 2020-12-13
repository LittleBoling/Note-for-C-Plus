# Note-for-C-Plus
## 2020年12月13日学习笔记
### String 用法小结  
对string类的思考源于最近做的leetcode中栈相关的题目，针对844题  
>给定 S 和 T 两个字符串，当它们分别被输入到空白的文本编辑器后，判断二者是否相等，并返回结果。 # 代表退格字符。
>注意：如果对空文本输入退格字符，文本继续为空。

官方解答给出了这样一段代码：
    
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

####1.数组元素访问方式

    //string种的所有元素可通过数组下标的形式访问
    sting s = "test";
    print(s[1]);
    //输出：e
####2.size()和length()
    #include<iostream>
    #include<string>
    using namespace std;
 
    int main(void)
    {
        //这两个方法完全等价
        string s = "dasddasd";
        printf("size()返回的长度为:%lu\nlength()返回的长度为:%lu",s.size(),s.length());
        return 0;
    }
####3. find()函数和rfind()函数 : 这两个函数用于查找字串在母串中的位置，并且返回该位置，当然如果找不到就会返回一个特别的标记string::nops,而find()函数是从字符串开始指针向后进行查找,rfind()函数是从字符串的结束指针开始向前查找，其使用及输出如下：  
    #include<iostream>
    #include<string>
    using namespace std;

    int main(void)
    {
        string s = "hello worldh";
        int index = s.find("h");     // 从串首向后查找
        int index2 = s.find("h",2)   // 固定位置后子串在母串的位置
        int index1 = s.rfind("h");  // 从串尾向前查找
        printf("(find()):字母h在母串中的位置为:%d\n", index); 
        printf("(rfind()):字母h在母串中的位置为:%d", index1);
        return 0;
    }
####4.assign()函数：该函数用于将目标串的值复制到该串上，并且只复制值，其使用及输出如下：  
    #include <iostream>
    #include <string>
    using namespace std;

    int main(void)
    {
        string s = "hello worldh";
        s.clear();
        s.assign("hello world");
        cout<<s<<endl;   
    }
####5.clear()函数，把当前字符串清空，这时候如果调用string::size()函数或string::length()函数将返回0，其使用及输出如下：  
    #include <iostream>
    #include <string>
    using namespace std;

    int main(void)
    {
        string s = "hello worldh";
        s.clear();
        cout<<"clear后的串的长度"<<s.size()<<endl;
    }
####6. resize()函数，该函数可以将字符串变长到指定长度，若小于原本字符串的长度，则会截断原字符串；这个函数的一个重载形式是str.resize(length,'s') 可以用该输入字符's'来对字符串进行扩充至length的长度，该函数的使用及输出如下：  
    #include <iostream>
    #include <string>
    using namespace std;

    int main(void)
    {
        string s = "hello worldh";
        s.resize(5);       // s会变为 hello
        cout<<s<<endl;
        s.resize(10,'C'); // s 会变为 helloCCCCC
        cout<<s<<endl;   
    }
####7.replace(pos,len,dist)函数: 该函数用于将该串从pos位置开始将长度为len的字串替换为dist串,值得注意的是该函数只替换一次，这与市面上的py和java等语言不一样，需要留意，该函数的使用和输出如下：  
    #include <iostream>
    #include <string>
    using namespace std;

    int main(void)
    {
        string s = "hello worldh";
        s.replace(s.find("h"),2,"#"); // 把从第一个h开始的两个字符变为一个字符 #
        cout<<"替换后的字符串为: "<<s<<endl;   
    }
####8.erase(index,length)函数:该函数删除index位置后length长度的子串，其代码及输出如下:  
    #include <iostream>
    #include <string>
    using namespace std;

    int main(void)
    {
        string s = "hello worldh";
        s.erase(s.find("h"),3);
        cout<<"擦除过后的串"<<s<<endl; // 将会输出lo worldh
    }
####9.substr(index,length)函数:该函数从index开始截断到长度为length并返回截断的子串；值得注意的是，该函数不改变母串的值，其使用及输出如下:  
    #include <iostream>
    #include <string>
    using namespace std;

    int main(void)
    {
        s = s.substr(0,5); 
        cout<<"截断并赋值后的字符串为:"<<s<<endl; // 会输出hello
    }
####10.push_back(char c)函数，pop_back()函数，append(string s)函数：push_back(char c)函数往该字符串的尾端加入一个字符;pop_back()函数从该字符串的尾端弹出一个字符;而apend(string s)函数将会在该字符串的末尾添加一个字符串，并且返回添加后字符串的引用。他们的使用及输出如下图所示:  
    #include <iostream>
    #include <string>
    using namespace std;

    int main(void)
    {
        string s = "hello worldh";
        // s.erase(s.find("h"),3);
        s.pop_back(); //弹出串的最后一个元素
        cout<<"弹出串尾元素后的字符串为: "<<s<<endl;
        s.push_back('s'); // 在串的最后添加一个字符
        cout<<"往串尾添加字符后的字符串为: "<<s<<endl;
        s.append("hhh"); // 在串的最后添加一个字符串
        cout<<"往串尾添加字符串后的字符串为: "<<s<<endl;
    }
####11. String 还包含一个迭代器用法
    //string类提供了向前和向后遍历的迭代器iterator，迭代器提供了访问各个字符的语法
    //类似于指针操作，迭代器不检查范围。
    //用string::iterator或string::const_iterator声明迭代器变量
    //const_iterator不允许改变迭代的内容。常用迭代器函数有：
    const_iterator begin()const;
    iterator begin();                //返回string的起始位置
    const_iterator end()const;
    iterator end();                    //返回string的最后一个字符后面的位置
    const_iterator rbegin()const;
    iterator rbegin();                //返回string的最后一个字符的位置
    const_iterator rend()const;
    iterator rend();                    //返回string第一个字符位置的前面
    rbegin和rend用于从后向前的迭代访问，通过设置迭代器string::reverse_iterator,string::const_reverse_iterator实现
