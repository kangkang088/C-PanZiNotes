# Computer System A Prgramer's Perspective

# 第一章

## 1.1 信息就是上下文

> hello.c 的表示方法说明了一个基本思想：系统中所有的信息—— 包括磁盘文件、内
> 存中的程序、内存中存放的用户数据以及网络上传送的数据，都是由一串比特表示的。区
> 分不同数据对象的唯一方法是我们读到这些数据对象时的上下文。比如，在不同的上下文
> 中，一个同样的字节序列可能表示一个整数、浮点数、字符串或者机器指令。

## 1.2 程序被其他程序翻译成不同的格式

### 1.2.1 预处理

> 预处理阶段。预处理器（CPP)根据以字符 #开头的命令，修改原始的 C 程序。比如hello.c 中第 1 行的 #include < stdio.h> 命令告诉预处理器读取系统头文件stdio.h 的内容，并把它直接插入程序文本中。结果就得到了另一个 C 程序，通常是以.i 作为文件扩展名。

### 1.2.2 编译

> 编译阶段。编译器(ccl)将文本文件 hello.i 翻译成文本文件 hello.sÿ 它包含一个汇编语言程序。该程序包含函数 main 的定义，如下所示：

### 1.2.3 汇编

> 汇编阶段。接下来，汇编器(as)将 hello.s 翻译成机器语言指令，把这些指令打包成一种叫做可重定位目标程序（relocatable object program)的格式，并将结果保存在目标文件 hello.o 中。hello.o 文件是一个二进制文件，它包含的 17 个字节是函数 main的指令编码。如果我们在文本编辑器中打开 hello.〇 文件，将看到一堆乱码。

### 1.2.4 链接

> 链接阶段。请注意，hello 程序调用了 printf 函数，它是每个 C 编译器都提供的标准 C 库中的一个函数。printf 函数存在于一个名为 printf .o 的单独的预编译好了的目标文件中，而这个文件必须以某种方式合并到我们的 hello.〇 程序中。链接器(Id)就负责处理这种合并。结果就得到 hello 文件，它是一个可执行目标文件(或者简称为可执行文件），可以被加载到内存中，由系统执行。

## 1.4.1 系统硬件组成

1. 总线

   > 贯穿整个系统的是一组电子管道，称作总线，它携带信息字节并负责在各个部件间传递。通常总线被设计成传送定长的字节块，也就是字（word)。字中的字节数（即字长）是一个基本的系统参数，各个系统中都不尽相同。现在的大多数机器字长要么是 4 个字节（32位）， 要么是 8 个字节(64 位）。

2. IO设备

   > 每个 I/O 设备都通过一个控制 器或适配器与 I/O 总线相连。控制器和适配器之间的区别主要在于它们的封装方式。控制器是 I/O 设备本身或者系统的主印制电路板（通常称作主板)上的芯片组。而适配器则是一块插在主板插槽上的卡。无论如何，它们的功能都是在 I/O 总线和 I/O 设备之间传递信息。

3. 主存

   > 主存是由一组动态随机存取存储器(DRAM)芯片组成

4. 处理器

5. 