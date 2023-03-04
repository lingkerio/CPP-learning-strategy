# 逗号运算符
1. 将原本只能放一条表达式的地方，通过逗号将两条表达式合并放进去
2. 分隔数据对象参数
3. 合并的表达式从左向右执行
4. 逗号表达式的值是逗号右边（第二部分）的值
5. 逗号的优先级是所有运算符中最低的
# 字符串的比较

1. string类可以用关系运算符比较
2. C-风格字符串可以用库函数 strcmp/strncmp 比较
# 计时

1. C++库和ANSI C有一个函数clock()，返回程序开始执行后所用的系统时间
2. 系统时间的单位不一定是秒，且返回类型也不确定
3. 头文件ctime定义了一个符号常量——CLOCKS_PER_SEC，该常量等于每秒钟包含的系统时间单位数，故将系统时间除以这个值可以得到秒数，秒数乘以这个值也可以得到系统时间单位为单位的时间
4. ctime将clock_t作为clock()的返回类型，将变量声明为clock_t类型，编译器会将它转换成合适的类型
# 类型别名

1. 使用define预处理指令创建别名
2. 使用typedef关键字创建别名
3. 对于指针类型的别名，用typedef创建更好
# 基于范围的for循环（C++）

1. 语法为
```cpp
for (typeName variable : range)
    body
//这种循环会自动将范围内的值逐个赋给variable，如果variable前加&，表明其为一个引用变量
//则可以改变原范围的数据，否则就只是作为原范围数据的副本
```

2. 这种循环常用于各种模板容器类
# cin对文本输入的处理
## EOF（end of file）

1. windows命令提示符：Ctrl+Z
2. UNIX：行首Ctrl+D
3. 大多PC环境否额能识别Ctrl+Z，但是否必须在行首，是否必选下enter，各不相同
## 检测EOF

1. 检测到EOF后，cin将failbit和eofbit都设置为1
2. 成员函数eof()根据eofbit返回不同的值，eofbit为0时返回false，为1时返回true
3. 成员函数fail()根据failbit和eofbit返回不同的值，若eofbit或failbit为1，则返回true，否则返回false
4. 两种方法都是在事后报告
## 四种种cin输入成员函数

1. cin.get(arrayName,ArSize)最多读取ArSize个字符到数组中，返回一个cin对象
2. cin.get(charName)读取一个字符到一个char类型变量charName中，返回一个cin对象
3. cin.get()读取一个字符，并返回这个字符的ASCII码，读到文件尾返回EOF
4. cin.getline(arrayName,ArSize)最多读取ArSize个字符到数组中，返回一个cin对象

这些成员函数读到EOF后都会对 eofbit 和 failbit 进行设置
# cctype字符函数库
![2023_01_17 15_57 Office Lens.jpg](https://cdn.nlark.com/yuque/0/2023/jpeg/34874768/1673942290617-a2b01c6b-d809-44cc-ac61-4142f7f8f9ee.jpeg#averageHue=%23bca995&clientId=u56dbed3d-9e89-4&from=paste&height=1363&id=uaaec45e0&name=2023_01_17%2015_57%20Office%20Lens.jpg&originHeight=2663&originWidth=1383&originalType=binary&ratio=1&rotation=90&showTitle=true&size=541896&status=done&style=none&taskId=u6aa9f3ea-59f3-4b15-a953-418aa19cf19&title=cctype%E5%AD%97%E7%AC%A6%E5%87%BD%E6%95%B0%E5%BA%93&width=708 "cctype字符函数库")
# 


