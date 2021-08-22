---
title: c++day01.md
date: 2021-08-21 10:52:00
tags:
---

# download

-  [ Windows10下载MinGW ]( https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win64/Personal%20Builds/mingw-builds/8.1.0/threads-posix/seh/?tdsourcetag=s_pctim_aiomsg )
  - 点击页面中的`x86_64-8.1.0-release-posix-seh-rt_v6-rev0.7z` 进行下载
  - 下载完成后把 `bin` 目录放入系统环境变量即可在终端使用 `c++` 命令进行编译 `.cpp` 源代码

# Hello World

- `MyFirstApp`

```c++
#include <iostream>

int main(){
    std::cout << "Hello World! \n"; // this will output to the console hello world
    system("pause>0");
}
```

```shell
# 编译
g++ .\MyFirstApp.cpp

# 运行
.\a.exe
```

- 换行  `\n` 或 ` << endl;`

- 编译命令 `g++ [source file] -o [output filename]`

# Variables 

- 命名
  - 构成: 下划线, 字母(区分大小写), 数字(不可数字开头)
  - 一般用小驼峰命名法

**Data types**

| 类型   | 定义 | size(bytes) | 说明                                           |
| ------ | --|--- | ---------------------------------------------- |
| 整数   | int | 4 | -2147483648 to 2147483647 |
| 字符 | char | 1 | 单引号为字符 'a' |
| 字符串 | string |  | 双引号为字符串 "character" |
| 布尔   | bool | 1 | true / false                                   |
| 浮点数 | float| 4 |  |
| 大浮点数 | double | 8 |  |

**Data type overflow**

- 变量的值超过其内存空间, 类似钟表指针, 13 点 = 1 点 (INT_MAX + 1 = INT_MIN)

**ASCII table**

- asign characters to number (it's for American)
- ASCII extends: utf-(1-16)  (for others)
- 字符转换为ASCII数字 `(int)'a'` 和 `int('a')` 两种写法

# Condition Statement

**语法**

`if(){}elif(){}else(){}`

- 注: 如果 `{}` 内只有一行代码, 可以不写 `{}`

```c++
#include <iostream>
using namespace std;

int main(int argc, char const *argv[])
{
    //User enters side lengths of a triangle (a, b, c)
    //Program should write out whethre that triangle is
    //equilateral, isosceles or scalene
    float a, b, c;
    cout << "a, b, c: ";
    cin >> a >> b >> c;
    
    if (a == b && b == c)
        cout << "Equilateral triangle";
    else
    {
        if (a != b && a != c && b != c)
            cout << "Scalene triangle";
        else
            cout << "Isosceles triangle";
    }

    return 0;
}
```

# Operators

```c++
#include <iostream>
using namespace std;

int main(int argc, char const *argv[])
{
    // 执行优先级 从上到下
    // + - * / %
    cout << 1 + 1 << endl;
    cout << 5 / 2 << endl;  // 2
    cout << 5.0 / 2 << endl;  // 2.5

    // ++, --
    int counter = 7;
    counter++;
    cout << counter << endl;
    counter--;
    cout << counter << endl;

    int counter2 = 7;
    cout << counter2++ << endl;  // 7
    cout << counter2 << endl;  // 8
    cout << ++counter2 << endl;  // 9

    system("cls"); // clear console

    // <, >, <=, >=, ==, !=
    int a = 5, b = 5;
    // cout << (a > b) << endl;  // 0 for false (1 for true)

    // &&, ||, !
    int c = 8, d = 9;
    // cout << !(c == 5 && b == 9);

    // 优先级
    cout << (c == 8 && d == 4 + 5);  // 1

    // =, +=, -=, *=, /=, %=
    int x = 5;
    x += 7;  //same as: x = x + 7
    cout << x << endl;

    return 0;
}
```

# 三目

```c++
#include <iostream>
using namespace std;

int main(int argc, char const *argv[])
{
    int hostUserNum, guestUserNum;
    cout << "HOST: ";
    cin >> hostUserNum;
    system("cls");
    cout << "Guest: ";
    cin >> guestUserNum;

    (hostUserNum == guestUserNum)? cout << "Correct!": cout << "Failed!";

    return 0;
}
```

# switch case

> 注意每个case后面必需接break退出, 因为程序只判断一次case条件, 进入一次后, 其他的case不会再判断, 会运行下面的所有case.

```c++
#include <iostream>
using namespace std;

int main(int argc, char const *argv[])
{
    float num1, num2;
    char operation;
    cout << "Caculator" << endl;
    cin >> num1 >> operation >> num2;

    switch (operation)
    {
    case '-':cout << num1 << operation << num2 << "=" << num1 - num2;
break;
    case '+':cout << num1 << operation << num2 << "=" << num1 + num2; break;
    case '*':cout << num1 << operation << num2 << "=" << num1 * num2; break;
    case '/':cout << num1 << operation << num2 << "=" << num1 / num2; break;
    case '%':
        bool isNum1Int, isNum2Int;
        isNum1Int = (int(num1) == num1);
        isNum2Int = (int(num2) == num2);

        if (isNum1Int && isNum2Int)
            cout << num1 << operation << num2 << "=" << int(num1) % int(num2);
        else
            cout << "Not valid!";

    break;
    
    default:cout << "Not valid opeation!"; break;
    }

    return 0;
}

```



