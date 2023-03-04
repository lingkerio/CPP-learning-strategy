# 名称空间
```cpp
namespace aName {

declarations

}
```
## 名称空间的使用
---
> ### 1. using声明和using编译指令
>     using声明使得特定的标识符可用，using编译指令使得整个命名空间可用。使用using编译指令的话，局部版本将会覆盖名称空间版本。而使用using声明，局部版本和名称空间版本将会导致产生错误。
>     对变量使用::运算符将会直接调用变量的global namespace版本，即全局变量。
>     推荐只用using声明
> ### 2. 名称空间可以嵌套
>     可以用嵌套的命名空间访问嵌套的命名空间中的声明，也可用包含该命名空间的命名空间来访问。using编译指令是可传递的。
>     给名称空间创建别名,如下
```cpp
namespace my_very_favorite_things {...}
namespace mvft = my_very_favorite_things;
```
> ### 3. 匿名名称空间
>     创建一个名称空间但不命名，提供了链接性为内部的静态变量的替代品
