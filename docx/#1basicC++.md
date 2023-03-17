## 初识C++
[TOC]
```cpp
#include <iostream>
using namespace std;
int main()
{
    cout << "Hello,World" << endl;
    return 0;
}
```
1.C++头文件存在无扩展名、有扩展名、c开头三种
2.cin/cout 必须使用iostream头文件
3.初识namespace特性
4.endl是带有重起一行并同时清空缓冲区的功能的控制符
5.\n 也能够起到换行的作用

### C++代码的标记（token）和空白（white space）
1.一行代码中不可分割的元素叫标记
2.空格、制表符、回车统称为空白

### C++源代码风格

- 每条语句占一行
- 每个函数都有一个开始花括号和一个结束花括号，这两个花括号各占一行
- 函数中的语句都相对于花括号进行缩进
- 与函数名称相关的圆括号周围没有空白
## C++语句
### 1.声明语句
![](https://cdn.nlark.com/yuque/0/2023/jpeg/34874768/1672974381423-98f08672-bc7c-4b5c-9e4d-32813b207160.jpeg)
### 2.赋值语句
C++允许连续使用赋值运算符，将同一个值连续赋给多个变量
```cpp
a1 = a2 = a3 = a4 = 5;
```
### 3.cout语句

1. 传递给cout的变量或常量会被自动识别类型，然后以对应的类型输出
2. cout可以通过<<拼接要输出的内容，同时可以将代码行用换行符分割成多行，因为C++允许换行符和空格的相互替换
### 4.cin语句

1. cin将输入流的信息以变量能接受的形式传递给变量

### 5.初识类

1. cin是一个istream类对象，cout是一个ostream对象，在iostream头文件定义
2. 


![](https://cdn.nlark.com/yuque/0/2023/jpeg/34874768/1672975558244-81c1060a-f291-4725-a6cc-5a338f42dc72.jpeg)
## 初识编译指令
### 让程序访问名称空间std的方法

1. 将using namespace std；放在函数定义前，让文件中所有函数都可以访问
2. 将using namespace std；放在特定的函数定义中，让该函数能访问
3. 在特定函数使用using std::cout;让该函数能使用特定元素
4. 完全不使用using编译指令，而是使用std::前缀
