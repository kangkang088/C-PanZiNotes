# 飞思Cpp

# 2022年10月8日

# C/Cpp概述

Cpp：面向对象（以类为主体），面向过程

C：面向过程（以函数为主体）

面向对象：抽象、封装、继承、多态

类：具有相同或相似特征的实体的集合，类是一种自包含结构

语法上来说：类 = 属性(数据成员) + 行为(成员函数)

## class和struct的区别

1. C语言struct表示数据的集合
2. C++class和struct都可以表示类；Cpp中struct的默认访问权限是public，class是private

# 防卫式声明

**在使用文件时，先define，可以避免多次重复引用**

方式一：支持所有Cpp程序（推荐）

```Cpp
#ifndef __PATH_FILENAME_H__
#define __PATH_FILENAME_H__
...
#enddef
```

方式二：只支持VisualCpp

```Cpp
#program once
```

# class语法

```Cpp
类的定义:
class 类名
{
访问权限:
    数据成员
    成员函数
};
```

```Cpp
class {
private:
	...
public:
	...
protected:
	...
};
```

## this指针

类的成员函数中隐藏了this指针，this指向调用该函数的对象

所以，在类内函数调用类成员可以使用

```Cpp
this->memberName
```

一般情况下this可以省略不写
当形参与成员名相同时，成员名前必须添加this指针

## 类内定义自动内联

当函数于类内定义时，自动内联（编译器可能优化函数为内联函数）

C语言没有inline，但可以用#define

> 内联函数:以空间换取时间,当出现函数调用时，复制代码。代码过长、循环或者递归,不使用内联

# 类所占字节

空类占1个字节，用来标记类的存在

一般类的字节数是所有数据成员的字节数总和（需要考虑内存对齐和包含虚基类指针和虚函数表指针）

# 内存对齐

类会以数据成员当中最大字节数的成员做内存对齐，内存对齐是按照定义顺序来的。

> +的是内存对齐的字节数

比如

以下程序以4字节对齐，

4 

4

2 + 2 

4

所以是16

```Cpp
class Temp {
private:
	char str[10];
	short a;
	int b;
};
int main()
{
	cout << sizeof(Temp) << endl;
	//输出16
	return 0;
}
```

以下程序也以4字节对齐，但是是20字节

因为

2 + 2

4

4

4

2 + 2

所以是20

```Cpp
class Temp {
private:
	short a;
	int b;
	char str[10];
};
int main()
{
	cout << sizeof(Temp) << endl;
	//输出20
	return 0;
}
```

# 2022年10月9日

# 类的初始化方式

1. 公有的初始化函数
2. 构造函数
3. 直接初始化

# 空类所包含的内容

空类:1个字节 4个函数(合成构造函数、合成析构函数、合成拷贝构造函数、合成赋值运算符函数)

> 其实可能还有合成移动构造函数，合成移动拷贝运算符

# malloc和new的区别

1. malloc是函数,new是运算符;
2. new自动调用构造函数;
3. malloc返回的是void*，new返回的是对应指针

# 特殊的三大类函数

构造函数、析构函数、拷贝构造函数

## 构造函数

创建对象初始化
	1.函数名与类名相同;
	2.无返回值类型;
	3.创建对象时由系统自动调用;
	4.创建对象有两种方式: 类名 对象名; new 类名;
	5.当没有显式构造函数时，系统提供了隐式构造函数。类名(){}
	6.构造函数可以带参(重载)

## 析构函数

销毁对象
1.函数名  ~类名
2.无返回值类型
3.销毁对象时由系统自动调用
4.销毁对象有两种方式:1.生存周期结束。2.delete
5.当没有显式的析构函数，系统提供隐式析构函数 ~类名(){}
6.析构函数无参

## 拷贝构造函数

1.函数名与类名相同
2.类名(const 类名&);

### 拷贝构造函数调用情况

1.用类的对象给另外一个对象初始化;隐式或者显式
2.类对象作为函数的形参
3.返回值类型为类类型

# 2022年10月15日

# 类成员函数

类非静态成员函数都**隐式**的携带了一个this指针，所以可以直接在成员函数当中使用this指针。

# 类所占空间

类所占空间字节数有所有非静态数据成员函数决定（需要考虑内存对齐和虚基类指针和虚函数指针），成员函数不占内存

> 注意：静态成员在所有类中只有一份，所以sizeof(className)不会计算静态成员所占字节

# 静态成员

静态成员在所有类中只有一份，所有类共享这一份数据

## 静态数据成员

在类内使用static声明

静态数据成员必须在类外初始化，并且，此时不用再写static

```Cpp
type className::valueName = val;
```

## 静态成员函数

静态成员函数只能访问静态成员（包括静态数据和函数）

逻辑上，因为如果一个对象没有实例化，就不能访问其成员，因为不是静态成员

实现上，静态成员函数中，**没有this指针**，所以不能访问非静态成员。

# 如何在main函数之前执行代码

定义一个类类型的全局变量，此时在main调用之前，就会先调用这个类对象的构造函数

```cpp
Test {
public:
	Test() {
		cout << "Test constr" << endl;
	}
};

Test t;

int main() {
	cout << "main" << endl;
	return 0;
}
```

# static目前已知的应用

1. 静态全局变量
2. 静态局部变量:
3. 静态函数:
4. 静态数据成员:
5. 静态成员函数:

# 作业：

1. 特殊构造函数有哪些?
2. 单实例类两种形式(线程安全):懒汉模式和饿汉模式.
3. 写一个类，保证创建的所有对象都在堆区。

## 如何让类只有一份实例（单例模式）

让类的构造函数为private，提供一个接口，来获取这个接口，在这个接口当中实例化这一份实例。

# 2022年10月16日

# 数据成员初始化方式

1. 直接初始化
2. 公有成员函数
3. 构造函数
4. 成员初始化列表

# 类const成员

## const数据成员

使用const修饰数据成员

两种初始化：

1. 类内初始值
2. 构造函数初始化列表

> 拥有常量成员的类必须初始化其常量成员，否则，它的合成构造函数将是delete的。

## const成员函数

在声明成员函数时，在参数列表后使用const

此时，**const成员函数隐式携带的this指针为常量指针**（底层const，不可通过指针修改指向的值）。

```Cpp
void Func(const Test* this) const {
	...
}
```

所以，一般来说不可在const成员函数内修改成员值(但是可以修改其他值，如方法内定义的值）。

与static成员函数不同，const成员函数可以正常访问类内成员。

**可以通过使用mutable关键字，将成员声明为可修改的，这样在const成员函数中也可修改此值。**

```Cpp
class Test {
public:
	const int num = 0;
	mutable int mutableVal = 0;
	int val = 0;
	void Func() const  {
		mutableVal = 100;
		//val = 100; error
	}
};
```

# 友元

作用：使用friend声明的函数或类，可以直接访问此类的成员

特点：

1. 友元是单向的，即A类声明了一个友元类B，但是A类不可直接访问B类成员。
2. 友元是不传递的，A的一个友元B，B的一个友元C，但是A与C不是友元。
3. 友元是不继承的。

## 友元函数

1. 可以访问类中私有成员
2. 不是类的成员函数(该函数中没有this指针)

语法：在类内使用friend声明一个函数

```Cpp
friend void OutFunc();
```

## 友元类

1. friend关键字声明友元类
2. 友元类中所有成员函数都是友元函数

语法：在类内使用friend声明一个类

```Cpp
friend class outClass;
```

# 运算符重载

当自定义数据类型不支持该运算时，重载该运算符。

## 基本语法

```Cpp
返回值 函数名::operator 运算符(args) {...}
```

## 调用

1.函数形式

```Cpp
class.operator+(args);
```

2.运算符形式(优先级和结合性不变)

```Cpp
objA + objB;
```

## 重载+，-

需要返回一个新的类值，因为加法不改变本身值，返回一个新的类也可以达到链式加法的目的。

类内直接重载

```Cpp
Complex operator+(const Complex& rhs);
Complex operator-(const Complex& rhs);
```

类外声明为友元

```Cpp
friend Complex operator-(const Complex& lhs, const Complex& rhs);
friend Complex operator-(const Complex& lhs, const Complex& rhs);
```

## 重载<<，>>

<<应该声明为类外的友元函数，因为调用<<不是由类调用的，而是ostream 

并且需要返回ostream的引用，已到达链式输出的效果

> cout在io里只有一份，所以需要引用，又由于需要修改io流的状态，所以io流也不能为const

```cpp
friend ostream& operator<<(ostream& cout, const Complex& rhs);
```

\>\>同上

```Cpp
friend istream& operator>>(istream& in,  CComplex &com);
```

## 重载++，--

由于有前置和后置之分，所以，我们使用一个占位参数来区分前置和后置

没有的是前置，有的是后置

```Cpp
CClock operator++(int);//后置
CClock& operator++();//前置
```

# 不能被重载的运算符

分别是："?:"，”.”，“::”，“sizeof”，“.*”。

[ C++操作符重载（不能被重载的操作符）_ZWE7616175的博客-CSDN博客_+号重载符为什么没重载](https://blog.csdn.net/ZWE7616175/article/details/80439870)

# 作业

1. 写一个日期类(年月日):

   实现输入、输出、两个日期相减结果为相差天数

   一个日期+天数=另外一个日期

2. 写英雄类和地图类、实现英雄在地图中移动和切换地图

3. string类中重载赋值函数 operator=

# 2022年11月12日

# C文件读写

## sprintf

格式化输入，将args以format格式输入到target

```Cpp
sprintf(targetAddr, "format", args);
```

## fopen

打开文件，以openType方式打开file

```Cpp
fopen("filePath", "openType");
```

## fclose

关闭文件，关闭filePtr指向的文件

```Cpp
fclose(filePtr);
```

## fwrite

二进制写入，从targetAddr地址开始，读取size * number 个字节，写入到filePtr指向的文件

```Cpp
fwrite(targetAddr, size, number, filePtr);
```

## fread

二进制读取，从filePtr指向的文件，读取size * number 个字节，读取到targetAddr地址

```Cpp
fread(targetAddr, size, number, filePtr);
```

## 应用

```Cpp
	char path[20] = "";
	sprintf(path, "Res/Map/%d.map", m_Index);
	FILE *pfile = fopen(path,"rb");
	//读取文件数据:
	fread(&m_Row, sizeof(int), 1, pfile);//行数
	fread(&m_Col, sizeof(int), 1, pfile);//列数
	SetMemory();
	//读取地图元素的值(分行读取元素的值)
	for (int i = 0; i < m_Row; i++)
	{
		fread(m_pMap[i], sizeof(int), m_Col, pfile);
	}
	fclose(pfile);
```

# 作业

1. 切关(三维数组、文件读写)
2. 地图中拾取物品(消耗品:至少写两种(例如 红瓶、蓝瓶))要求存储到背包中、并能使用物品。

# 2022年11月13日

# 继承

继承是指子类继承父类所有属性，此时，这个类叫做派生类（子类），被继承的类叫做基类（父类）

父类派生子类： 派生类is基类

动物类派生出狗类：狗是动物

语法：

```Cpp
class ClassName : 继承权限 父类名 {
	...
};
```

## 继承方式

继承方式:公有继承、保护继承、私有继承

## 基类成员在派生类中的访问权限

父类成员权限	公有的		保护的		私有的
公有继承			公有的		保护的		不可访问的
保护继承			保护的		保护的		不可访问的
私有继承			私有的		私有的		不可访问的

## 派生类与基类构造与析构函数调用顺序

1. 先调用基类构造函数，如果有多个，按照继承顺序从左往右。
2. 再调用子对象的构造函数，如果有多个，按照定义顺序从上往下
3. 最后调用派生类自己的构造函数
4. 派生类析构函数调用顺序:与构造函数完全相反。

> 上述情况是在没有虚继承的情况下，虚继承情况将在后续讨论

## 派生类构造函数与基类构造函数

1. 如果直接基类构造函数不带参，在派生类中可以不显式调用

2. 如果直接基类构造函数带参，必须在派生类的成员初始化列表中显式调用

   > 因为基类拥有有参构造函数，基类就不会有合成无参构造函数，所以需要显示调用

3. 如果派生类中的子对象构造函数带参，也必须显式调用(成员初始化列表中)，理由同上

# 作业

Npc的基类:写出其两个派生类  输出其所有属性(基类构造函数必须带参)

# 2022年11月20日

# 基类和派生类转换

1. 基类对象 = 派生类对象 正确
2. 派生类对象 = 基类对象 错误
3. 基类指针可以指向派生类对象
4. 派生类对象不可以指向基类对象

# 菱形继承问题

如题，菱形继承问题，可以使用virtual关键字虚继承解决。

虚继承将在子类产生一个虚基类指针（4字节）

```Cpp
class Base {
public:
	void Print() {
		cout << "Base" << endl;
	}
};

class Derive: virtual public Base {
public:
	void Print(){
		cout << "Derive" << endl;
	}
};

int main()
{
	cout << sizeof(Derive) << endl;
    //4
}
```

# 虚基类

一个类被虚继承时

1. 如果基类有虚基类，先调用虚基类构造函数，再按照继承顺序从左往右依次调用

   构造函数调用顺序:虚基类->其他基类(继承顺序从左往右)->子对象(从上往下)->派生类

   析构函数与构造函数调用顺序完全相反

2. 如果虚基类构造函数带参，再其派生类中(不管其是否为直接派生)必须显式调用	

3. 虚基类只有一份拷贝(直接调用虚基类构造函数、当再次请求调用虚基类构造函数时，系统直接忽略)
	
4. 虚继承时，产生一个指针指向虚基类

# 作业

1. 了解C++强转类型（四种），并写出他们的区别。

# 2022年11月23日

# 多态

多态：对同一个消息的不同响应。

## 静态多态

编译时，确定了调用的函数（其实是父类函数覆盖子类函数）。

```Cpp
#include <iostream>
#include <math.h>

using namespace std;

class A {
public:
    void Init() {
        cout << "A Init" << endl;
    }
};

class B : public A {
public:
    void Init() {
        cout << "B Init" << endl;
    }
};

int main() {
    A* ptr = new B();
    ptr->Init();
    //A Init
    return 0;
}
```

## 动态多态

运行时，确定调用的函数。

**使用virtual声明函数，子类重写父类函数，此时将调用子类函数。**

```Cpp
#include <iostream>
#include <math.h>

using namespace std;

class A {
public:
    virtual void Init() {
        cout << "A Init" << endl;
    }
};

class B : public A {
public:
    void Init() {
        cout << "B Init" << endl;
    }
};

int main() {
    A* ptr = new B();
    ptr->Init();
    //B Init
    return 0;
}
```

当基类有虚函数时，子类会继承一个virtual table ptr，4字节

```Cpp
class Base {
public:
	virtual void Print() {
		cout << "Base" << endl;
	}
};

class Derive: public Base {
public:
	void Print() override {
		cout << "Derive" << endl;
	}
};

int main()
{
	cout << sizeof(Derive) << endl;
    //4
}
```

## 虚析构函数

普通析构函数无法析构子类对象，将构造函数声明为virtual，即虚析构函数即可析构子类对象。

**虚析构函数必须实现！**

```Cpp
class A {
public:
   
    virtual void Init() {
        cout << "A Init" << endl;
    }

    virtual ~A() {

    }
};
```

## 重载

同一个范围，函数名相同，参数不同

## 隐藏

不同范围，函数名相同，参数不同（不管是有virtual修饰）；

不同范围，函数名相同，参数相同（没有virtual修饰）。

## 覆盖

不同范围，函数名相同，参数相同（必须是虚函数）

> 这里的不同范围指的是不同类内

## 纯虚函数

```Cpp
virtual void Init() = 0;
```

拥有纯虚函数的类叫做抽象类，不能实例化，但是子类继承此类时，可以实现纯虚函数

## 抽象类

有纯虚函数的类叫做抽象类。

1. 抽象类不能创建对象（实例化）；
2. 在子类实现该方法，如果没有实现子类还是抽象类；
3. 抽象类可以定义指针或引用；

## 纯虚析构函数

```Cpp
virtual ~A() = 0;
```

和虚析构函数一致，只不过没有实现。

## 不能声明为虚函数的函数

构造函数：因为使用构造函数时，对象还未构造完成。

友元函数：因为友元函数不是类的成员函数。

静态成员函数：因为静态成员是全局的。

# 作业

1. 定义一个动物类：派生出狗、牛、羊三个子类，模拟动物叫声。
2. 了解简单工厂模式

# 2022年11月28日

# 模板

模板，是对于类（类型）的进一步抽象

## 函数模板的定义

> 模板声明和定义都写在一个头文件中

语法：

```Cpp
template<args,...>
returnType FunctinName(args) {
    ...
}
```

例如，定义一个加法的模板函数

```Cpp
template<class typeName, ...>
typeName Add(typeName lhs, typeName rhs) {
	return lhs + rhs;
}
```

> 注意：适配类型需要支持模板函数中的操作，比如上面的例子中，如果是自定义类型，需要重载+运算符

## 使用模板函数

直接使用

```Cpp
int n = Add(2, 2);
```

指定类型使用

```Cpp
int n = Add<int>(2, 2);
```

## 类型推导不应该有二义性

在上述例子中可以使用

```Cpp
int n = Add(2, 2);
```

使用模板函数

但是，如果

```cpp
int n = Add(2, 2.5);
```

将导致编译器报错，因为首先推导出的是int型，但是紧接着是double型，导致编译器无法确定推导类型。

此时，而使用一个普通函数解决。

```Cpp
int Add(int lhs, int rhs);
```

## 函数模板和普通函数调用优先级

1. 优先适配普通函数
2. 参数类型不一致，将先执行隐式转换调用普通函数
3. 上述两个不符合，再进行类型推导，使用模板函数

## 函数模板定义时可以指定普通类型参数

函数模板定义时可以指定普通类型参数，并且两种参数（推导类型和普通类型）可以有默认值

推导类型参数的默认值是类型，普通参数的默认值是数据值。

```Cpp
template<class T = int, int i = 0>
T Add(T lhs, T rhs) {
	return lhs + rhs + i;
}

int main() {
	cout << Add<int, 10>(1, 1) << endl;
    //12
	return 0;
}
```

## 类模板

使用类模板，可以将推导类型用于成员。

语法：

```Cpp
template<class T, int size = 1>
class Array{
private:
	T* items;
public:
	Array() {
        items = new T[size];
    }
}
```

## 模板类使用

使用时，**必须指定参数**，因为不像模板函数可以进行类型推导，类在构造时，本身就是一个类型，不可推导其本身。

```Cpp
template<class T = int, int size = 1>
class Array {
private:
	T* items;

public:
	int size;
	Array(): size(size) {
		items = new T[size];
	}
	void Print();
};

template<class T, int len>
void Array<T, len>::Print() {
	for (int i = 0; i < len; ++i) {
		std::cout << items[i] << " ";
	}
	std::cout << '\n';
}
```

```Cpp
int main() {
	Array<int, 10> t;
	t.Print();
	return 0;
}
```

## 类外声明模板类函数

类外声明类模板函数必须再使用函数模板，并指定类型

```Cpp
template<class T, int len>
void Array<T, len>::Print() {
	for (int i = 0; i < len; ++i) {
		std::cout << items[i] << " ";
	}
	std::cout << '\n';
}
```

# 作业

## 1.使用模板重写Array



# RPG作业要求

代码实现设计要求：

1. 要求使用面向对象思想（抽象、封装、继承、多态）
2. 需要使用多种设计模式（单例、工厂、外观等）
3. 必须包含实现动态数组类（作用于地图、背包）

游戏内容要求：

1. 读档，存档（使用文件或者其他方式，需要考虑性能问题，即不能直接全部写到文件，可以使用xml文件）

2. 战斗、升级

3. 背包（固定大小或无限扩容）

   > 固定大小时，必须可以丢弃物品

4. 拾取物品，购买物品，使用物品

5. 装备栏，状态栏

6. 至少三张地图

选做内容：

1. 技能、任务、联网
