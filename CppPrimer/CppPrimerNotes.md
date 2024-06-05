# CppPrimerNots

## 第二章 变量和基础数据类型

### 2.1.3 字面值常量

#### 指定字面值的类型

字符和字符串字面值可以使用前缀指定类型

| 字符与字符串前缀 |       类型       |   含义    |
| :--------------: | :--------------: | :-------: |
|        u         |     char16_t     | Unicode16 |
|        U         |     char32_t     | Unicode32 |
|        L         |     wchar_t      |  宽字符   |
|        u8        |       char       |   UTF-8   |
|   **整型后缀**   | **最小匹配类型** | **含义**  |
|      u or U      |     unsigned     |  无符号   |
|      l or L      |       long       |           |
|     ll or LL     |    long long     |           |
|  **浮点型后缀**  |     **类型**     |           |
|      f or F      |      float       |           |
|      l or L      |   long double    |           |

### 2.2.1 变量定义

#### 1.初始化不是赋值

注意：**初始化是指在变量创建是指定初始值，赋值是指在初始化后赋以新值**

#### 2.列表初始化

Cpp11允许所有变量使用花括号初始化

```cpp
int num{ 0 };
```

注意：当初值有丢失风险时，编译器会报错

```cpp
long double ld = 3.1415926536;
int a{ ld };	//error
```

#### 3.默认初始化

当变量没有指定初值时，称为默认初始化

### 2.4.1 const的引用

#### 1.对常量的引用可以不赋常量

```cpp
int num = 10;
const int& r1 = i;	//i 不为常量
```

#### 2.对常量的引用可以不赋左值

**即只要是一个常量，就可以赋值给常量的引用**

```cpp
int num = 10;
const int& r2 = i * 2;
const int& r3 = 10;
int& r4 = i * 2;	//error，非对常量的引用
```

### 2.4.3 顶层const与底层const

#### 1.顶层const

指针本身是一个const，则此const为顶层const

#### 2.底层const

指针所指向变量为const，则此const为底层const

注意：**底层const指针可以指向一个非const变量**，但是此时无法通过指针修改此变量值

```cpp
int num = 10;
int* const ptr = &num;
```

### 2.4.4 constexpr和常量表达式

#### 1.常量表达式

是指值不会改变的，并且在**编译过程**就得到计算结果的表达式。

如：字面值，const对象

#### 2.constexpr变量

Cpp11中，允许将变量声明为constexpr，让**编译器检查变量的值是否是一个常量表达式**

```cpp
constexpr int num = 20;	//字面值
constexpr int limit = num + 2;	//常量表达式
```

> tips：如果认为此变量的值是一个常量表达式，那就把它声明成constexpr

### 2.5.1 类型别名（typedef和using）

#### 1.using和typedef

```cpp
using SI = Sale_item;
typedef double wages;
```

### 2.5.2 auto

#### 1.auto会忽略顶层const

auto类型推导将会忽略顶层const，底层const则会保留下来

```cpp
const int num = 10;
auto a = num;
```

如果希望推导出顶层const，则需要明确指出

```cpp
const auto b = num;
```

### 2.5.3 decltype类型指示符

语法：decltype(内容)

作用：推导内容中值的类型

```cpp
decltype(func()) num;
```

注意：**内容中是什么类型，decltype就推导出什么类型**，这意味着可以推导出引用，即可以作左值

#### 1.decltype不会忽略顶层const

#### 2.declytype可以推导出引用

#### 4.给推导的变量加括号，则推导得到的为引用

```cpp
int num = 10;
//int& a
decltype((num)) a = num; //引用必须初始化
```

注意：**只有表达式为变量时才会如此**

```cpp
int num = 10;
decltype((num + 10)) a;	//int a
```

### 2.6.1 定义Sales_date类型

#### 1.类内初始值（Cpp11）

即类内声明成员属性时赋上初始值

```cpp
class A {
public:
	int num = 10;	//类内初始值
};
```

**当我们指定类内初始值时，必须以"="，"{}"形式赋值**

## 第三章 字符串、向量和数组

### 3.2.2 string对象上的操作

#### 1.getline()函数

getline读取一行数据，直到遇到换行（换行也读入）

```cpp
string line = "";
getline(cin, line);
cout << line << endl;
```

注意：**换行虽然被getline读入，但是不存储到line**，而是被丢弃了

#### 2.string::size_type类型

它是一种无符号整数类型，size()函数返回此类型的值

使用auto可以推导出此类型

### 3.3 vector

#### 1.buffer overflow

缓冲区溢出：通过下标访问不存在的元素

### 3.5.2 访问数组元素

#### 1.size_t类型

就是unsigned int

> typedef unsigned int     size_t;

#### 2.difference_t

有符号整数类型（通常是std::ptrdiff_t ）

为了方便迭代器（指针）相减而产生的

> typedef int              ptrdiff_t;

#### 3.intptr_t

> typedef int              intptr_t;

### 3.5.3 指针和数组

#### 1.标准库函数begin和end（Cpp11）

Cpp11新标准，begin和end函数

begin()

> 定义于头文件 `<iterator>`
>
> 返回指向给定容器 `c` 或数组 `array` 起始的迭代器。这些模板依赖于拥有合理实现的 C::begin() 。

end()

> 定义于头文件 `<iterator>`
>
> 返回指向给定容器 `c` 或数组 `array` 结尾（即最末元素的后一元素）的迭代器。这些模板依赖于拥有合理实现的 C::end() 。

```cpp
	int ary[10] = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 0 };
	int* ptr = begin(ary);
	cout << *ptr << endl;	//1

	int* lastNextPtr = end(ary);
	cout << *(lastNextPtr - 1) << endl;	//0
```

注意：对于容器依然适用

> [std::end, std::cend_C++中文网 (c-cpp.com)](https://c-cpp.com/cpp/iterator/end)

### 3.5.5 与旧代码的接口

#### 1.c_str()

string提供了一个函数，使得其内容转换为c风格字符串

string.c_str();

```cpp
string str = "abcd";
const char* cStr = str.c_str();
```

#### 2.使用数组初始化vector

通过begin和end

```cpp
int ary[10]{ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
vector<int> vec(begin(ary), end(ary));
```

直接使用指针

```
int ary[10]{ 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
vector<int> vec(ary, ary + 10);
```

## 第四章 表达式

### 4.9 sizeof运算符

#### 1.sizeof有两种形式

```cpp
sizeof(type/type);
sizeof expr;
```

注意：**第二种方式运算对象只能是表达式**

注意：**sizeof返回一个常量表达式**

### 4.1 类型转换

#### 1.何时发生隐式转换

1. 在大多数表达式中，比int类型小的整型值首先提升为较大的整数类型（整型提升）
2. 在条件语句中，非布尔值转换为布尔类型
3. 初始化过程中，初始值转换为变量类型
4. 在赋值语句中，右侧运算对象转换成左侧运算对象的类型
5. 算术运算或关系运算的运算对象将转换为同一类型
6. 函数调用时会发生隐式的类型转换

### 4.11.1 算术转换

#### 1.整型提升

​	整型提升( integral promotion)负责把小整数类型转换成较大的整数类型。对于 bool、char、signed char、unsigned char、short和unsigned short等类型来说，只要它们所有可能的值都能存在 int 里，它们就会提升成int类型;否则，提升成unsigned int类型。就如我们所熟知的，布尔值false提升成0、true提升成1。
​	较大的char类型(wchar_t、char16_t、char32_t)提升成int.unsigned int、long、unsigned long、long long和unsigned long long中最小的一种类型，前提是转换后的类型要能容纳原类型所有可能的值。

### 4.11.2 其他隐式转换

#### 1.转换成常量

允许指向非常量类型的指针转换成指向相应的常量类型的指针，对于引用也是如此

```cpp
int i = 10;
const int& crefI = i;
const int* cptr = &i;
//int& ref = crefI;	//error
//int* p = cptr;	//error
```

#### 2.类类型定义的转换

允许类类型隐式转换，但是每次只能转换一次

```cpp
string str = "abcd";	//
```

### 4.11.3 显式转换

#### 1.强制转换

使用一下形式转换：

```cpp
cast-name<type>(expr);
```

type是转换的目标类型，expr是要转换的值或表达式，如果type是引用类型，则结果是左值

#### 2.四种cast-name（转换方式, Cpp11）

##### 1.static_cast，默认转换

任何具有明确定义的类型转换，只要不包含底层const，都可以使用static_const

##### 2.const_cast，常量转换为非常量

const_cast只能改变运算对象的底层const

```cpp
const char* pc;
char* p = const_cast<char*>(pc);	//正确，但是通过p写值是未定义行为
```

**const_cast常常用于有函数重载的上下文中**

##### 3.reinterpret_cast，类型转换

将此expr转换为指定类型

**注意，这只是低级层次的类似声明的转换，类似C语言的直接强制直接转换**

##### 4.dynamic_cast，动态类型转换

支持运行时类型识别，具体在19.2节

#### 3.旧式的转换（C语言直接转换）

```cpp
type(expr);
(type)expr;
```

直接将expr转换为type类型

### 4.12 运算符优先级表

P166

## 第五章 语句

### 5.5.3 goto语句

#### 1.goto语法

```cpp
goto label;
```

label即标签

#### 2.带标签语句

```cpp
begin:
	int x = 10;
```

注意：**label不会与程序变量命名冲突，只是一个标记**

### 5.6.2 try和throw

#### 1.throw语法

```cpp
throw exception_type(字符串);
```

注意：**我们必须初始化异常对象，使用字符串**

#### 2.try语法

```cpp
try {
	...
}
catch (excepetion_type item) {
	...
}
```

当在try语句块内抛出一个异常时，catch可以捕获到item，获得其信息

#### 3.异常成员函数what()

无论哪种类型的异常，每一异常对象都有一个what()函数

返回的的是一个const char*，即创建异常时的字符串

所以我们可以打印其中内容

```cpp
cout << item.err() << endl;
```

#### 4.catch的执行

>   ​	在复杂系统中，程序在遇到抛出异常的代码前，其执行路径可能已经经过了多个try语句块。例如，一个try语句块可能调用了包含另一个try语句块的函数，新的try语句块可能调用了包含又一个try语句块的新函数，以此类推。
>   ​	寻找处理代码的过程与函数调用链刚好们相反，并在调用该函数的函数中继续寻的函数。如果没找到匹配的catch 于可，资立个新的亟狗也被终止，继续搜索调用它的找。如果还是没有找到匹配的 catch 于，运一有刚找效话当类型的catch子句为止。函数。以此类推，沿着程序的执行路径逐层回退，直到找到适当类型的catch子句为止。
>   ​	如果最终还是没能找到任何匹配的catch子句，程序转到名为terminate 的标准库函数。该函数的行为与系统有关，一般情况下，执行该函数将导致程序非正常退出。
>   ​	对于那些没有任何try语句块定义的异常，也按照类似的方式处理:毕竟，没有try语句块也就意味着没有匹配的catch子句。如果一段程序没有try语句块且发生了异常，系统会调用terminate函数并终止当前程序的执行。

### 5.6.3 标准库异常类

#### 1.\<stdexcept\>定义的异常类

|        类        | 通常含义                                       |
| :--------------: | :--------------------------------------------- |
|    exception     | 最常见的问题                                   |
|  runtime_error   | 运行时错误                                     |
|   range_error    | 运行时错误：生成的结果超出了有意义的值域范围   |
|  overflow_error  | 运行时错误：计算上溢                           |
| underflow_error  | 运行时错误：计算下溢                           |
|   logic_error    | 程序逻辑错误                                   |
|   domain_error   | 逻辑错误：参数对应的结果只不存在               |
| invalid_argument | 逻辑错误：无效参数                             |
|   length_error   | 逻辑错误：试图创建一个超出该类型最大长度的对象 |
|   out_of_range   | 逻辑错误：使用一个超出有效范围的值             |

#### 2.标准库中的异常类

| 头文件     | 异常类              |
| ---------- | ------------------- |
| exception  | exception           |
| stdexecept | 见上表              |
| new        | bad_alloc(12.1.2节) |
| type_info  | bad_cast(19.2节)    |

注意：**exception只报告异常发生，而不提供任何额外信息**

注意：**exception，bad_alloc，bad_cast只能使用默认初始化，不给你赋初始值**

## 第六章 函数

### 6.1.1 局部对象

#### 1.自动对象

只存在块执行期间的对象称为自动对象

块执行完后，块内创建的自动对象的值将为未定义

**函数形参是自动对象**

### 6.2.5 main：处理命令行选项

p196

### 6.2.5 含有可变形参的函数

#### 1.initializer_list（初始化列表类型,Cpp11）

如果函数参数类型相同但是数量未知，可以使用初始化列表类型作为函数参数

1. initializer_list是一个模板类型
2. initializer_list中的元素全部都为const

#### 2.省略符形参

为了让Cpp程序访问使用了varargs的C标准库的C代码而设置的。

形式：出现在形参最后位置

```
void foo(pram_list, ...);
void foo(...);
```

### 6.3.2 有返回值的函数

#### 1.返回右值引用的函数可以作左值

```cpp
int& function(int& num) {
	return num;
}

int main() {
	int num = 0;
	function(num) = 100;
	cout << num << endl;
}
```

#### 2.列表初始化返回函数返回值（Cpp11）

```cpp
vector<int> function() {
	return { 1, 2, 3, 4 };
}
```

#### 3.main函数的返回值

main函数的返回值一般与机器有关

但在\<cstdlib\>中定义了两个预处理变量

```cpp
EXIT_FAILURE
EXIT_SUCCESS
```

### 6.3.3 返回数组指针

#### 1.直接返回数组指针的两种形式

形式：

直接定义

```cpp
type (*function(param_list))[dimention] {
	
}

int (*function(int temp))[10];	//声明了一个返回数组大小为10的数组指针的函数
```

使用typedef

```cpp
typedef int(*aryPtr)[10];
aryPtr function(int temp);	
```

#### 2.尾置返回类型（Cpp11）

语法:

```cpp
auto func(int val) -> int(*)[10];	//声明了一个返回数组大小为10的数组指针的函数
```

#### 3.使用decltype

```
int ary[] = { 1, 2, 3, 4, 5, 6};

decltype(ary) *func(int val);
```

注意：**decltype关键字中表达式的类型是什么类型，得到的类型就是什么类型，所以此处得到一个数组，需要加上*才返回的是一个数组指针**

### 6.4 函数重载

#### 1.顶层const不能作为函数重载条件

**因为顶层const可以接受非const**

```cpp
int func(const int val);
int func(int val);			//error 顶层const
```

#### 2.底层const可以作为函数重载条件

注意：**只有当参数为指针或者引用是，才有底层const**

```cpp
int func(const int *ptr);
int func(int* ptr);			//两个func不同

int fuc(const int& ref);
int fuc(int& ref);			//两个func不同
```

### 6.5 特殊用途语言特性

### 6.5.2 内联函数和constexpr函数

#### 1.内联函数

使用inline声明

注意：**inline只是给编译器一个请求，编译器可以忽略这个请求，inline是由编译器决定的**

#### 2.constexpr函数

constexpr函数是指可以用于常量表达式的函数，即这种函数一般返回常量

初始化时，编译器将constexpr函数的调用替换成其结果值，且会将其**隐式的指定为inline函数**

##### 1.constexpr函数的几项约定

1. 函数返回值必须为字面值类型
2. 所有形参类型必须为字面值类型
3. 函数体中只能有一条return语句

##### 2.constexpr函数允许返回非常量

```cpp
constexpr int new_sz() {
	return 42;
}

constexpr int scale(size_t cnt) {
	return new_sz() * cnt;
}
```

注意：此时，只有scale传入常量，scale返回的才是常量，否者将不返回常量

```cpp
int arr[scale(4)];
int i = 2;
//int arr2[scale(i)];		//错误，i不是一个常量
```

#### 3.把内联函数和constexpr函数定义放在头文件内

内联函数和constexpr函数可以在程序中**多次定义**，为了使其一致，通常将定义置于头文件中

### 6.5.3 调试帮助

#### 1.assert宏

```cpp
assert(expr);
```

作用：对于expr求值，真则无事，假则中断程序并输出信息

#### 2.NDEBUG

assert依赖于此预处理变量，如果定义了NDEBUG，assert将什么也不做

#### 3.\_\_func\_\_

编译器为每个函数都定义了\_\_func\_\_，是一个const char*的静态数组，用于存放函数名字

可以直接输出这个量

```cpp
void Solution() {
	cout << __func__ << endl;
}
```

#### 4.另外4个比较有用的预处理量

1. \_\_FILE\_\_：存放文件名的字符串字面值
2. \_\_LINE\_\_：存放当前行号的整型字面值
3. \_\_TIME\_\_：存放文件编译时间的字符串字面值
4. \_\_DATE\_\_：存放文件编译日期的字符串字面值

## 第七章 类

### 7.1.2 定义改善的Sales_data类

#### 1.成员函数隐式包含this指针

当成员函数声明时，隐式包含this指针，形如

```cpp
class A {
public:
	void fucn(int a, A* this) {
		
	}
}
```

#### 2.const成员函数

const成员将包含一个底层const的this指针，以达到不可修改类成员的目的

形如

```cpp
class A {
public:
	void fucn(int a, const A* this) const {
		
	}
}
```

#### 3.定义在类内部的函数时隐式内联的

定义在类内部的函数时隐式的inline函数

#### 4.常量对象、常量对象的引用或指针，只能调用常量成员函数

常量对象、常量对象的引用或指针，只能**调用常量成员函数**，成员属性不受影响

### 7.1.4 构造函数

#### 1.构造函数不能声明为const

因为即使是一个const对象，构造过程中，也可能需要对成员进行一些赋值修改操作

只有构造完成后，const对象才具有常量属性

注意：**可以声明为constexpr**

#### 2.只有当没有声明构造函数时，编译器才会生成默认构造函数

只有当没有声明构造函数时，编译器才会生成默认构造函数

即，只要有一个构造函数，无论有参还是无参，编译器就不会生成默认构造函数

#### 3.=default（显式的声明默认构造函数）

显式的声明默认构造函数

即，**当已经声明了其他构造函数时，还需要编译器自动生成的默认构造函数**，可以使用=default

语法：

```cpp
class A {
public:
	A() = default;
};
```

注意：参构造函数只有当在类内定义才会隐式内联，在类外部定义不会，和普通函数一致

### 7.2.1 友元

#### 1.友元只能声明在类的内部

如题，且友元只是一个函数声明，并非函数定义

**友元函数不是类成员函数**

### 7.3.1 类成员再探

#### 1.可变数据成员（mutable关键字）

为了使得数据成员在const函数内任然可变，可以使用mutable关键字声明成员

### 7.3.4 友元再探

#### 1.可以将一个类声明为友元

即

```cpp
class A {
public:
	friend class B;
private:
	...
};

class B {
public:
  ...  
};
```

#### 2.友元没有传递性

即上述例子中，类B的友元，不能访问类A中私有成员

### 7.5.1 构造函数再探

#### 1.当具有const和引用成员时，必须使用初始化列表

因为const和引用成员必须初始化

#### 2.初始化列表的顺序只与成员声明顺序有关

```cpp
class A {
public:
	int x;
	int j;
	int y;
	A(int val) : y(val), j(y), x(j) { }	//未定义行为
};
```

**上述代码可能会引起警告，因为x的初始化位于y和j之前**

即无论代码中初始化列表顺序如何，类成员的初始化只与类成员声明顺序有关

### 7.5.2 委托构造函数（Cpp11）

#### 1.委托构造函数

Cpp11允许一个构造函数调用另外一个构造函数，称为委托构造函数

```cpp
class A {
public:
	string msg;
	unsigned int num;
	double fl;
	int temp;
	//非委托构造函数
	A(string str, unsigned int val, double price, int ID) :
		msg(str), num(val), fl(price), temp(ID) { }
	//委托构造函数
	A() : A("", 0, 0, 0) { }
	A(string str) : A(str, 0, 0, 0) { }
	A(int val, double price) : A(to_string(val)) { }
};
```

### 7.5.3 默认构造函数的作用

#### 1.A temp() 是一个函数，而不是一个对象！！！

将设有

```cpp
class A {
	...
};
```

**新手错误！！！**

```cpp
A temp;	//正确，调用默认构造函数
```

### 7.5.4 隐式类类型转换

#### 1.只允许一步类类型转换

```cpp
class A {
public:
	string str;
	A(string temp) : str(temp) {

	}
};

void func(A cA) {
	cout << cA.str << endl;
}

int main() {
	//const char* -> string -> A	错误
	func("99999");	
	return 0;
}
```

正确写法

```cpp
int main() {
	func(string("99999"));
	return 0;
}
```

注意：只是不允许类类型多步转换，基本内置类型是允许的

```cpp
class A {
public:
	int num;
	A(int temp) : num(temp) {

	}
};

void func(A cA) {
	cout << cA.num << endl;
}

int main() {
	//double -> int -> A	基本内置类型，正确
	func(10.99);
	return 0;
}
```

#### 2.抑制构造定义的隐式转换（explicit）

使用explicit关键声明构造函数时，此构造函数不可隐式转换

为使用explicit前

```cpp
class B {
public:
	int num;
	B(int temp) : num(temp) {

	}
};

void func(B temp) {
	cout << temp.num << endl;
}

int main() {
	func(10);	//正确，存在隐式转换
	return 0;
}
```

使用explicit后

```cpp
class B {
public:
	int num;
	explicit B(int temp) : num(temp) {

	}
};

void func(B temp) {
	cout << temp.num << endl;
}

int main() {
	func(10);	//错误，不存在隐式转换
	return 0;
}
```

#### 3.explicit只对有一个参数的构造函数有效

所以可以不用讲有多个参数的构造函数声明为explicit

#### 4.explicit只能用于构造函数

如题

#### 5.explicit只能用于直接初始化

即必须使用"()"初始化，不能使用"="，因为"="是另外一个拷贝构造函数

```cpp
class B {
public:
	int num;
	explicit B(int temp) : num(temp) {

	}
};

int main() {
	B cB(10);		//正确，直接初始化，调用explicit B(int temp)
	B tempB = 10;	//错误，调用的是拷贝构造函数，未声明
	return 0;
}
```

#### 6.explicit总结

1. 为了使构造函数没有隐式转换，使用explicit关键字声明构造函数
2. explicit只能用于构造函数
3. explicit只对有一个参数的构造函数有效
4. 使用显示转换，可规避explicit
5. 隐式转换多出现于类作函数参数

### 7.5.5 聚合类

满足一下条件的类是聚合类：

1. 所有成员都是public
2. 没有定义如何构造函数
3. 没有类内初始值
4. 没有基类，也没有virtual函数

其实就是全部都是数据的类，数据聚合（结构体）

### 7.5.6 字面值常量类

字面值常量类可能包含constexpr成员函数

#### 1.数据成员都是字面值类型的聚合类是字面值常量类

如题

#### 2.如果不是一个聚合类，但复合一下条件的类也是字面值常量类

1. 数据成员都必须是字面值类型
2. 类必须至少含有一个constexpr构造函数
3. 如果一个数据成员含有类内初始值，则内置类型成员的初始值必须是常量表达式；或者如果成员属于某种类类型，则初始值必须使用成员自己的constexpr构造函数
4. 类必须使用析构函数的默认定义

#### 3.constexpr构造函数

1. constexpr构造函数**必须初始化所有成员**，且必须使用常量表达式或者constexpr构造函数初始化
2. constexpr构造函数一般没有语句

#### 4.constexpr构造函数可以=default

**只有当没有其他数据成员或者其他数据成员均有类内初始值时**

### 7.6 类的静态成员

#### 1.类的静态成员只有一份

任何一个类都包含且共享静态成员

所以可以直接使用作用域符访问类静态成员

#### 2.静态成员函数没有this指针

静态成员函数不需要通过作用域符访问静态成员，可以直接访问

#### 3.static声明只出需要现在类内部

外部定义时，不需要static

#### 4.static类内初始值必须是constexpr

不然不允许赋类内初始值

#### 5.static成员可以是类本身对象

之前，普通成员时是不能是本身类对象的，使用static可使得类包含本身

#### 6.static成员可以做成员函数实参

普通成员是不可以的

## 第八章 IO库

### 8.1.1 IO对象无拷贝或赋值

所以一般以引用方式传递参数，且由于需要改变IO对象，所以不能是const的

### 8.1.2 条件状态

P312 表8.2：IO库条件状态

### 8.1.3 管理输出缓冲

#### 1.缓冲刷新原因

1. return时，执行缓冲区刷新
2. 缓冲区满时
3. endl，flush，ends显示刷新
4. 使用操纵符unitbuf设置流状态，清空缓冲区，对应nounitbuf
5. cerr是设置unitbuf的
6. 当读写关联的流时，缓冲区刷新，默认情况下，cerr和cin关联cout

#### 2.显示刷新缓冲区

1. endl，输出一个换行并刷新
2. flush，只刷新
3. ends，输出一个空字符并刷新

#### 3.unitbuf操纵符

```cpp
cout << unitbuf;	//所有输出操作后都会立即刷新缓冲区
cout << nounitbuf; 	//回到正常缓冲
```

#### 4.关联输入流和输出流

使用tie函数

无参返回关联的流的指针，没有关联返回空指针

有参则参数为指定需要关联的流

```cpp
cin.tie(&cout);
```

### 8.2.2 文件模式

|  模式  |             含义             |                  备注                  |
| :----: | :--------------------------: | :------------------------------------: |
|   in   |         以读方式打开         |                                        |
|  out   |         以写方式打开         |                                        |
|  app   | 每次写操作前均定位到文件末尾 |                                        |
|  ate   | 打开文件后立即定位到文件末尾 |                                        |
| trunc  |           截断文件           | 只有当out模式设定时，才可指定trunc模式 |
| binary |        以二进制方式IO        |                                        |

样例：

使用按位或指定多个模式

```cpp
ofstream out("file.txt");
ofstream out1("file.txt", ofstream::out | ofstream::trunc);
```

#### 1.默认为out和trunc模式，会截断文件

此时，文件会被截断

**保存原有文件的唯一方式是使用in或者app**

### 8.3 string流

#### 1.stringstream操作

|       操作       |                     含义                      |
| :--------------: | :-------------------------------------------: |
|  sstream strm;   |       定义一个没绑定的stringstream对象        |
| sstream strm(s); | strm保存了一个s的拷贝，此构造函数时explicit的 |
|   strm.str();    |          返回strm所保存的string拷贝           |
|   strm.str(s);   |           将s拷贝到strm中，返回void           |

### 8.3.1 使用istringstream

#### 1.使用istringstream

输入一段字符串，将其中单词都保存到一个vector

```cpp
string line;
getline(cin, line);
istringstream record(line);	//绑定line
vector<string> words;
string temp = "";
while (record >> temp) {	//读取line中数据，以空格隔开
	words.push_back(temp);
}
```

### 8.3.2 使用ostringstream

#### 1.使用ostringstream

将数组中所有每个单词放入一个ostringstream

```cpp
vector<string> words;
...	//输入words
ostringstream record;
for (auto& word : words) {
    record << " " << word;
}

cout << record.str() << endl;
```

## 第九章 顺序容器

### 9.1 顺序容器概述

**除了链表，其他顺序容器都支持随机（下标）访问**

|     容器     |       含义       |
| :----------: | :--------------: |
|    vector    | 可变数组（向量） |
|    deque     |     双端队列     |
|     list     |     双向链表     |
| forward_list |     单向链表     |
|    array     |   固定大小数组   |
|    string    |      字符串      |

### 9.2.4 容器的列表初始化

#### 1.标准库arrayj具有固定大小

```cpp
array<int, 10>		//类型为：保存10个int的数组
```

#### 2.可以用内置数组拷贝构造array

```cpp
int nums[10] = { 1, 2, 3, 4, 5};
array<int, 10> ary = nums;
```

注意：**内置数组是不可以如此拷贝初始化的**

### 9.2.5 赋值和swap

#### 1.assign赋值

|       操作       |               含义               |
| :--------------: | :------------------------------: |
| seq.assign(b, e) | 将seq元素替换为迭代器b-e范围元素 |
|  seq.assign(il)  | il表示一个初始化列表，赋值给seq  |
| seq.assign(n, t) | 将seq中内容替换为n个值为t的元素  |

注意：**assign操作会使得指向容器左部的迭代器、引用和指针失效**

注意：assign操作不适用关联式容器和array

#### 2.swap为常数时间的交换

除了array外，swap不对任何元素进行拷贝、删除和插入操作，因此swap是在常数时间内完成的

### 9.2.6 容器大小操作

empty()：判空

size()：返回大小

max_size()：返回元素类型最大容量

#### 1.forward_list 不支持size

但是支持max_size和empty

### 9.3.1 向顺序容器添加元素

#### 1.向vector、string或deque插入元素会使得迭代器、引用、指针失效

如题

#### 2.insert操作可以返回插入后当前位置迭代器

```cpp
list<string> lst;
auto iter = lst.begin();
while(cin >> word) {
	iter = lst.insert(iter, word);	//等价于调用push_front();
}
```

#### 3.emplace可以构造一个元素，push拷贝一个元素

如题

### 9.3.2 访问元素

**at和下标操作不使用于list，back不使用与forward_list**

#### 1.at可以抛出异常

越界时，将抛出out_of_range异常

### 9.3.4 特殊的forward_list操作

p313

### 9.3.6 容器操作可能使得迭代器失效

#### 1.不要保存end返回的迭代器

因为end经常会失效

### 9.4 vector对象是如何增长的

#### 1.容器大小管理操作

|       操作        |                 含义                 |
| :---------------: | :----------------------------------: |
| c.shrink_to_fit() | 将capccity减少为与c.size()相同的大小 |
|   c.capacity()    |       返回C现在可以保存的容量        |
|   c.reserve(n)    |   分配至少能容纳n个元素的内存空间    |

注意：

**shrink_to_fit()只适用于vector、string和deque**

**capacity()和reserve只适用于vector和string**

### 9.5.3 string搜索操作

#### 1.find_first_of(args)

find_first_of(),find_last_of(),查找第一，最后一次出现的位置

find_first_not_of(),find_last_not_of()，查找第一、最后一个不在args中的字符

### 9.5.4 compare函数

类似strcmp

p327

### 9.5.5 数值转换

例：

```cpp
stoi(s, p = 0, b = 10);
```

p328

### 9.6 容器适配器

容器适配器是指，底层使用其他容器实现，使得其具备特殊的性质

默认情况下，stack和queue是基于deque实现的，priority_queue是在vector上实现的

我们可以指定其实现

```cpp
stack<sting, vector<string>> str_stk;
```

## 十、第十章 泛型算法

### 10.2.1 只读算法

#### 1.find(b, e, val)

在迭代器范围内查找val，成功返回迭代器或者指针

#### 2.accumulate(b, e, val)

计算迭代器范围内的元素和，初始值为val

注意：此为执行+操作，所以对于string，是将所有元素相连

#### 3.equal(lhsb, lhse, rhsb)

比较两个迭代器范围内元素是否相等，是返回true，不是返回false

注意：equal假定rhs和lhs一样长，如果不一样长，将会造成错误访问

### 10.2.2 写容器算法

#### 1.fill(b, e, val)

将迭代器范围内所有元素置为val

#### 2.fill_n(b, size, val)

将迭代器指向容器置为val

注意：**fill_n不检查写操作，即即使容器是空的，也不报错**

#### 3.back_inserter（插入迭代器）

插入迭代器，返回容器插入位置

所以常常使用插入迭代器来创建容器

```cpp
vector<int> vec;
fill_n(back_inserter(vec), 10, 0);
```

#### 4.拷贝算法（copy）

copy(b, e, b);

#### 5.replace(b, e, reval, val)

将迭代器范围内所有reval替换为val

replace_copy(b, e, insertPos, reval, val)

insertPos为插入位置

### 10.2.3 重排容器元素算法

#### 1.unique（b, e）

对于有序的容器，使用unique算法，将容器重新排列，使得容器没有重复元素

返回最后一个不重复元素之后的位置的的迭代器

注意：**这只是重新排列，只是将重复元素移动到末尾，未执行删除操作，如需要删除，需使用erase**

例：删除重复单词

```cpp
sort(words.begin(), words.end());
auto end_unique = unique(words.begin(), words.end());
words.erase(end_unique, words.end());
```

### 10.3.1 向算法传递函数

#### 1.谓词

谓词是一个可调用的表达式，其返回结果是一个能用作条件的值

一元谓词：接受单一参数的谓词

二元谓词：接受两个参数的谓词

#### 2.stable_sort(稳定排序算法)

stable_sort(b, e, func);

#### 3.排序算法的稳定性

排序后相同元素还维持原有的字典序位置，就是稳定的

即原有A1 = A2，A1在A2左边，排序后，A1任然在A2左边，这就是稳定

#### 4.find_if(b, e, func)

返回迭代器范围内，第一个使谓词返回true的元素

### 10.3.2 lambda表达式（Cpp11）

也称匿名函数

语法：

```
[捕获列表] (参数列表) -> 返回值类型 { 函数体 }
```

#### 1.捕获列表含义

捕获列表：**捕获lambda表达式所在函数的局部变量**，使得可以在匿名函数中使用外部变量

注意：函数内static变量或在函数外声明的如标准库cout等不需要捕获就可使用

#### 2.将lambda表达式作右值

可以将一个lambda表达式赋值给一个变量，此时，这个变量是一个函数

```cpp
auto func = []() { return 10; };
cout << func() << endl;
```

#### 3.for_each(b, e, func)

for_each遍历迭代器范围内所有元素，并对每个元素执行func操作

```cpp
vector<int> vec(10, 10);
for_each(vec.begin(), vec.end(), [](const int& num) {
	cout << num << " ";
});
```

### 10.3.3 lambda的捕获和返回

[C++11 lambda表达式精讲 (biancheng.net)](http://c.biancheng.net/view/3741.html)

定义lambda表达式时，其实编译器生成了一个类，这个类包含了所有捕获对象的数据成员，这些数据成员在lambda对象创建时被初始化

#### 1.lambda捕获列表

p352

注意：**当使用混合捕获列表时，显式捕获的变量必须使用与隐式捕获不同的方式**

### 10.3.4 标准库bind函数

> 通常我们可以将bind函数看作一个通用的函数适配器，它接受一个可调用对象，生成一个新的可调用对象来“适应”原对象的参数列表。bind可以根据当前已有的可调用对象，构造出一个新的可调用对象，有了bind，我们可以实现“动态生成新的函数”的功能。简而言之，就是可以通过bind函数修改原函数并生成一个可以被调用的对象，类似于函数的重载，但是我们又不需要去重新写一个函数，用bind函数就可以实现。

#### 1.语法

```cpp
bind(func, args_list);
```

需要引用functional头文件

```cpp
#include <iostream>
#include <iomanip>
#include <time.h>
#include <string>
#include <algorithm>
#include <vector>
#include <functional>

using namespace std;
using namespace placeholders;

int func(int numA, int numB, int numC, int numD) {
	cout << numA << endl;
	cout << numB << endl;
	cout << numC << endl;
	cout << numD << endl;
	return 0;
}

int main() {
	int x = 10;
	int y = 20;
	int z = 30;
	int k = 40;
    //将func函数的第一、三个参数绑定到x,z，另外两个参数由调用aBindFunc时传入
	auto aBindFunc = bind(func, x, placeholders::_1, z, placeholders::_2);
	aBindFunc(y, k);
	return 0;
}
/*
	output
	10
	20
	30
	40
*/
```

#### 2.placehoders名字（\_n）

名字\_n都定义在placehoders命名空间中，这是一个占位符，使得bind函数指定对象可以传入几个参数

```cpp
using namespace placeholders;

int func(int numA, int numB, int numC, int numD) {
	cout << numA << endl;
	cout << numB << endl;
	cout << numC << endl;
	cout << numD << endl;
	return 0;
}

int main() {
	int x = 10;
	int y = 20;
	int z = 30;
	int k = 40;
    //将func函数的第一、三个参数绑定到x,z，另外两个参数由调用aBindFunc时传入
	auto aBindFunc = bind(func, x, _1, z, _2);
	aBindFunc(y, k);
	return 0;
}
```

注意：**_n只是个占位符，与参数顺序无关**

也就是说，即使我换成(func, x, _2, z, _1)

```cpp
auto aBindFunc = bind(func, x, _2, z, _1);
aBindFunc(y, k);
```

