# function Object

函数对象(也可以被称之为functor——函数符)包括：**函数名、指向函数的指针、重载了()运算符的对象**。

## basic concept

- **generator**：无需参数就可以调用的函数符
- **unary function**：一个参数调用的函数符
- **binary function**：两个参数调用的函数符
- **predicate**：unary function and return bool
- **binary predicate**：binary function and return bool

## automatically adapt functor

functor携带了标识参数类型和返回类型的成员

STL提供了可以将二元自适应functor转换为一元自适应functor的函数
