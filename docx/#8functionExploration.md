# 内联函数
1. 以空间换时间
2. 函数声明或者定义需要使用关键字**_inline_**
3. 通常省略原型，将整个定义放在本应使用原型的地方
4. 内联函数不允许递归
5. 有些编译器可能因为函数过大或函数使用了递归而不将其作为内联函数
6. 函数定义占用多行的函数作为内联函数就不太合适
# 引用变量

1. 创建引用变量：typeName & reference = initializer;  // intializer is necessary
2. 引用变量将会一直效忠初始化时的那个变量
3. const修饰的引用作为函数形参时，有可能创建临时变量
   - 实参的类型正确，但不是左值
   - 实参的类型不正确，但可以转换为正确的类型
4. 引用参数尽可能声明为const
   - 使用const可以避免无意中修改数据造成的错误
   - 使用const可以使函数接受const和非const数据，否则只能接受非const数据
   - 使用const引用使函数能够正确生成并使用临时变量
5. C++11新增右值引用，用&&声明
6. 返回引用的函数实际上是被引用变量的别名，效率更高
7. 返回引用要注意不要返回被释放的内存单元的引用
8. 使用引用参数的原则
   1. 使用传递的值而不作修改的函数
      - 内置类型或小型结构，按值传递
      - 数组，按指向const的指针传递
      - 大结构，const指针或const引用
      - 类对象，const引用
   2. 修改调用函数中数据的函数
      - 内置数据类型，指针
      - 数组，指针
      - 结构，引用或指针
      - 类对象，引用
# 默认参数

1. 默认参数指当函数调用时省略了实参时自动使用的一个值
2. 设置默认值
```cpp
//for instance
char* left(const char * str, int n = 1);
```

3. 若有默认参数的形参对应的实参没有被省略，则实参会覆盖默认参数
4. 如果要为一个参数设置默认值，必须要为它右边的所有参数都设置默认值
5. 实参按从左到右的顺序赋值给形参，而不能跳过任何参数
# 函数重载

1. C++允许定义同名函数，条件是函数特征标（function signature）不同
2. 特征标即函数参数数目 & 参数类型
3. 如果函数调用没有匹配的原型，C++会尝试使用标准类型转换强制匹配，如果有多个原型能在转换后与函数调用匹配，C++将拒绝这种函数调用并将其视为错误
4. 类型引用和类型本身被视为同一个特征标，而是否是const参数被视为不同的特征标
5. 函数调用如果和多个原型匹配，将自动调用最合适的版本
6. 仅当函数基本上执行相同的任务但是用不同形式的数据时，才应该采用函数重载
7. 有时也可以通过默认参数起到函数重载的效果但比重载更简洁
# 函数模板
basic syntax:
```cpp
template <typename user_definite_name>//typename can be replaced by class
function prototype;

template <typename user_definite_name>//typename can be replaced by class
function definition;
```
## 具体化（specialization）
### 实例化

1. 显式实例化（explicit instantiation）
   - syntax:template return_type function_name<type> (parameter list);
   - 指明要实例化一个这样特定type的函数
2. 隐式实例化
   - 调用函数时根据参数类型自动实例
### 显式具体化（explicit specialization）

- syntax:template <> return_type function_name<parameter_type>(parameter list);
- 这种方式需要单独给这个模板函数写一个特定的定义

## 重载解析

1. 根据调用的函数名创建候选函数列表
2. 根据实参数目以及类型创建可行函数列表
3. 确定可行函数的优先级
   1. 完全匹配：完全匹配允许一些无关紧要的转换
      - 指向非const数据的指针或引用优先与指向非const数据的指针或引用结合
      - 非模板函数优先于模板函数
      - 显式具体化模板函数优先于隐式实例化
      - 转换进行更少的优先于转换进行多的
   2. 提升转换（整型提升，以及浮点类型的转变）
   3. 标准转换（整型变为字符型，整型变为浮点型）
   4. 用户定义的转换
4. 创建自定义函数选择：
- function<>(parameter list);//template function
- function<type>(parameter list);//explicit instantiation
### 

## 模板函数的发展

1. keyword：decltype
   - syntax：`decltype(expression) var;`
   - first:如果expression是一个没有用括号括起来的标识符，则var的类型与标识符类型一致
   - second：如果expression是一个函数调用，则var的类型与函数返回值类型一致
   - third：如果expression是一个左值（一种显而易见的情况：括号括起来的标识符），var为指向expression类型的引用
   - forth：前面条件都不满足时，var类型与expression类型一致
2. 后置返回类型
   - 当无法预先知道返回类型就可以后置说明
   - `auto function (parameter list) -> type`
   - 结合decltype：`auto function (parameter list) -> decltype(expression)`
