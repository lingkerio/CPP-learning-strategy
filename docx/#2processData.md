# 数据处理
[TOC]
##  变量命名规范
- 名称中只能包含字母字符，数字，和下划线
- 名称的第一个字符不能是数字
- C++对大小写敏感
- 以两个下划线打头或以下划线和大写字母打头的名称被保留给实现（编译器及其使用的资源）使用。以一个下划线开头的名称被保留给实现，用作全局标识符
- C++对于名称的长度没有限制，名称中的所有字符都有意义，但有些平台有长度限制
## 控制cout输出进制的控制符
都位于名称空间std
dec：十进制（cout的默认输出进制）
hex：十六进制
oct：八进制
## 储存数字的方式
### 给数字增加后缀
l/L：表示long
u/U：表示unsigned int
ul/UL:表示unsigned long
ll/LL：表示long long
ull/Ull/uLL/ULL：表示unsigned long long
### 根据数字长度
#### 十进制数
采用int、long、long long中能储存需要储存的数字的最小类型
#### 十六进制数/八进制数
采用int、unsigned int、long、unsigned long、long long、unsigned long long中能储存需要储存的数字的最小类型
## 转义序列
![2023_01_12 00_35 Office Lens.jpg](https://cdn.nlark.com/yuque/0/2023/jpeg/34874768/1673455162920-42d3c17d-79f1-4c99-b1f3-25ae22868678.jpeg#averageHue=%23cccbca&clientId=u9edcd66e-34ed-4&from=ui&height=12296&id=ud57e3704&name=2023_01_12%2000_35%20Office%20Lens.jpg&originHeight=3564&originWidth=1033&originalType=binary&ratio=1&rotation=90&showTitle=false&size=261174&status=done&style=none&taskId=u4655ebd5-7ef0-47ed-ba6c-e5b006c2194&title=&width=3564)
## 通用字符名（universal character name）
以\u或\U开头表示ISO 10646字符集的字符
\u开头后接八个十六进制位
\U开头后接16个十六进制位
这些十六进制位表示ISO 10646码点
## wchar_t
可以表示扩展字符集
长度大小取决于实现
处理该类型使用wcin和wcout，最新版本的iostream头文件提供了这些工具
前缀L表示宽字符串
## char16_t,char32_t
两者都是无符号的，前者长度16位，后者长度32位
前缀u表示char16_t类型的字符常量和字符串常量，char16_t类型与\u类通用字符名匹配
前缀U表示char32_t类型的字符常量和字符串常量，char32_t类型与\U类通用字符名匹配
wchar_t和char16_t和char32_t都有底层类型，随实现而异
## const限定符
在声明时应对const初始化，否则const值将是不确定且无法修改的
const值可以用于指定数组的长度
## 浮点数

- cfloat头文件中存在着实现对浮点数的设置
- 浮点常量的声明：f/F后缀将常量声明为float类型，l/L后缀将常量声明为long double类型，默认情况下浮点常量被作为double类型储存
## 类型转换

1. 初始化和赋值进行的转换：C++允许将一种类型的变量赋值给另一种类型的变量，值将自动转换为接受变量的类型![2023_01_15 18_57 Office Lens.jpg](https://cdn.nlark.com/yuque/0/2023/jpeg/34874768/1673780324945-d1b8a522-3af9-476f-aab5-ee6d8d43842d.jpeg#averageHue=%23dadada&clientId=u944ea6f5-a8f4-4&from=ui&height=2246&id=u2692a3b5&name=2023_01_15%2018_57%20Office%20Lens.jpg&originHeight=3520&originWidth=1046&originalType=binary&ratio=1&rotation=90&showTitle=false&size=430753&status=done&style=stroke&taskId=u8954f85f-c18f-43a0-b73f-4c52d15423a&title=&width=667.3333740234375)
2. 以{}方式初始化时进行的转换

列表初始化更加严格，不允许缩窄（narrowing），不允许将浮点型转换为整型，不同的整形之间或将整型转换为浮点型可能被允许，条件是编译器知道目标变量能够正确储存赋给它的值。如果是大类型要转换成小类型要求赋给变量的值来自于常量或const变量，不可以来自变量。
3.表达式中的转换
在计算表达式时，低于int的整型类型，将自动转换为int，即为整型提升（integral promotion），根据具体实现，如果short短于int，则unsigned short自动转换为int，如果short与int等长，则转换为unsigned int；wchar_t类型被提升为int，unsigned int，long，unsigned long中第一个宽度足够存储wchar_t取值范围的类型
当运算涉及两种类型的转换校验表：
![qq_pic_merged_1673780999725.jpg](https://cdn.nlark.com/yuque/0/2023/jpeg/34874768/1673781013027-09ecbb1f-0ef6-4630-ba2e-e711b00f8e22.jpeg#averageHue=%239f9c99&clientId=u944ea6f5-a8f4-4&from=paste&height=2282&id=uc2ab839e&name=qq_pic_merged_1673780999725.jpg&originHeight=1244&originWidth=452&originalType=binary&ratio=1&rotation=90&showTitle=false&size=123332&status=done&style=stroke&taskId=u2edff4b2-835a-4bdd-a02e-4478be1d7aa&title=&width=829)
4.向函数传递参数时的转换
传参类型一般由函数原型控制，当取消原型对参数的控制，C++将对char，short类型应用整型提升，对float参数提升为double
5.强制类型转换
语法一：（typeName）value // from C syntax
语法二：  typeName（value）//unique C++ syntax 
C++提供了强制转换运算符：static_cast<typeName> (value)   //这更加严格
## auto关键字
auto让编译器根据初始值的类型推断变量的类型，类似于Java中的var关键字
一般用于处理复杂类型，如标准模块库（STL）
