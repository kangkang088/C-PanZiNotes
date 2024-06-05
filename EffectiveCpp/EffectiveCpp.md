# EffectiveCpp

## 1.视C++为一个语言联邦

可以视C++为四个部分
（1）C

（2）面向对象Cpp

（3）模板Cpp

（4）STL

> C++并不是一个带有一组守则的一体语言；它是从四个次语言组成的联邦政府，每个次语言都有自己的规约。记住这四个次语言你就会发现Cpp容易了解得多

## 2.尽量以const，enum，inline替换#define

（1）#define是定义宏的命令，所定义的宏在编译前就被预处理了，且可能没有进入符号表，当声明的常量出错时，可能提示的是所定义的数字，而不是这个宏，导致对此错误浪费很多追踪的时间。可以用const定义常量解决。

```cpp
#define ASPECT_RATIO 1.635	//宏定义
const double AspectRatio = 1.635;	//const常量
```

（2）常量指针为了保证不能改变指针本身和指针所指向值，需要写两次const

```cpp
const char* const authorName = "Scott Meyers"; 	//char*
const std::string authorName = "Scott Meyers";	//可用string代替char*
```

(3)声明类专属常量时，加上const的同时，也需要加上static，以确保只有一份常量

```cpp
class GamePlayer {
private:
	static const int NumTurns = 5;	//常量声明式
	int scores[NumTurns];			//使用该常量
	...
};
```

(4)无法使用#define定义一个class专属常量，因为#define不重视作用域，它被定义后，之后的编译过程都将有效（除非被#undef）

(5)