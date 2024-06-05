# 侯捷 - C++面向对象高级开发 - 上

# 第二课：头文件与类的声明

## 1.防卫式声明

> 谷歌代码规范

所有头文件都应该使用#define来防止头文件被多重包含,命名格式当是:
\<PROJECT\>\_\<PATH\>\_\<FILE\>\_H\_\.

为保证唯一性, 头文件的命名应该基于所在项目源代码树的全路径. 例如, 项目 foo 中的头文件 foo/
src/bar/baz.h 可按如下方式保护:

```cpp
#ifndef FOO_BAR_BAZ_H_
#define FOO_BAR_BAZ_H_
...
#endif //FOO_BAR_BAZ_H_
```

## 2.头文件（header）的布局

头文件应该按顺序包括以下几个部分

1. 前置声明
2. 类声明
3. 类定义

> 谷歌代码规范：尽可能地避免使用前置声明。使用 #include 包含需要的头文件即可。

## 3.类（class）声明

1. class head
2. class body

> 有一些函数在body直接定义，另一些在body外定义

```cpp
class className {
	class body
}
```

## 4.template简介

模板使得类可以实例化是才确定传入的类型

```cpp
template<typename T>
class complex {
	class body;
}
```

```cpp
complex<double> c1;
```

# 第三课：构造函数

## 1.inline（内联）函数

内联函数比普通函数快

但是即使声明了inline，编译器也不一定将函数确定为inline函数，inline关键字只是个声明（建议）

注意：

**函数若在class body内定义，便自动变成inline函数候选**

即在类定义时就定义函数，编译器可能会将其优化成inline函数

## 2.access level（访问级别）

1. public：公共访问，类内类外都可以访问，继承
2. private：私有，只有类内可以使用，不继承
3. protected：保护，类内类外都可访问，继承

## 3.constructor（ctor，构造函数）

```cpp
class complex 
{
public:
	complex (double r = 0, double i = 0)
		: re (r), im (i)
	{ }
}
```

构造函数可接初始化列表，直接初始化类成员，较赋值快

注意：**如果不使用初始化列表，在构造函数内即赋值**

## 4.ctor可以overloading(重载)

```cpp
complex () : re(0), im(0) { }
complex (double r = 0, double i = 0) 
    : re (r), im (i)
{ }        
```

# 第四课：参数传递和返回值

## 1.常成员函数

在成员函数后加const，可声明此函数为常成员函数

```cpp
double real () const { return re; }
```

作用：此函数内不允许改变成员的内容

## 2.参数传递

1. pass by value：值传递

   传递一个值的拷贝

2. pass by rederence：引用传递

   传递一个引用

注意：为了节省内存，尽量传引用