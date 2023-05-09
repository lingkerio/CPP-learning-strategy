# algorithm

算法设计有两个通用部分：

1. 使用模板来提供泛型
2. 使用迭代器来提供访问container中数据的通用表示

## STL算法组

STL将算法分成4组

- 非修改式序列操作
- 修改式序列操作
- 排序和相关操作
- 通用数字计算

前三者声明在algorithm头文件，余下定义在numeric头文件

## 算法的通用特征

in-place algorithm
or
copying algorithm
