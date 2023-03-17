# 文本文件I/O
[TOC]
## 文本文件输出

1. 包含头文件 **_fstream_**
2. 声明需要的 **_ofstream_**对象，并用合法且喜欢的方式命名如 **_fout_**
3. 指明名称空间 **_std _**,无论是使用编译指令_**using**_，还是使用前缀**_std::_**
4. 使用open方法将**_ofstream_**对象与文件关联起来
5. 使用完文件，应使用方法**_close_**将其关闭
6. 可结合使用_**ofstream**_对象和运算符**_<<_**来输出各种类型的数据
## 文本文件输入

1. 包含头文件 **_fstream_**
2. 声明需要的 **_ifstream_**对象，并用合法且喜欢的方式命名如 **_fin_**
3. 指明名称空间 **_std _**,无论是使用编译指令_**using**_，还是使用前缀**_std::_**
4. 使用**_open_**方法将**_ifstream_**对象与文件关联起来
5. 使用完文件，应使用方法**_close_**将其关闭
6. 可结合使用_**ifstream**_对象和运算符**_>>_**来输入各种类型的数据
```cpp
#include <bits/stdc++.h>
using namespace std;
const int SIZE = 60;
int main()
{
    char filename[SIZE];
    ifstream fin;
    cout << "Enter name 0f the data file ";
    cin.getline(filename,SIZE);
    fin.open(filename);
    if (!fin.is_open())
    {
        cout << "Could not open the file " << filename << endl;
        cout << "Program terminating.\n";
        exit(EXIT_FAILURE);
    }
    double value;
    double sum = 0.0;
    int count = 0;
    
    while (fin >> value)
    {
        ++count;
        sum += value;
        fin >> value;
    }
    if (fin.eof())
        cout << "End of file reached.\n";
    else if (fin.fail())
        cout << "Input terminated by data mimatch.\n";
    else
        cout << "Input terminated for unknown reason.\n";
    if (count == 0)
        cout << "No data processed.\n";
    else
    {
        cout << "Items read: " << count << endl;
        cout << "SUm: " << sum << endl;
        cout << "Average: "  << sum / count << endl;
    }
    fin.close();
    return 0;
}
```
