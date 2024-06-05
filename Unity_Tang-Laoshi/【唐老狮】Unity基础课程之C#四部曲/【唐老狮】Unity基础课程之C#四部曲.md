# 【唐老狮】Unity基础课程之C#四部曲

笔记整理者：盘子ssa，QQ（2426966358），2022年12月23日

# 【唐老狮】Unity基础课程之C#入门

# 主要学习内容

C#基础语法
环境搭建、变量、类型转换、运算符条件分支语句、循环语句

# 任务8：注释

1. 两杠注释：用于注释一行信息
2. 星号注释：用于注释多行信息
3. 三杠注释：用于注释类、命名空间等等

# 任务10：控制台输入输出语句和学习建议

## 作业

### 第一题

1.请简单描述Console.Write("")和Console.WriteLine("")的区别，简单描述Console.ReadKey()和Console.ReadLine()的区别。

> Console.Write()输出不换行，WriteLine输出换行
>
> ReadKey只读取一个字符，ReadLine读取一行字符

### 第二题

⒉.请用户输入用户名、年龄、班级

```C#
static void Main(String[] argc)
{
    Console.WriteLine("请输入用户名:");
    Console.ReadLine();

    Console.WriteLine("请输入年龄:");
    Console.ReadLine();

    Console.WriteLine("请输入班级:");
    Console.ReadLine();
}
```

### 第三题

3.问用户喜欢什么运动，不管用户输入什么，你都回答:“哈哈，好巧，我也喜欢这个运动”

```C#
Console.WriteLine("你喜欢什么运动:");
Console.ReadLine();
Console.WriteLine("哈哈，好巧，我也喜欢这个运动");
```

### 第四题

在控制台上输出如下10*10的空心星型方阵

```C#
for (int i = 0; i < 10; ++i)
{
    Console.Write("*");
}
Console.WriteLine();
for (int i = 0; i < 8; ++i)
{
    Console.WriteLine("*        *");
}
for (int i = 0; i < 10; ++i)
{
    Console.Write("*");
}
```

# 任务12：变量知识点

## C#常用数据类型

C#拥有13种基本数据类型（string是引用类型）

有符号整形：sbyte，int，short，long

无符号整形：byte，uint，ushort，ulong

浮点数类型：float（8位有效数字），double（17位有效数字），decimal（28位有效数字）

其他类型：bool，char，stirng

> 为了区分double，float，decimal
>
> float需要在小数后+f，decimal需要+m，整数不需要

## 作业

### 第一题

下面代码的输出结果是?

```C#
double num = 36.6;
Console.WriteLine("num");
```

> num

### 第二题

声明float类型变量时，为何要在数字后面加f?

> 因为C#中，浮点数默认为double类型，需要加上f来辨别是否是float类型

### 第三题

请定义一系列变量来存储你的名字、年龄、性别、身高、体重、家庭住址等，并打印出来。

```C#
string myName = "Panzi";
int age = 22;
bool gender = false;
float height = 166;
string Address = "Hunan";
Console.WriteLine(myName);
Console.WriteLine(age);
Console.WriteLine(gender);
Console.WriteLine(height);
Console.WriteLine(Address);
```

### 第四题

小明的数学考试成绩是80，语文的考试成绩是78，英语的考试成绩是98，请用变量描述并打印

```C#
int mathScore = 80;
int chineseScore = 78;
int englishScore = 98;
Console.WriteLine(mathScore);
Console.WriteLine(chineseScore);
Console.WriteLine(englishScore);
```

# 任务14：变量的本质知识点

## 作业

### 第一题

请默写出常用的14个变量类型,以及他们所占用的内存空间。

> sbyte：1
>
> int：4
>
> short：2
>
> long：8
>
> byte：1
>
> uint：4
>
> ushort：2
>
> ulong：8
>
> float：4
>
> double：8
>
> decimal：16
>
> bool：1
>
> char：2
>
> string：string.Count()

### 第二题

请将2进制11000111、001101、01010101转为10进制，写出计算过程

### 第三题

请将10进制99、1024、78937转为2进制，写出计算过程

# 任务16：变量的命名规范知识点

```C#
#region 知识点一：必须遵守的规则
//1.不能重名
//2.不能以数字开头
//3.不能使用程序关键字命名
//4.不能有特殊符号（下划线除外）

//建议的命名规则：变量名要有含义——>用英文（拼音）表示变量的作用
//非常不建议的命名规则：用汉字命名

#endregion

#region 知识点二：常用命名规则
//驼峰命名法——首字母小写，之后单词首字母大写（变量）
string myName = "唐老狮";
string yourName = "你的名字";
string yourMotherName = "";

//帕斯卡命名法——所有单词首字母都大写（函数、类）
string MyName = "dskafj";

//潜在知识点——C#中对大小写是敏感的 是区分的
#endregion
```

# 任务22：隐式转换知识点

1. 相同类型之间大范围可以装小范围
2. 无符号可以转换为有符号，但是有符号不可以转换为无符号
3. 整数可以转换为浮点数
4. float和double不能转换为decimal

基本规则：隐式转换，小的不能转大的，少的不能转多的，父不能转子

# 任务24：显示转换知识点

## 知识点一 括号强转

作用：一般情况下 将高精度的类型强制转换为低精度

语法： 变量类型 变量名 = (变量类型)变量；

注意： 精度问题 范围问题

## 知识点二 Parse法

作用：把字符串类型转换为对应的类型

语法： 变量类型.Parse("字符串");

注意： 字符串必须能够转换成对应类型 否则报错。浮点数强转整数不会四舍五入

```C#
string str2 = "123";
int i4 = int.Parse("123");
```

## 知识点三 Convert法

作用：更准确的将 各个类型之间进行相互转换；

语法： Convert.To目标类型(变量或常量)

注意： 填写的变量或常量必须正确 否则出错。

```C#
int a = Convert.ToInt32("12");
Console.WriteLine(a);
```

精度更准确

精度比括号强转好一点，会四舍五入

```C#
a = Convert.ToInt32(1.45845f);
Console.WriteLine(a);
```

每一个类型都存在对应的 Convert中的方法：

```C#
sbyte sb5 = Convert.ToSByte("1");
short s5 = Convert.ToInt16("1");
int i5 = Convert.ToInt32("1");
long l5 = Convert.ToInt64("1");

byte b6 = Convert.ToByte("1");
ushort us5 = Convert.ToUInt16("1");
uint ui5 = Convert.ToUInt32("1");
ulong ul5 = Convert.ToUInt64("1");

float f5 = Convert.ToSingle("13.2");
double d5 = Convert.ToDouble("13.2");
decimal de5 = Convert.ToDecimal("13.2");

bool bo5 = Convert.ToBoolean("true");
char c5 = Convert.ToChar("A");

string str5 = Convert.ToString(123123);
```

## 知识点四 其它类型转string

作用：拼接打印

语法：变量.ToString();

```C#
string str6 = 1.ToString();
```

# 任务53：必备知识1：控制台相关

## 知识点一 复习 输入输出

### 输出

```C#
Console.WriteLine();//自带换行
Console.Write();//不换行
```

### 输入

```C#
Console.ReadLine();//读入一行
Console.ReadKey();//读入一个字符
Console.ReadKey(true).KeyChar;//读入一个字符，但是不现实在控制台
```

## 知识点二 控制台其他方法

### 1.清空方法

```C#
Console.Clear();
```

### 2.设置控制台大小

注意：

1. 先设置窗口大小，再设置缓冲区大小
2. 缓冲区的大小不能小于窗口的大小
3. 窗口的大小不能大于控制台的最大尺寸

设置窗口大小（固定）

```C#
Console.SetWindowSize(100, 50);
```

设置缓冲区大小（可打印区域大小）

```
Console.SetBufferSize(100, 50);
```

### 3.设置光标的位置

控制台是左上角为原点0 0 右侧是X轴正方向 下方是Y轴正方向 它是一个平面二维坐标系。

注意：

1. 边界问题：只能在缓冲区大小内设置，不然会报错
2. 横纵距离单位不同 1y = 2x 视觉上的

设置光标的位置：意思是，如果后面有输出，将从此处开始

```C#
Console.SetCursorPosition(10, 5);
```

### 4.设置颜色相关

一旦设置，后面将全是此颜色

文字颜色设置

```C#
Console.ForegroundColor = ConsoleColor.Red;
```

背景颜色设置

```C#
Console.BackgroundColor = ConsoleColor.White;
//重置背景颜色过后 需要Clear一次 才能把整个背景颜色改变
Console.Clear();
```

### 5.光标显隐

```C#
Console.CursorVisible = false;
```

### 6.关闭控制台

```C#
Environment.Exit(0);
```

### 7.获取缓冲区大小

高

```C#
Console.BufferHeight;
```

宽

```C#
Console.BufferWidth;
```

## 作业

通过W,A,S,D键在控制台中控制一个黄色方块上下左右移动注意:边界问题
知识点: while，switch，输入输出等等

```C#
static void Main(string[] args)
{
    int x = 0;
    int y = 0;

    Console.BackgroundColor = ConsoleColor.Red;
    Console.Clear();
    Console.ForegroundColor = ConsoleColor.Yellow;

    Console.SetWindowSize(50, 30);
    Console.SetBufferSize(50, 30);
    Console.CursorVisible = false;
    char symbol = '■';

    int height = Console.BufferHeight - 1;
    int width = Console.BufferWidth - 2;
    while (true)
    {
        Console.SetCursorPosition(x, y);
        Console.Write(symbol);

        char input = Console.ReadKey(true).KeyChar;

        Console.SetCursorPosition(x, y);
        Console.Write("  ");
        switch (input)
        {
            case 'w':
            case 'W':
                y -= 1;
                break;
            case 'a':
            case 'A':
                x -= 2;
                break;
            case 's':
            case 'S':
                y += 1;
                break;
            case 'd':
            case 'D':
                x += 2;
                break;
        }
        if (x < 0)
        {
            x = 0;
        }
        if (y < 0)
        {
            y = 0;
        }
        if (x >= width)
        {
            x = width;
        }
        if (y >= height)
        {
            y = height;
        }

    }

}
```

# 任务55：必备知识2：随机数

## 知识点一 产生随机数对象

语法：Random 随机数变量名 = new Random();

```C#
Random r = new Random();
```

## 知识点二 生成随机数

```C#
int i = r.Next(); //生成一个非负数的随机数
Console.WriteLine(i);

i = r.Next(100); // 生成一个 0~99的随机数 左边始终是0 左包含  右边是100 右不包含
Console.WriteLine(i);

i = r.Next(5, 100); // 生成一个 5到99的随机数 左包含 右不包含
Console.WriteLine(i);
```

# -----------------------

# 【唐老狮】Unity基础课程之C#基础

# 任务5：数组 知识点

## 知识点一 基本概念

数组是存储一组相同类型数据的集合，数组分为 一维、多维、交错数组

一般情况 一维数组 就简称为 数组

## 知识点二 数组的声明

5种方式，大同小异

> 其实，就是变成了在堆区开辟内存，其他和Cpp一致，只不过声明标识符变成了int[]

```C#
//变量类型[] 数组名;
//变量类型 可以是我们学过的 或者 没学过的所有变量类型
int[] arr1;	//只是声明了一个数组 但是并没有分配内存空间

//变量类型[] 数组名 = new 变量类型[数组的长度];
int[] arr2 = new int[5]; //这种方式 相当于开了5个房间 但是房间里面的int值 默认为0

//变量类型[] 数组名 = new 变量类型[数组的长度] { 内容1, 内容2, 内容3, .......};
int[] arr3 = new int[5] { 1, 2, 3, 4, 5 };

//变量类型[] 数组名 = new 变量类型[] { 内容1, 内容2, 内容3, .......};
int[] arr4 = new int[] { 1, 2, 3, 4, 5, 6, 7, 8, 9 }; //后面的内容就决定了 数组的长度 “房间数”

//变量类型[] 数组名 = { 内容1, 内容2, 内容3, .......};
int[] arr5 = { 1, 3, 4, 5, 6 };//后面的内容就决定了 数组的长度 “房间数”

bool[] arr6 = { true, false };
```

## 知识点三 数组的使用

### 1.数组的长度

```C#
Console.WriteLine(array.Length);
```

### 2.获取数组中的元素

下标获取，与Cpp一致，下标[0, Length)，不能越界。

```C#
int[] array = {0, 1, 2, 3, 4};
Console.WriteLine(array[0]);
Console.WriteLine(array[2]);
Console.WriteLine(array[4]);
```

### 3.修改数组中的元素

直接修改，与Cpp一致

```C#
array[0] = 99;
```

### 4.遍历数组（通过循环快速获取数组中的每一个元素）

```C#
for (int i = 0; i < array.Length; i++)
{
    Console.WriteLine(array[i]);
}
```

### 5.增加数组的元素

数组初始化以后 是不能够 **直接添加新的元素的**，只能通过重新赋值的方式。

与Cpp一致

```C#
int[] array2 = new int[5];
//重新赋值
for (int i = 0; i < array.Length; i++)
{
    array2[i] = array[i];
}
array = array2;
for (int i = 0; i < array.Length; i++)
{
    Console.WriteLine(array[i]);
}
array[4] = 999;
```

### 6.删除数组的元素

数组初始化以后 是不能够 **直接删除元素的**，也是只能通过重新赋值的方式。

与Cpp一致

```C#
int[] array3 = new int[5];
for (int i = 0; i < array3.Length; i++)
{
    array3[i] = array[i];
}
array = array3;
Console.WriteLine(array.Length);
```

### 7.查找数组中的元素

对于无序数组，只能通过遍历一个个访问数组元素。

```C#
int a = 3;

for (int i = 0; i < array.Length; i++)
{
    if (a == array[i])
    {
        Console.WriteLine("和a相等的元素在{0}索引位置", i);
        break;
    }
}
```

## 总结

1. 概念：同一变量类型的数据集合
2. 一定要掌握的知识：声明，遍历，增删查改
3. 所有的变量类型都可以申明为 数组
4. 她是用来批量存储游戏中的同一类型对象的 容器 比如 所有的怪物 所有玩家

## 作业

### 第一题

请创建—个一维数组并赋值，让其值与下标一样，长度为100

```C#
int[] array = new int[100];
for (int i = 0; i < array.Length; ++i) {
    array[i] = i;
    Console.Write(array[i] + " ");
}
```

### 第二题

创建另一个数组B，让数组A中的每个元素的值乘以2存入到数组B中

```C#
int[] arrayA = new int[100];
for (int i = 0; i < arrayA.Length; ++i) {
    arrayA[i] = i;
}

int[] arrayB = new int[100];
for (int i = 0; i < arrayB.Length; ++i) {
    arrayB[i] = arrayA[i] * 2;
    Console.Write(arrayB[i] + " ");
}
```

### 第三题

随机 (0~100）生成1个长度为10的整数数组

```C#
Random random = new Random();
int[] array = new int[10];
for (int i = 0; i < array.Length; ++i) {
    array[i] = random.Next(0, 101);
    Console.Write(array[i] + " ");
}
```

### 第四题

从一个整数数组中找出最大值、最小值、总合、平均值(可以使用随机数1~100)

```C#
int maxNum = 0;
int minNum = 101;
int sum = 0;
int average = 0;

Random random = new Random();
int[] array = new int[10];
for (int i = 0; i < array.Length; ++i) {
    array[i] = random.Next(0, 101);
    Console.Write(array[i] + " ");
	if (maxNum < array[i]) {
        maxNum = array[i];
    }
    if (minNum > array[i]) {
        minNum = array[i];
    }
    sum += array[i];
}
average = sum / array.Length;
Console.WriteLine();
Console.Write($"maxNum:{maxNum}, minNum:{minNum}, sum:{sum}, average:{average}");
```

### 第五题

交换数组中的第一个和最后一个、第二个和倒数第二个，依次类推，把敦组进行反转并打印

```C#
Random random = new Random();
int[] array = new int[10];
for (int i = 0; i < array.Length; ++i) {
    array[i] = random.Next(0, 101);
    Console.Write(array[i] + " ");
}
Console.WriteLine();
int left = 0;
int right = array.Length - 1;
while (left < right) {
    int temp = array[left];
    array[left] = array[right];
    array[right] = temp;
    ++left;
    --right;
}
for (int i = 0; i < array.Length; ++i) {
    Console.Write(array[i] + " ");
}
```

### 第六题

将一个整数数组的每一个元素进行如下的处理:如果元素是正数则将这个位置的元素值加1;如果元素是负数则将这个位置的元素值减1;如果元素是0，则不变.

### 第七题

定义一个有10个元素的数组，使用for循环，输入10名同学的数学成绩，将成绩依次存入数组，然后分别求出最高分和最低分，并且求出10名同学的数学平均成绩。

### 第八题

请声明一个string类型的数组(长度为25)(该数组中存储着符号)，通过遍历数组的方式取出其中存储的符号打印出以下效果

![image-20221225103640806](【唐老狮】Unity基础课程之C#四部曲.assets/image-20221225103640806.png)

```C#
string[] strArray = new string[25];
for (int j = 0; j < strArray.Length; ++j)
{
    strArray[j] = j % 2 == 0 ? "□" : "■";
}
int i = 0;
while (i < strArray.Length)
{
    Console.Write(strArray[i]);
    ++i;
    if (i % 5 == 0)
    {
        Console.WriteLine();
    }
}
```

# 任务8：二维数组 知识点

## 知识点一 基本概念

二维数组 是使用两个下标(索引)来确定元素的数组

两个下标可以理解成 行标 和 列标

比如矩阵

1 2 3

4 5 6
可以用二维数组 int[2, 3] 表示
好比 两行 三列的数据集合

> 其实是一个n * m的矩阵
>
> 可扩展为多维数组

## 知识点二 二维数组的声明

```C#
//变量类型[,] 二维数组变量名;
int[,] arr; //申明过后 会在后面进行初始化

//变量类型[,] 二维数组变量名 = new 变量类型[行,列];
int[,] arr2 = new int[3, 3];

//变量类型[,] 二维数组变量名 = new 变量类型[行,列]{ {0行内容1, 0行内容2, 0行内容3.......}, {1行内容1, 1行内容2, 1行内容3.......}.... };
int[,] arr3 = new int[3, 3] { { 1, 2, 3 }, 
                             { 4, 5, 6 }, 
                             { 7, 8, 9 } };

//变量类型[,] 二维数组变量名 = new 变量类型[,]{ {0行内容1, 0行内容2, 0行内容3.......}, {1行内容1, 1行内容2, 1行内容3.......}.... };
int[,] arr4 = new int[,] { { 1, 2, 3 },
                          { 4, 5, 6 },
                          { 7, 8, 9 } };

//变量类型[,] 二维数组变量名 = { {0行内容1, 0行内容2, 0行内容3.......}, {1行内容1, 1行内容2, 1行内容3.......}.... };
int[,] arr5 = { { 1, 2, 3 },
               { 4, 5, 6 },
               { 7, 8, 9 } };
```

## 知识点三 二维数组的使用

### 1.二维数组的长度

```C#
Console.WriteLine(array.GetLength(0));//0行数
Console.WriteLine(array.GetLength(1));//1列数
array.Legnth; //2 * 3, 6
```

### 2.获取二维数组中的元素

```C#
// 注意：第一个元素的索引是0 最后一个元素的索引 肯定是长度-1
Console.WriteLine(array[0, 1]);
Console.WriteLine(array[1, 2]);
```

### 3.修改二维数组中的元素

```C#
array[0, 0] = 99;
Console.WriteLine(array[0, 0]);
Console.WriteLine("**********");
```

### 4.遍历二维数组

```C#
for (int i = 0; i < array.GetLength(0); i++)
{
    for (int j = 0; j < array.GetLength(1); j++)
    {
        //i 行 0 1
        //j 列 0 1 2
        Console.WriteLine(array[i, j]);
        //0,0  0,1  0,2
        //1,0  1,1  1,2
    }
}
```

## 总结

1. 概念：同一变量类型的 行列数据集合
2. 一定要掌握的内容：申明，遍历，增删查改
3. 所有的变量类型都可以申明为 二维数组
4. 游戏中一般用来存储 矩阵，再控制台小游戏中可以用二维数组 来表示地图格子

# 任务10：交错数组 知识点

## 知识点一 基本概念

交错数组 是 数组的数组，每个维度的数量可以不同

注意：二维数组的每行的列数相同，交错数组每行的列数可能不同

## 知识点二 数组的声明

```C#
//变量类型[][] 交错数组名;
int[][] arr1;

//变量类型[][] 交错数组名 = new 变量类型[行数][];
int[][] arr2 = new int[3][];

//变量类型[][] 交错数组名 = new 变量类型[行数][]{ 一维数组1, 一维数组2,........ };
int[][] arr3 = new int[3][] { new int[] { 1, 2, 3 },
                             new int[] { 1, 2 },
                             new int[] { 1 }};

//变量类型[][] 交错数组名 = new 变量类型[][]{ 一维数组1, 一维数组2,........ };
int[][] arr4 = new int[][] { new int[] { 1, 2, 3 },
                            new int[] { 1, 2 },
                            new int[] { 1 }};

//变量类型[][] 交错数组名 = { 一维数组1, 一维数组2,........ };
int[][] arr5 = { new int[] { 1, 2, 3 },
                new int[] { 1, 2 },
                new int[] { 1 }};
```

## 知识点三 数组的使用

### 1.数组的长度

```C#
//行
Console.WriteLine(array.GetLength(0));
//得到某一行的列数
Console.WriteLine(array[i].Length);
```

### 2.获取交错数组中的元素

```C#
// 注意：不要越界
Console.WriteLine(array[0][1]);
```

### 3.修改交错数组中的元素

```C#
array[0][1] = 99;
Console.WriteLine(array[0][1]);
```

### 4.遍历交错数组

```C#
for (int i = 0; i < array.GetLength(0); i++)
{
    for (int j = 0; j < array[i].Length; j++)
    {
        Console.Write(array[i][j] + " ");
    }
    Console.WriteLine();
}
```

## 总结

1. 概念：交错数组 可以存储同一类型的m行不确定列的数据
1. 一定要掌握的内容：声明、遍历、增删查改
1. 所有的变量类型都可以申明为 交错数组
1. 一般交错数组很少使用 了解即可

# 任务11：值和引用类型 使用和存储上的区别 知识点

## 知识点一 变量类型的复习

```C#
//无符号整形
byte b = 1;
ushort us = 1;
uint ui = 1;
ulong ul = 1;
////有符号整形
sbyte sb = 1;
short s = 1;
int i = 1;
long l = 1;
//浮点数
float f = 1f;
double d = 1.1;
decimal de = 1.1m;
//特殊类型
bool bo = true;
char c = 'A';
string str = "strs";
//复杂数据类型
// enum 枚举 
// 数组 (一维，二维，交错)
```

### 类型细分

把以上 学过的 变量类型 分成 值类型和引用类型

引用类型: string, 数组, 类（未学习）

值类型: 其它、结构体

## 知识点二 值类型和引用类型的区别

### 1.使用上的区别

值类型 在相互赋值时 把内容拷贝给了对方  它变我不变

引用类型的相互赋值 是 让两者指向同一个值  它变我也变

### 2.为什么有以上区别

值类型 和 引用类型 存储在的 内存区域 是不同的 存储方式是不同的,所以就造成了 他们在使用上的区别。

值类型存储在 栈空间  —— 系统分配，自动回收，小而快

引用类型 存储在 堆空间 —— 手动申请和释放，大而慢

# 任务13：特殊的引用类型string 知识点

## 知识点二 string的它变我不变

因为string是引用类型 按理说 应该是它变我也变

string非常的特殊 它具备 值类型的特征 它变我不变

string 虽然方便 但是有一个小缺点 就是频繁的 改变string 重新赋值

会产生内存垃圾，优化替代方案 我们会在 C#核心当中进行讲解

# 任务17：ref和out 知识点

## 知识点一 学习ref和out的原因

它们可以解决 在函数内部改变外部传入的内容 里面变了 外面也要变

> 其实就是传递引用

## 知识点二 ref和out的使用

```C#
//函数参数的修饰符
//当传入的值类型参数在内部修改时 或者引用类型参数在内部重新申明时
//外部的值会发生变化

//ref
static void ChangeValueRef(ref int value)
{
    //out传入的变量必须在内部赋值 ref不用
    value = 3;
}

static void ChangeArrayRef(ref int[] arr )
{
    arr = new int[] { 100, 200, 300 };
}

//out
static void ChangeValueOut(out int value)
{
    //out传入的变量必须在内部赋值 ref不用
    value = 99;
}

static void ChangeArrayOut(out int[] arr)
{
    arr = new int[] { 999, 888, 777 };
}

static void Main(string[] args)
{
    Console.WriteLine("ref和out");
    int a = 1;
    ChangeValueRef(ref a);
    ChangeValueOut(out a);
}

```

## 知识点三 ref和out的区别

相同点：

1. 都是为了引用传递
2. 实参必须都填写对应的修饰符

不同点：

1. ref传入的变量必须初始化，out不用
2. out传入的变量必须在内部赋值，ref不用

ref传入的变量必须初始化 但是在内部 可改可不改

out传入的变量不用初始化 但是在内部 必须修改该值（必须赋值）

## 作业



# 任务19：变长参数和参数默认值 知识点

## 知识点二 变长参数关键词

变长参数关键字 params

```C#
static int Sum(params int[] arr)
{
    int sum = 0;
    for (int i = 0; i < arr.Length; i++)
    {
        sum += arr[i];
    }
    return sum;
}
static void Main(string[] args)
{
    Sum();
    Sum(1,2,3,4,5,6,7,8,1,22,456,123,1);
}
```

params int[] 意味着可以传入n个int参数 n可以等于0  传入的参数会存在arr数组中

注意：

1. params关键字后面必为数组
2. 数组的类型可以是任意的类型
3. 函数参数可以有别的参数和一个params关键字修饰的参数
4. 函数参数中只能最多出现一个params关键字 并且一定是在最后一组参数 前面可以有n个其它参数

## 知识点三 参数默认值

有参数默认值的参数 一般称为可选参数

作用是 当调用函数时可以不传入参数，不传就会使用默认值作为参数的值

```C#
static void Speak(string str = "我没什么话可说")
{
    Console.WriteLine(str);
}
```

注意：

1. 支持多参数默认值 每个参数都可以有默认值
2. 如果要混用可选参数，必须写在普通参数后面
3. params参数还是只能在最后一个

```C#
static void Speak2(string a, string test, string name = "唐老狮", string str = "我没什么话可说", params string[] strArr)
{

}
```

## 总结

1. 变长参数关键字 params
   1. 作用： 可以传入n个同类型参数   n可以是0
   2. params后面必须是数组 意味着只能是同一类型的可变参数
   3. 变长参数只能有一个
   4. 必须在所有参数最后写变长参数 
2. 参数默认值（可选参数）
   1. 作用：可以给参数默认值 使用时可以不传参 不传用默认的 传了用传的
   2. 可选参数可以有多个
   3. 正常参数比写在可选参数前面，可选参数只能写在所有参数的后面

# 任务21：函数重载 知识点

## 知识点一 基本概念

在同一语句块(class或者struct)中，函数（方法）名相同或者参数的数量相同，但参数的类型或顺序不同

作用：

1. 命名一组功能相似的函数，减少函数名的数量，避免命名空间的污染
2. 提升程序可读性

注意：

1. 重载和返回值类型无关，只和参数类型，个数，顺序有关
2. 调用时程序会自己根据传入的参数类型判断使用哪一个重载

## 知识点二 实例

注意：

ref，out可以和其他参数作重载，但是两者不可以互相重载

```C#
static float CalcSum(float f, int a)
{
    return f + a;
}

//ref 和 out

// ref和out 可以理解成 他们也是一种变量类型 所以可以用在重载中 但是 ref和out不能同时修饰
static float CalcSum(ref float f, int a)
{
    return f + a;
}
//ref和out不能互相作重载条件，但是可以和其他类型
//错误
//static float CalcSum(out float f, int a)
//{
//    f = 10;
//    return f + a;
//}
```

## 总结

概念：同一个语句块中，函数名相同，参数数量、类型、顺序不同的函数 就称为我们的重载函数。

注意：和返回值无关，ref和out不能互相作为重载条件，变长参数可以。

作用：一般用来处理不同参数的同一类型的逻辑处理。

# 任务23：递归函数 知识点

## 知识点一 基本概念

递归函数 就是 让函数自己调用自己

一个正确的递归函数

1. 必须有结束调用的条件	
2. 用于条件判断的 这个条件 必须改变 能够达到停止的目的

## 作业

### 第五题

不允许使用循环语句、条件语句，在控制台中打印出1-200这200个数（提示：递归+短路）

```C#
static bool Func(int num)
{
    Console.Write(num + " ");
    return num == 200 || Func(num + 1);
}
```

# 任务25：结构体 知识点

## 知识点一 基本概念

结构体 是一种自定义变量类型  类似枚举需要自己定义

它是数据和函数的集合

在结构体中 可以申明各种变量和方法

作用：用来表现存在关系的数据集合 比如用结构体表现学生 动物 人类等等

## 知识点二 基本语法

1. 结构体一般写在 namespace语句块中
2. 结构体关键字 struct

```C#
struct 自定义结构体名
{
    // 第一部分
    // 变量

    // 第二部分
    // 构造函数(可选)

    // 第三部分 
    // 函数
}
```

注意：结构体名的规范是帕斯卡命名法（大驼峰）

## 知识点三 实例

```C#
	struct Student
    {
        #region 知识点五 访问修饰符
        //修饰结构体中变量和方法 是否能被外部使用
        //public 公共的 可以被外部访问
        //private 私有的 只能在内容使用
        //默认不写 为private
        //protected
        //internal
        //protected internal
        #endregion


        //变量
        //结构体申明的变量 不能直接初始化
        //变量类型 可以写任意类型 包括结构体 但是 不能是自己的结构体 可以是其它的
        //Student s;// 不能是自己的结构体
        //年龄
        public int age;
        //性别
        public bool sex;
        //学号
        public int number;
        //姓名
        public string name;

        //构造函数
        #region 知识点六 结构体的构造函数
        //基本概念
        //1.没有返回值
        //2.函数名必须和结构体名相同
        //3.必须有参数
        //4.如果申明了构造函数 那么必须在其中对所有变量数据初始化

        //构造函数 一般是用于在外部方便初始化的
        public Student(int age, bool sex, int number, string name)
        {
            //新的关键字 this 
            //代表自己
            this.age = age;
            this.sex = sex;
            this.number = number;
            this.name = name;
        }

        #endregion

        //函数方法
        //表现这个数据结构的行为

        //注意 在结构体中的方法 目前不需要加static关键字 
        public void Speak()
        {
            //函数中可以直接使用结构体内部申明的变量
            Console.WriteLine("我的名字是{0},我今年{1}岁", name, age);
        }
        //可以根据需求 写无数个函数的
    }
```

## 知识点四 结构体的使用

```C#
static void Main(string[] args)
{
    Console.WriteLine("结构体");

    #region 知识点四 结构体的使用
        //变量类型 变量名;
    Student s1;
    s1.age = 10;
    s1.sex = false;
    s1.number = 1;
    s1.name = "唐老狮";
    s1.Speak();

    Student s2 = new Student(18, true, 2, "小红");
    s2.Speak();
    #endregion
}
```

## 知识点五 访问修饰符

修饰结构体中变量和方法 是否能被外部使用

public 公共的 可以被外部访问

private 私有的 只能在内容使用

## 知识点六 结构体的构造函数

基本概念

1. 没有返回值
2. 函数名必须和结构体名相同
3. 必须有参数
4. 如果声明了构造函数，那么必须在其中对所有变量数据初始化

关键字this，可通过this.成员名，访问成员

```C#
public Student(int age, bool sex, int number, string name)
{
    //新的关键字 this 
    //代表自己
    this.age = age;
    this.sex = sex;
    this.number = number;
    this.name = name;
}
```

## 总结

1. 概念：结构体 struct 是变量和函数的集合 用来表示特定的数据集合

2. 访问修饰符： 

   public 和private 用来修饰变量和方法的

   public外部可以调用；private内部用 不写的话默认就是private

3. 在结构体中声明的变量，不能初始化 ，只能在外部或者在函数中赋值（初始化）

4. 在结构体中申明的函数，不用加static的

## 作业

### 第四题

```C#
struct PlayerInfo
{
    public string name;
    public E_Occupation occupation;

    public PlayerInfo(string name, E_Occupation occupation)
    {
        this.name = name;
        this.occupation = occupation;
    }

    public void Atk()
    {
        string o = "";
        string s = "";
        switch (occupation)
        {
            case E_Occupation.Warrior:
                o = "战士";
                s = "冲锋";
                //Console.WriteLine("战士{0}释放了冲锋");
                break;
            case E_Occupation.Hunter:
                o = "猎人";
                s = "假死";
                //Console.WriteLine("猎人{0}释放了假死");
                break;
            case E_Occupation.Master:
                o = "法师";
                s = "奥术冲击";
                //Console.WriteLine("法师0}释放了奥数冲击");
                break;
            default:
                break;
        }
        Console.WriteLine("{0}{1}释放了{2}", o, name, s);
    }
}
//职业
enum E_Occupation
{
    /// <summary>
    /// 战士
    /// </summary>
    Warrior,
    /// <summary>
    /// 猎人
    /// </summary>
    Hunter,
    /// <summary>
    /// 法师
    /// </summary>
    Master,
}

static void Main(String[] argc)
{
    Console.WriteLine("请输入你的姓名");
    string name = Console.ReadLine();
    Console.WriteLine("请输入职业(0战士 1猎人 2法师)");
    try
    {
        E_Occupation o = (E_Occupation)int.Parse(Console.ReadLine());
        //根据输入的内容初始化了一个玩家对象
        PlayerInfo info = new PlayerInfo(name, o);
        info.Atk();
    }
    catch
    {
        Console.WriteLine("请输入数字");
    }
}
```

# 任务27：冒泡排序 知识点

## 知识点一 排序的基本概念

排序是计算机内经常进行的一种操作，其目的是将一组“无序”的记录序列调整为“有序”的记录序列

## 知识点二 冒泡排序基本原理

两两相邻，不停比较，不停交换，比较n轮

## 知识点三 代码实现

```C#
//外面声明一个标识 来表示 该轮是否进行了交换
bool isSort = false;
//2.特使情况的优化
for (int m = 0; m < arr.Length; m++)
{
    //每一轮开始时 默认没有进行过交换
    isSort = false;
    // 尽一次循环 就需要比较一轮
    for (int n = 0; n < arr.Length - 1 - m; n++)
    {
        //如果 第n个数 比第n+1个数 大 他们就要交换位置
        if (arr[n] > arr[n + 1])
        {
            isSort = true;
            // 第二步 交换位置
            // 中间商不赚差价 
            int temp = arr[n];
            arr[n] = arr[n + 1];
            arr[n + 1] = temp;
        }
    }
    //当一轮结束过后 如果isSort这个标识 还是false
    //那就意味着 已经是最终的序列了 不需要再判断交换了
    if( !isSort )
    {
        break;
    }
}

for (int i = 0; i < arr.Length; i++)
{
    Console.WriteLine(arr[i]);
}
```

## 总结

基本概念：

两两相邻，不停比较，不停交换，比较n轮

套路写法：

两层循环，外层轮数，内层比较，两值比较，满足交换

优化：

比过不比，标记排序

# 实践小项目附加要求

1. 实现游戏内暂停场景，场景包括标题（游戏暂停），文字（继续游戏，回到主界面，退出游戏），实现和开始场景一样的选择效果，并且选择后按“j”可以跳转到对应场景。

# ------------------------

# 【唐老狮】Unity基础课程之C#核心

# 任务5：成员变量和访问修饰符 知识点

## 可以在定义成员时赋初始值

可以在定义成员时赋初始值，但是当拥有本身类型的成员时，不可以对该成员进行初始化，因为会造成无限循环调用。

## default(type)

default(type)可以返回这个类型的默认值，值类型中，数字一般为0，char为空字符，bool为false，引用类型为null。

# 任务9：构造、析构、垃圾回收 知识点

## 构造函数

类中是允许自己申明无参构造函数的，结构体是不允许

并且结构体的构造函数，必须初始化所有成员。

## 可以使用委托构造函数

也就是说，可以在使用一个构造函数时，使用this(args),调用其他构造函数

```C#
public Person(int age, string name):this(age + 10)
{
	Console.WriteLine("Person两个参数构造函数调用");
}
```

和Cpp不同，Cpp委托构造函数是使用类名的，C#是使用this。

## 析构函数

C#当中拥有自动垃圾回收机制，不需要我们收到回收堆区内存，所以，现阶段不需要析构函数。

我们也可以直接定义析构函数，知道垃圾回收时，才会调用此函数。

## 知识点四 垃圾回收机制

### 垃圾回收

垃圾回收，英文简写GC（Garbage Collector）

垃圾回收的过程是在遍历堆(Heap)上动态分配的所有对象

通过识别它们是否被引用来确定哪些对象是垃圾，哪些对象仍要被使用

所谓的垃圾就是没有被任何变量，对象引用的内容

垃圾就需要被回收释放

### 垃圾回收有很多种算法

比如

引用计数(Reference Counting)

标记清除(Mark Sweep)

标记整理(Mark Compact)

复制集合(Copy Collection)

### GC只负责堆(Heap)内存的垃圾回收

GC只负责堆(Heap)内存的垃圾回收

引用类型都是存在堆(Heap)中的，所以它的分配和释放都通过垃圾回收机制来管理

栈(Stack)上的内存是由系统自动管理的

值类型在栈(Stack)中分配内存的，他们有自己的生命周期，不用对他们进行管理，会自动分配和释放

### C#中内存回收机制的大概原理（分代算法）

0代内存     1代内存     2代内存

代的概念：代是垃圾回收机制使用的一种算法（分代算法）

新分配的对象都会被配置在第0代内存中

每次分配都可能会进行垃圾回收以释放内存(0代内存满时)

在一次内存回收过程开始时，垃圾回收器会认为堆中全是垃圾，会进行以下两步

1.标记对象 从根（静态字段、方法参数）开始检查引用对象，标记后为可达对象，未标记为不可达对象不可达对象就认为是垃圾

2.搬迁对象压缩堆  （挂起执行托管代码线程） 释放未标记的对象 搬迁可达对象 修改引用地址

大对象总被认为是第二代内存  目的是减少性能损耗，提高性能

不会对大对象进行搬迁压缩  85000字节（83kb）以上的对象为大对象

### 手动触发垃圾回收的方法 

一般情况下 我们不会频繁调用

都是在 Loading过场景时 才调用

```C#
GC.Collect();
```

# 任务11：成员属性 知识点

## 概念

本质是函数，用来包装对于字段的访问，使用时直接点出来（与字段一致）。

```C#
class A {
	private	string name;
	public string Name {
		get {
			return name;
		}
		
		set {
			name = val;
		}
	}
}
```

上下文关键字：val，在成员属性set当中，val作为传递的参数，用以接收外部传递进来的值。

## 知识点四 成员属性中 get和set前可以加访问修饰符

1. 默认不加 会使用属性声明时的访问权限
2. 加的访问修饰符要低于属性的访问权限
3. 不能让get和set的访问权限都低于属性的权限（应该是为了向上兼容，使得某一个的权限一定是和属性是一致的，以防属性的权限失去作用）

访问权限是指对于外部的开放权限：public->protected internal->protected->internal->private

## 知识点五 get和set可以只有一个

只有一个时  没必要在前面加访问修饰符

一般情况下 只会出现 只有 get的情况 基本不会出现只有set

## 知识点六 自动属性

作用：外部能得不能改的特征

```C#
public float Height
{
    //没有再get和set中写逻辑的需求或者想法
    get;
    private set;
}
```

如果类中有一个特征是只希望外部能得不能改的 又没什么特殊处理

那么可以直接使用自动属性

> 实际上，是编译器帮你定义了一个变量存储到了类中。

# 任务13：索引器 知识点

## 知识点一 索引器基本概念

让对象可以像数组一样通过索引访问其中元素，使程序看起来更直观，更容易编写。

本质其实也是函数，与成员属性差不多。

## 知识点二 索引器语法

```C#
//访问修饰符 返回值 this[参数类型 参数名, 参数类型 参数名.....]
//{
//      内部的写法和规则和索引器相同
//      get{}
//      set{}
//}
```

## 知识点五 索引器可以重载

重载规则与普通函数重载规则一致

# 任务15：静态成员 知识点

## 知识点一 静态成员基本概念

用static修饰的 成员变量、方法、属性等

静态成员的特点是：直接用类名点出使用

注意：静态成员不能通过类实例访问，必须使用类名点出来使用。

静态成员一开始就处于静态全局区。

## 知识点九 常量和静态变量

相同点：他们都可以通过类名点出使用

不同点：

1. const必须初始化，不能修改 static没有这个规则
2. const只能修饰变量、static可以修饰很多
3. const一定是写在访问修饰符后面的 ，static没有这个要求

# 任务17：静态类和静态构造函数 知识点

## 知识点一 静态类

用static修饰的类

特点：只能包含静态成员，不能被实例化

作用：

1. 将常用的静态成员写在静态类中 方便使用
2. 静态类不能被实例化，更能体现工具类的 唯一性

> 比如 Console就是一个静态类

## 知识点二 静态构造函数

在构造函数加上 static 修饰

特点：

1. 静态类和普通类都可以有
2. 不能使用访问修饰符
3. 不能有参数
4. 只会自动调用一次

作用：在静态构造函数中初始化 静态变量

在静态类中的静态构造函数，会在程序一运行就自动调用一次；

在普通类中的静态构造函数，会在第一个实例前自动调用一次。

# 任务19：拓展方法 知识点

## 知识点一 拓展方法基本概念

概念：为**现有非静态** 变量类型 添加 新方法

作用：

1. 提升程序拓展性
2. 不需要再对象中重新写方法
3. 不需要继承来添加方法
4. 为别人封装的类型写额外的方法

特点：

1. 一定是写在静态类中
2. 一定是个静态函数
3. 第一个参数为拓展目标（即调用者本身）
4. 第一个参数用this修饰

## 知识点二 基本语法

访问修饰符 static 返回值 函数名(this 拓展类名 参数名, 参数类型 参数名,参数类型 参数名....)

```C#
static class Tools
{
    //为int拓展了一个成员方法
    //成员方法 是需要 实例化对象后 才 能使用的
    //value 代表 使用该方法的 实例化对象
    public static void SpeakValue(this int value)
    {
        //拓展的方法 的逻辑
        Console.WriteLine("唐老狮为int拓展的方法" + value);
    }

    public static void SpeakStringInfo(this string str, string str2, string str3)
    {
        Console.WriteLine("唐老狮为string拓展的方法");
        Console.WriteLine("调用方法的对象" + str);
        Console.WriteLine("传的参数" + str2 + str3);
    }

    public static void Fun3(this Test t)
    {
        Console.WriteLine("为test拓展的方法");
    }

}
```

> 注意：
>
> 自身方法优先于拓展方法的调用。
>
> 不能为静态类扩展方法

# 任务21：运算符重载 知识点

## 知识点一 基本概念

概念：让自定义类和结构体，能够使用运算符

使用关键字：operator

特点：

1. **一定是一个公共的静态方法**
2. 返回值写在operator前
3. 逻辑处理自定义

作用：让自定义类和结构体对象可以进行运算

注意：

1. 条件运算符需要成对实现
2. 一个符号可以多个重载
3. 不能使用ref和out

## 知识点二 基本语法

```C#
public static 返回类型 operator 运算符(参数列表)
```

## 知识点三 实例

```C#
public static Point operator +(Point p1, Point p2)
{
    Point p = new Point();
    p.x = p1.x + p2.x;
    p.y = p1.y + p2.y;
    return p;
}
```

> 注意：当重载二元运算符时，参数之一必须包含本身类型，并且根据参数顺序决定左操作数和右操作数。

```C#
public static Point operator +(Point p1, int value)
{
    Point p = new Point();
    p.x = p1.x + value;
    p.y = p1.y + value;
    return p;
}

public static Point operator +(int value, Point p1)
{
    Point p = new Point();
    p.x = p1.x + value;
    p.y = p1.y + value;
    return p;
}
```

## 知识点五 可重载和不可重载的运算符

可重载的运算符：

1. 算数运算符：+，-，*，/，%，++，--
2. 逻辑运算符：!（只能重载逻辑非）
3. 位运算符：&，|，~，^，<<，>>
4. 条件运算符：>=，<=；==，!=；<，>；true，false
   1. 返回值一般是bool值 也可以是其它的
   2. **相关符号必须配对实现**
   3. 可以重载true和false，使得一个类型的变量可以作为一个bool值

**不可重载的运算符**：

逻辑与(&&) ，逻辑或(||)，索引符 []，强转运算符 ()

特殊运算符 ：点（.），三目运算符（? :），赋值符号（包括复合赋值运算符）（=，+=，-=....）

# 任务23：内部类和分部类 知识点

## 知识点一 内部类

概念：在一个类中再申明一个类

特点：使用时要用包裹者点出自己

作用：亲密关系的变现

注意：访问修饰符作用很大

```C#
class Person
{
    public int age;
    public string name;
    public Body body;
    public class Body
    {
        Arm leftArm;
        Arm rightArm;
        class Arm
        {

        }
    }
}
```

```C#
Person p = new Person();
Person.Body body = new Person.Body();
```

## 知识点二 分部类

概念：把一个类分成几部分申明

关键字：partial（需要写在访问修饰符的后面）

作用：分部描述一个类，增加程序的拓展性

注意：分部类可以写在多个脚本文件中，分部类的访问修饰符要一致，分部类中不能有重复成员

## 知识点三 分部方法

概念：将方法的声明和实现分离

特点：

1. 不能加访问修饰符 默认私有
2. 只能在分部类中声明
3. 返回值只能是void
4. 可以有参数但不用 out关键字

局限性大，了解即可

```C#
partial class Student
{
    public bool sex;
    public string name;

    partial void Speak();
}

partial class Student
{
    public int number;

    partial void Speak()
    {
        //实现逻辑
    }

    public void Speak(string str)
    {

    }
}
```

# 任务24：继承的基本概念 知识点

**注意**：C#当中无需指定继承访问权限，直接

：类名

继承即可

## 知识点一 基本概念

一个类A继承一个类B，类A将会继承类B的所有成员，A类将拥有B类的所有特征和行为

被继承的类称为 父类、基类、超类

继承的类称为子类、派生类

子类可以有自己的特征和行为

特点：

1. 单根性 子类只能有一个父类
2. 传递性 子类可以间接继承父类的父类 

## 知识点二 基本语法

```C#
//class 类名 : 被继承的类名
//{

//}
```

## 知识点四 访问修饰符的影响

public - 公共 内外部访问

private - 私有 内部访问，子类继承但是不能访问

protected - 保护 内部和子类访问

## 知识点五 子类和父类的同名成员

概念：C#中允许子类存在和父类同名的成员

但是 极不建议使用，会隐藏父类成员，如果需要明确隐藏，可以使用new关键字覆盖。

# 任务26：里氏替换原则 知识点

## 知识点一 基本概念

里氏替换原则是面向对象七大原则中最重要的原则

概念：任何父类出现的地方，子类都可以替代

重点：语法表现——父类容器装子类对象,因为子类对象包含了父类的所有内容

作用：方便进行对象存储和管理

## 知识点二 基本实现

```C#
//里氏替换原则 用父类容器 装载子类对象
GameObject player = new Player();
GameObject monster = new Monster();
GameObject boss = new Boss();
```

## 知识点三 is和as

基本概念：

is：判断一个对象是否是指定类对象

返回值：bool  是为真 不是为假

```C#
if( player is Player )
{
    //Player p = player as Player;
    //p.PlayerAtk();
    (player as Player).PlayerAtk();
}
```

as：将一个对象转换为指定类对象

返回值：指定类型对象

成功返回指定类型对象，失败返回null

```C#
for (int i = 0; i < objects.Length; i++)
{
    if( objects[i] is Player )
    {
        (objects[i] as Player).PlayerAtk();
    }
    else if( objects[i] is Monster )
    {
        (objects[i] as Monster).MonsterAtk();
    }
    else if (objects[i] is Boss)
    {
        (objects[i] as Boss).BossAtk();
    }
}
```

is和as一般是配合使用的，先判断is，再使用as。

# 任务28：继承中的构造函数 知识点

## 知识点一 继承中的构造函数 基本概念

特点：当申明一个子类对象时，先执行父类的构造函数，再执行子类的构造函数。

注意：

1. 父类的无参构造 很重要
2. 子类可以通过base关键字 代表父类 调用父类构造

## 知识点三 父类的无参构造函重要

子类实例化时 默认自动调用的 是父类的无参构造 所以如果父类无参构造被顶掉 会报错。

> 意思是，当父类没有无参构造函数时，子类无法创建。

## 知识点四 通过base调用指定父类构造

```C#
public Son(int i) : base(i)
{
    Console.WriteLine("Son的一个参数的构造");
}

public Son(int i, string str):this(i)
{
    Console.WriteLine("Son的两个参数的构造");
}
```

# 任务30：万物之父和装箱拆箱 知识点

## 知识点一 万物之父

关键字：object

概念：是所有类型的基类，它是一个类（引用类型）

作用：

1. 可以利用里氏替换原则，用object容器装所有对象
2. 可以用来表示不确定类型，作为函数参数类型

## 知识点二 万物之父的使用

可以通过as和强制转换将object对象转换为对应类型。

## 知识点三 装箱拆箱

发生条件：用object存值类型（装箱）

再把object转为值类型（拆箱）

装箱：把值类型用引用类型存储，栈内存会迁移到堆内存中

拆箱：把引用类型存储的值类型取出来，堆内存会迁移到栈内存中

好处：不确定类型时可以方便参数的存储和传递

坏处：存在内存迁移，增加性能消耗

```C#
//装箱
object v = 3;
//拆箱
int intValue = (int)v;
```

# 任务32：密封类 知识点

##  知识点一 基本概念

密封类 是使用 sealed密封关键字修饰的类

作用：让类无法再被继承

```C#
class Father
{

}

sealed class Son:Father
{

}
```

## 知识点三 作用

在面向对象程序的设计中，密封类的主要作用就是不允许最底层子类被继承

可以保证程序的规范性、安全性

目前对于大家来说 可能用处不大

随着大家的成长，以后制作复杂系统或者程序框架时 便能慢慢体会到密封的作用

# 任务34：多态vob 知识点

## 知识点一 多态的概念

多态按字面的意思就是“多种状态”，让继承同一父类的子类们 在执行相同方法时有不同的表现（状态）

主要目的：同一父类的对象 执行相同行为（方法）有不同的表现

解决的问题：让同一个对象有唯一行为的特征

## 知识点三 多态的实现

我们目前已经学过的多态，编译时多态——函数重载，开始就写好的

我们将学习的：运行时多态( vob、抽象函数、接口 )

v: virtual(虚函数)，o: override(重写)，b: base(父类)。

虚函数 可以被子类重写

base的作用：代表父类 可以通过base来保留父类的行为。

```C#
//重写虚函数
public override void Atk()
{
    //base的作用
    //代表父类 可以通过base来保留父类的行为
    base.Atk();
    Console.WriteLine("玩家对象进行攻击");
}
```

> 注意：虚函数不能是私有的

# 任务36：抽象类和抽象函数 知识点

## 知识点一 抽象类

概念：被抽象关键字abstract修饰的类

特点：

1. 不能被实例化的类
2. 可以包含抽象方法
2. 可以包含抽象方法、字段、属性
3. 继承抽象类必须重写其抽象方法

```C#
abstract class Thing
{
    //抽象类中 封装的所有知识点都可以在其中书写
    public string name;

    //可以在抽象类中写抽象函数
}
```

## 知识点二 抽象函数

又叫 纯虚方法，用 abstract关键字修饰的方法

特点：

1. 只能在抽象类中申明
2. 没有方法体
3. 不能是私有的
4. 继承后必须实现 用override重写

### 抽象方法和虚方法的区别

1. 虚方法是可以由我们子类选择性来实现的
2. 虚方法和抽象方法 都可以被子类无限的 去重写

### 如何选择普通类还是抽象类

不希望被实例化的对象，相对比较抽象的类可以使用抽象类。

父类中的行为不太需要被实现的，只希望子类去定义具体的规则的 可以选择 抽象类然后使用其中的抽象方法来定义规则

作用：整体框架设计时  会使用。

# 任务38：接口 知识点

## 知识点一 接口的概念

接口是行为的抽象规范

它也是一种自定义类型

关键字 ：interface

### 接口声明的规范

1. 不包含成员变量（字段）
2. 只包含方法、属性、索引器、事件
3. 成员不能被实现
4. 成员可以不用写访问修饰符（默认是公共的），不能是私有的，如果是protected的，必须显式实现接口
5. 接口不能继承类，但是可以继承另一个接口

### 接口的使用规范

1. 类可以继承多个接口
2. 类继承接口后，必须实现接口中所有成员

### 特点

1. 它和类的声明类似
2. 接口是用来继承的
3. 接口不能被实例化，但是可以作为容器存储对象

## 知识点二 接口的声明

```C#
//接口关键字：interface
//语法：
// interface 接口名
// {
// }
//一句话记忆：接口是抽象行为的“基类”
//接口命名规范 帕斯卡前面加个I
```

## 知识点三 接口的使用

```C#
interface IFly
{
    void Fly();

    string Name
    {
        get;
        set;
    }

    int this[int index]
    {
        get;
        set;
    }

    event Action doSomthing;
}
```

接口用来继承：

1. 类可以继承1个类，n个接口
2. **继承了接口后 必须实现其中的内容 并且必须是public的，如果不是public，则必须显示实现接口**
3. 实现的接口函数，可以加v再在子类重写
4. 接口也遵循里氏替换原则

```C#
//接口用来继承
class Animal
{

}

//1.类可以继承1个类，n个接口
//2.继承了接口后 必须实现其中的内容 并且必须是public的
class Person : Animal, IFly
{
    //3.实现的接口函数，可以加v再在子类重写
    public virtual void Fly()
    {

    }

    public string Name
    {
        get;
        set;
    }

    public int this[int index]
    {
        get
        {
            return 0;
        }
        set
        {

        }
    }

    public event Action doSomthing;
}
```

## 知识点四 接口可以继承接口

接口继承接口时  不需要实现。

待类继承接口后  类自己去实现所有内容。

```C#
interface IWalk
{
    void Walk();
}

interface IMove : IFly, IWalk
{ 
}
```

## 知识点五 显式实现接口

当一个接口中一个方法是protected时，继承的类需要显式实现接口；

当一个类继承两个接口，但是接口中存在着同名方法时，需要显式实现接口。

注意：显式实现接口时 不能写访问修饰符。

```C#
interface IAtk
{
    void Atk();
}

interface ISuperAtk
{
    void Atk();
}

class Player : IAtk, ISuperAtk
{
    //显示实现接口 就是用 接口名.行为名 去实现
    void IAtk.Atk()
    {

    }

    void ISuperAtk.Atk()
    {

    }

    public void Atk()
    {

    }
}
```

# 任务40：密封方法 知识点

## 知识点一 密封方法基本概念

用密封关键字sealed 修饰的重写函数

作用：让虚方法或者抽象方法之后不能再被重写

特点：和override一起出现

> 也就是说，在子类重写父类虚方法时，加上sealed，使得这个方法不能被子类的子类重写。

```C#
abstract class Animal
{
    public string name;
    public abstract void Eat();

    public virtual void Speak()
    {
        Console.WriteLine("叫");
    }
}

class Person:Animal
{
    public override void Eat()
    {

    }

    public override void Speak()
    {

    }
}

class WhitePerson:Person
{
    public sealed override void Eat()
    {
        base.Eat();
    }

    public sealed override void Speak()
    {
        base.Speak();
    }
}
```

# 任务41：命名空间 知识点

## 知识点一 命名空间基本概念

概念：命名空间是用来组织和重用代码的

作用：就像是一个工具包，类就像是一件一件的工具，都是声明在命名空间中的

## 知识点二 命名空间的使用

```C#
//基本语法
//namespace 命名空间名
//{
//  类
//  类
//}
```

1. 命名空间可以分开写（分文件写）
2. 命名空间内**不允许有相同名的类**
3. 使用命名空间中的类必须先引用命名空间

## 知识点三 不同命名空间中相互使用 需要引用命名空间或指明出处

```C#
GameObject g = new GameObject();

Image img0 = new Image();
MyGame.UI.Image img = new MyGame.UI.Image();	//指明出处
MyGame.Game.Image img2 = new MyGame.Game.Image();
```

## 知识点四 不同命名空间中允许有同名类

如题。

但是，如果拥有同名类，并且引用了两个命名空间，使用类时，需要指明出处，否则不明确。

## 知识点五 命名空间可以包裹命名空间

如题，但是引用时，必须逐级引用，才能引用被包裹的命名空间。

```C#
using MyGame;
using MyGame.UI;
```

## 知识点六 关于修饰类的访问修饰符

public：**命名空间中的类默认为public（并且不能显示的声明为其他权限）**

internal：只能在该程序集中使用（目前来说，一个项目就是一个程序集）

abstract：抽象类

sealed：密封类

partial：分部类

# 任务43：万物之父中的方法 知识点

注意：Object被所有类继承。

## 知识点一 object中的静态方法

### 静态方法 Equals 

判断两个对象是否相等，最终的判断权，交给左侧对象的Equals方法，不管值类型引用类型都会按照左侧对象Equals方法的规则来进行比较

```C#
Console.WriteLine(Object.Equals(1, 1));
```

### 静态方法ReferenceEquals

比较两个对象是否是相同的引用，主要是用来比较引用类型的对象。

值类型对象返回值始终是false。

## 知识点二 object中的成员方法

### 普通方法GetType

该方法在反射相关知识点中是非常重要的方法，之后我们会具体的讲解这里返回的Type类型。

该方法的主要作用就是获取对象运行时的类型Type，通过Type结合反射相关知识点可以做很多关于对象的操作。

```C#
Test t = new Test();
Type type = t.GetType();
```

### 普通方法MemberwiseClone

该方法用于获取对象的浅拷贝对象，口语化的意思就是会返回一个新的对象，但是新对象中的引用变量会和老对象中一致。

注意：只有引用是浅拷贝，值类型只有深拷贝。

## 知识点三 object中的虚方法

### 虚方法Equals

默认实现还是比较两者是否为同一个引用，即相当于ReferenceEquals。

但是微软在所有值类型的基类System.ValueType中重写了该方法，用来比较值相等。

我们也可以重写该方法，定义自己的比较相等的规则.

### 虚方法GetHashCode

该方法是获取对象的哈希码

（一种通过算法算出的，表示对象的唯一编码，不同对象哈希码有可能一样，具体值根据哈希算法决定），

我们可以通过重写该函数来自己定义对象的哈希码算法，正常情况下，我们使用的极少，基本不用。

### 虚方法ToString

该方法用于返回当前对象代表的字符串，我们可以重写它定义我们自己的对象转字符串规则，该方法非常常用。当我们调用打印方法时，默认使用的就是对象的ToString方法后打印出来的内容。

# 任务45：string 知识点

**注意：string不可变，所有对于string内容修改的方法，都返回一个新的string**

## 知识点一 字符串指定位置获取

字符串本质是char数组

```C#
string str = "唐老狮";
Console.WriteLine(str[0]);
```

可以转换为char数组

str.ToCharArray();

```C#
char[] chars = str.ToCharArray();
Console.WriteLine(chars[1]);	
```

## 知识点二 字符串拼接

string.Format

```C#
str = string.Format("{0}{1}", 1, 3333);
Console.WriteLine(str);
```

## 知识点三 正向查找字符位置

IndexOf

未找到返回-1

```C#
str = "我是唐老狮！";
int index = str.IndexOf("唐");
Console.WriteLine(index);

index = str.IndexOf("吊");
Console.WriteLine(index);
```

## 知识点四 反向查找指定字符串位置

```C#
str = "我是唐老狮唐老狮";

index = str.LastIndexOf("唐老狮");
Console.WriteLine(index);

index = str.LastIndexOf("唐老师");
Console.WriteLine(index);
```

## 知识点五 移除指定位置后的字符

Remove();

一个参数，移除index后的所有字符；

两个参数，移除index后的n个字符。

```C#
str = "我是唐老狮唐老狮";
str.Remove(4);
Console.WriteLine(str);
str = str.Remove(4);
Console.WriteLine(str);

//执行两个参数进行移除
//参数1 开始位置
//参数2 字符个数
str = str.Remove(1, 1);
Console.WriteLine(str);
```

## 知识点六 替换指定字符串

```C#
str = "我是唐老狮唐老狮";
str.Replace("唐老狮", "老炮儿");
Console.WriteLine(str);
str = str.Replace("唐老狮", "老炮儿");
Console.WriteLine(str);
```

## 知识点七 大小写转换

```C#
str = "ksdfasdfasfasdfsasdfasdf";
str.ToUpper();
Console.WriteLine(str);
str = str.ToUpper();
Console.WriteLine(str);

str.ToLower();
Console.WriteLine(str);
str = str.ToLower();
Console.WriteLine(str);
```

## 知识点八 字符串截取

Substring，截取从指定位置开始之后的字符串

如果指定长度，不会自动的帮助你判断是否越界，你需要自己去判断

```C#
str = "唐老狮唐老狮";
//截取从指定位置开始之后的字符串
str.Substring(2);
Console.WriteLine(str);
str = str.Substring(2);
Console.WriteLine(str);

//参数一 开始位置
//参数二 指定个数
//不会自动的帮助你判断是否越界 你需要自己去判断
str = str.Substring(2, 2);
Console.WriteLine(str);
```

## 知识点九 字符串切割

Split

```C#
str = "1_1|2_2|3_3|5_1|6_1|7_2|8_3";
string[] strs = str.Split('|');
for (int i = 0; i < strs.Length; i++)
{
    Console.WriteLine(strs[i]);
    //x_x
}
```

# 任务47：StringBuilder 知识点

## 知识点 StringBuilder

## 初始化 直接指明内容

```C#
//必须要new，不能直接= "str"
StringBuilder str = new StringBuilder("123123123");
Console.WriteLine(str);
```

## 容量

StringBuilder存在一个容量的问题，每次往里面增加时 会自动扩容

获得容量

```C#
Console.WriteLine(str.Capacity);
```

获得字符长度

```C#
Console.WriteLine(str.Length);
```

## 增删查改替换

```C#
//增
str.Append("4444");
Console.WriteLine(str);
Console.WriteLine(str.Length);
Console.WriteLine(str.Capacity);

str.AppendFormat("{0}{1}", 100, 999);
Console.WriteLine(str);
Console.WriteLine(str.Length);
Console.WriteLine(str.Capacity);
//插入
str.Insert(0, "唐老狮");
Console.WriteLine(str);
//删
str.Remove(0, 10);
Console.WriteLine(str);
//清空
//str.Clear();
//Console.WriteLine(str);
//查
Console.WriteLine(str[1]);
//改
str[0] = 'A';
Console.WriteLine(str);
//替换
str.Replace("1", "唐");
Console.WriteLine(str);

//重新赋值 StringBuilder
str.Clear();
str.Append("123123");
Console.WriteLine(str);
//判断StringBuilder是否和某一个字符串相等
if( str.Equals("12312") )
{
    Console.WriteLine("相等");
}
```

# 任务49：结构体和类的区别 知识点

## 区别概述

结构体和类最大的区别是在存储空间上的，因为结构体是值，类是引用，因此他们的存储位置一个在栈上，一个在堆上。

结构体和类在使用上很类似，结构体甚至可以用面向对象的思想来形容一类对象。结构体具备着面向对象思想中封装的特性，但是它不具备继承和多态的特性，因此大大减少了它的使用频率。

由于结构体不具备继承的特性（但是可以继承接口），所以它不能够使用protected保护访问修饰符。

## 细节区别

1. 结构体是值类型，类是引用类型
2. 结构体存在栈中，类存在堆中
3. 结构体成员不能使用protected访问修饰符，而类可以
4. 结构体成员变量声明不能指定初始值，而类可以
5. 结构体不能申明无参的构造函数，而类可以
6. 结构体申明有参构造函数后，无参构造不会被顶掉
7. 结构体不能申明析构函数，而类可以
8. 结构体不能被继承，而类可以
9. 结构体需要在构造函数中初始化所有成员变量，而类随意
10. 结构体不能被静态static修饰（不存在静态结构体），而类可以
11. 结构体不能在自己内部申明和自已一样的结构体变量，而类可以

## 结构体的特别之处

**结构体可以继承 接口 因为接口是行为的抽象**

## 如何选择结构体和类

1. 想要用继承和多态时，直接淘汰结构体，比如玩家、怪物等等
2. 对象是数据集合时，优先考虑结构体，比如位置、坐标等等
3. 从值类型和引用类型赋值时的区别上去考虑，比如经常被赋值传递的对象，并且改变赋值对象，原对象不想跟着变化时，就用结构体。比如坐标、向量、旋转等等

# 任务50：抽象类和接口的区别 知识点

## 知识点一 相同点

1. 都可以被继承
2. 都不能直接实例化
3. 都可以包含方法，属性，事件，索引器声明
4. 子类必须实现未实现的方法
5. 都遵循里氏替换原则

## 知识点二 区别

1. 抽象类中可以有构造函数；接口中不能
2. 抽象类只能被单一继承；接口可以被继承多个
3. 抽象类中可以有成员变量；接口中不能
4. 抽象类中可以申明成员方法，虚方法，抽象方法，静态方法；接口中只能申明没有实现的抽象方法
5. 抽象类方法可以使用访问修饰符；接口中建议不写，默认public

## 如何选择抽象类和接口

表示对象的用抽象类，表示行为拓展的用接口

不同对象拥有的共同行为，我们往往可以使用接口来实现

举个例子：动物是一类对象，我们自然会选择抽象类；而飞翔是一个行为，我们自然会选择接口。

# 任务52：多脚本文件 知识点

## 知识点一 了解脚本文件格式和路径

了解bin文件夹和工程目录文件。

## 知识点二 新建脚本文件

一般来说，一个类、一个接口就是一个文件。

在资源管理器直接新建项

## 知识点三 在文件夹中新建脚本文件

可以创建文件夹管理，但是需要注意命名空间的改变。

# 任务53：UML类图 知识点

emmm，软件建模学过了。

# 任务54：面向对象七大原则 知识点

七大原则总体要实现的目标是：模块内的高内聚、模块间的低耦合，使程序模块的可重用性、移植性增强。

## 七大原则

**单一职责原则:一个类只处理自己应该处理的内容，不应该啥都写在一起**

**开闭原则:对拓展开放，对修改封闭。新加功能尽量是加处理而不是改代码**

**里氏替换原则:任何地方子类都能替代父类，父类容器装子类**

**依赖倒转原则:不要依赖具体的实现，要依赖抽象（接口)**

**迪米特法则:一个类要尽量减少对别的类的了解，尽量少用别的类和自己关联**

**接口隔离原则:一个接口一个行为，不要一个接口n个行为**

**合成复用原则:除非设计上需要继承，否则尽量用组合复用的形式**

## 单一职责原则

SRP(Single Responsibility Principle)

类被修改的几率很大，因此应该专注于单一的功能。

如果把多个功能放在同一个类中，功能之间就形成了关联，改变其中一个功能，有可能中止另一个功能。

举例:假设程序、策划、美术三个工种是三个类，他们应该各司其职，在程序世界中只应该做自己应该做的事情。

## 开闭原则

OCP(Open-Closed Principle)对拓展开发，对修改关闭

拓展开放:模块的行为可以被拓展从而满足新的需求

修改关闭:不允许修改模块的源代码（或者尽量使修改最小化)

举例:继承就是最典型的开闭原则的体现，可以通过添加新的子类和重写父类的方法来实现

## 里氏替换原则

LSP(Liskov Substitution Principle)

任何父类出现的地方，子类都可以替代

举例:用父类容器装载子类对象，因为子类对象包含了父类的所有内容

## 依赖倒转原则

DIP(Dependence Inversion Principle)

要依赖于抽象，不要依赖于具体的实现

## 迪米特原则

LoP(Law of Demeter)

又称最少知识原则

一个对象应当对其它对象尽可能少的了解不要和陌生人说话

举例:一个对象中的成员，要尽可能少的直接和其它类建立关系目的是降低耦合性

## 接口分离原则

ISP(Interface Segregation Principle)

不应该强迫别人依赖他们不需要使用的方法

一个接口不需要提供太多的行为，一个接口应该尽量只提供一个对外的功能

让别人去选择需要实现什么样的行为，而不是把所有的行为都封装到一个接口当中

举例:飞行接口、走路接口、跑步接口等等虽然都是移动的行为但是我们应该把他们分为一个一个单独的接口，让别人去选择使用

## 合成复用原则

CRP(Composite Reuse Principle)

尽量使用对象组合，而不是继承来达到复用的目的继承关系是强耦合，组合关系是低耦合

举例:脸应该是眼镜、鼻子、嘴巴、耳朵的组合，而不是依次的继承角色和装备也应该是组合，而不是继承

注意:不能盲目的使用合成复用原则，要在遵循迪米特原则的前提下

## 如何使用这些原则

在开始做项目之前，整理UML类图时先按自己的想法把需要的类整理出来

再把七大原则截图放在旁边，基于七大原则去优化整理自己的设计

整体目标就是:高内聚，低耦合

初学程序阶段

不要过多的**纠结于七大原则**

先用最适合自己的方法把需求实现了再使用七大原则去优化

不要想着一步到位，要循序渐进

面向对象编程能力提升是需要经验积累的

# -----------------------------

# 【唐老狮】Unity基础课程之C#进阶

# 任务2：ArrayList 知识点

## 知识点一 ArrayList的本质

ArrayList是一个C#为我们封装好的类，它的本质是一个object类型的数组。

ArrayList类帮助我们实现了很多方法，比如数组的增删查改。

## 知识点二 声明

需要引用命名空间using System.Collections;

```C#
ArrayList array = new ArrayList();
```

## 知识点三 增删查改

增

```C#
public virtual int Add(object? value);	//添加一个元素
public virtual void AddRange(ICollection c);	//添加一个范围内的元素
public virtual void Insert(int index, object? value); //在index处插入指定元素
public virtual void InsertRange(int index, ICollection c);	//在index处插入指定范围元素
```

删

```C#
public virtual void Remove(object? obj);	//删除指定元素
public virtual void RemoveAt(int index);	//删除指定位置index的元素
public virtual void RemoveRange(int index, int count);	//删除指定位置index开始的count个元素
public virtual void Clear();	//清空容器
```

查

```C#
public virtual object? this[int index] { get; set; }	//索引器
public virtual bool Contains(object? item);	//查找item是否存在于容器中
public virtual int IndexOf(object? value);	//正向查找value的位置
public virtual int LastIndexOf(object? value);	//反向查找value的位置
```

改

```C#
array[0] = "999";	//直接使用索引器进行修改
```

遍历

```C#
public virtual int Count { get; }	//属性，返回元素个数
public virtual int Capacity { get; set; }	//属性，返回容量
//迭代器遍历
foreach (object item in array)
{
    Console.WriteLine(item);
}
```

## 知识点四 装箱拆箱

ArrayList本质上是一个可以自动扩容的object数组，由于用万物之父来存储数据，自然存在装箱拆箱

当往其中进行值类型存储时就是在装箱，当将值类型对象取出来转换使用时，就存在拆箱

所以ArrayList尽量少用，之后我们会学习更好的数据容器。

```C#
int k = 1;
array[0] = k;//装箱
k = (int)array[0];//拆箱
```

## 练习题一：请简述ArrayList和数组的区别

ArrayList本质上是一个object数组的封装

1. ArrayList可以不用一开始就定长，单独使用数组是定长的
2. 数组可以指定存储类型，ArrayList默认为object类型
3. 数组的增删需要我们自己去实现，ArrayList帮我们封装了方便的API来使用
4. ArrayList使用时可能存在装箱拆箱，数组使用时只要不是object数组那就不存在这个问题
5. 数组长度为Length, ArrayList长度为Count

# 任务4：Stack 知识点

## 知识点一 Stack的本质

Stack（栈）是一个C#为我们封装好的类

它的本质也是object[]数组，只是封装了特殊的存储规则

Stack是栈存储容器，栈是一种先进后出的数据结构

先存入的数据后获取，后存入的数据先获取

栈是先进后出

## 知识点二 声明

需要引用命名空间 System.Collections

```C#
Stack stack = new Stack();
```

## 知识点三 增取查改

增

```C#
public virtual void Push(object obj);	//入栈
```

取

栈中不存在删除的概念，只有取出栈的概念

```C#
public virtual object Pop();	//出栈，删除栈顶元素，并返回这个元素
```

查

```C#
//栈无法查看指定位置的 元素，只能查看栈顶的内容
public virtual object Peek();	//返回栈顶元素，但是不删除
public virtual bool Contains(object obj);	//查看元素是否存在于栈中
```

改

栈无法改变其中的元素 只能压(存)和弹（取），实在要改 只有清空

```C#
public virtual void Clear();	//清空栈
```

## 知识点四 遍历

长度

```C#
public virtual int Count { get; }	//属性，返回栈中元素个数
```

用foreach遍历，遍历出来的顺序 也是从栈顶到栈底

```C#
foreach(object item in stack)
{
    Console.WriteLine(item);
}
```

还有一种遍历方式，将栈转换为object数组，遍历出来的顺序 也是从栈顶到栈底

```C#
object[] array = stack.ToArray();
for (int i = 0; i < array.Length; i++)
{
    Console.WriteLine(array[i]);
}
```

循环弹栈遍历

```C#
while( stack.Count > 0 )
{
    object o = stack.Pop();
    Console.WriteLine(o);
}
Console.WriteLine(stack.Count);
```

## 知识点五 装箱拆箱

由于用万物之父来存储数据，自然存在装箱拆箱。

当往其中进行值类型存储时就是在装箱。

当将值类型对象取出来转换使用时，就存在拆箱。

# 任务6：Queue 知识点

## 知识点一 Queue本质

Queue是一个C#为我们封装好的类，它的本质也是object[]数组，只是封装了特殊的存储规则

Queue是队列存储容器，队列是一种先进先出的数据结构，先存入的数据先获取，后存入的数据后获取。

先进先出

##  知识点二 声明

需要引用命名空间 System.Collections

```C#
Queue queue = new Queue();
```

## 知识点三 增取查改

增

```C#
public virtual void Enqueue(object obj);	//入队
```

取

队列中不存在删除的概念，只有取的概念 取出先加入的对象

```C#
public virtual object Dequeue();	//取出队头元素并删除，然后返回
```

查

```C#
//查看队列头部元素但不会移除
public virtual object Peek();	//取出队头元素但不删除，然后返回
public virtual bool Contains(object obj);	//查看元素是否存在于队列中
```

改

队列无法改变其中的元素 只能进出队列，实在要改 只有清空

```C#
public virtual void Clear();
```

## 知识点四 遍历

长度

```C#
public virtual int Count { get; }
```

用foreach遍历

```C#
foreach (object item in queue)
{
    Console.WriteLine(item);
}
```

将队列转换为object数组遍历

```C#
object[] array = queue.ToArray();
for (int i = 0; i < array.Length; i++)
{
    Console.WriteLine(array[i]);
}
```

循环出队遍历

```C#
while(queue.Count>0)
{
    object o = queue.Dequeue();
    Console.WriteLine(o);
}
Console.WriteLine(queue.Count);
```

## 知识点五 装箱拆箱

由于用万物之父来存储数据，自然存在装箱拆箱。

当往其中进行值类型存储时就是在装箱。

当将值类型对象取出来转换使用时，就存在拆箱。

# 任务8：Hashtable 知识点

## 知识点一 Hashtalbe的本质

Hashtable（又称散列表） 是基于键的哈希代码组织起来的 键/值对

它的主要作用是提高数据查询的效率

使用键来访问集合中的元素

## 知识点二 声明

需要引用命名空间 System.Collections

```C#
Hashtable hashtable = new Hashtable();
```

## 知识点三 增删查改

增

注意：不能出现相同键

```C#
public virtual void Add(object key, object? value);	//添加一组键值对
```

删：只能通过键去删除；删除不存在的键 没反应；或者直接清空

```C#
public virtual void Remove(object key);
public virtual void Clear();
```

查

```C#
public virtual object? this[object key] { get; set; }	//索引器，通过键查找值
//查看是否存在，根据键检测，找不开返回null
public virtual bool Contains(object key);
public virtual bool ContainsKey(object key);
//根据值检测
public virtual bool ContainsValue(object? value);
```

改：只能改 键对应的值内容 无法修改键

```C#
hashtable[1] = 100.5f;	//通过索引器修改
```

## 知识点四 遍历

得到键值对 对数

```C#
public virtual int Count { get; }	//属性，返回键值对的个数
```

遍历所有键

```C#
foreach (object item in hashtable.Keys)
{
    Console.WriteLine("键："+item);
    Console.WriteLine("值："+hashtable[item]);
}
```

遍历所有值

```C#
foreach (object item in hashtable.Values)
{
    Console.WriteLine("值：" + item);
}
```

键值对一起遍历

```C#
foreach (DictionaryEntry item in hashtable)
{
	Console.WriteLine("键：" + item.Key + "值：" + item.Value);
}
```

迭代器遍历法

```C#
IDictionaryEnumerator myEnumerator = hashtable.GetEnumerator();
bool flag = myEnumerator.MoveNext();
while (flag)
{
    Console.WriteLine("键：" + myEnumerator.Key + "值：" + myEnumerator.Value);
    flag = myEnumerator.MoveNext();
}
```

## 知识点五 装箱拆箱

由于用万物之父来存储数据，自然存在装箱拆箱

当往其中进行值类型存储时就是在装箱

当将值类型对象取出来转换使用时，就存在拆箱

# 任务10：泛型 知识点

## 知识点一 泛型是什么

泛型实现了类型参数化，达到代码重用目的

通过类型参数化来实现同一份代码上操作多种类型

泛型相当于类型占位符

定义类或方法时使用替代符代表变量类型

当真正使用类或者方法时再具体指定类型

## 知识点二 泛型分类

泛型类和泛型接口

基本语法：

```C#
class 类名<泛型占位字母>
interface 接口名<泛型占位字母>
```

泛型函数

```C#
//基本语法：函数名<泛型占位字母>(参数列表)
```

注意：泛型占位字母可以有多个，用逗号分开

## 知识点三 泛型类和接口

```C#
class TestClass<T>
{
    public T value;
}    

class TestClass2<T1,T2,K,M,LL,Key,Value>
{
    public T1 value1;
    public T2 value2;
    public K value3;
    public M value4;
    public LL value5;
    public Key value6;
    public Value value7;
}

interface TestInterface<T>
{
    T Value
    {
        get;
        set;
    }
}

//注意，继承泛型接口，必须指定类型
class Test : TestInterface<int>
{
    public int Value { get => throw new NotImplementedException(); set => throw new NotImplementedException(); }
}
```

```C#
TestClass<int> t = new TestClass<int>();
t.value = 10;
Console.WriteLine(t.value);

TestClass<string> t2 = new TestClass<string>();
t2.value = "123123";
Console.WriteLine(t2.value);

TestClass2<int, string, float, double, TestClass<int>, uint, short> t3 = new TestClass2<int, string, float, double, TestClass<int>, uint, short>();

```

## 知识点四 泛型方法

### 普通类中的泛型方法

```C#
class Test2
{
    public void TestFun<T>( T value)
    {
        Console.WriteLine(value);
    }

    public void TestFun<T>()
    {
        //用泛型类型 在里面做一些逻辑处理
        T t = default(T);
    }

    public T TestFun<T>(string v)
    {
        return default(T);
    }

    public void TestFun<T,K,M>(T t, K k, M m)
    {

    }
}
```

### 泛型类中的泛型方法

```C#
class Test2<T>
{
    public T value;

    public void TestFun<K>(K k)
    {
        Console.WriteLine(k);
    }

    //这个不叫泛型方法 因为 T是泛型类申明的时候 就指定 在使用这个函数的时候 
    //我们不能再去动态的变化了
    public void TestFun(T t)
    {

    }
}
```

```C#
Test2 tt = new Test2();
tt.TestFun<string>("123123");

Test2<int> tt2 = new Test2<int>();
tt2.TestFun(10);
tt2.TestFun<string>("123");
tt2.TestFun<float>(1.2f);
tt2.TestFun(20);
```

## 知识点五 泛型的作用

1. 不同类型对象的相同逻辑处理就可以选择泛型
2. 使用泛型可以一定程度避免装箱拆箱

举例：优化ArrayList

```C#
class ArrayList<T>
{
    private T[] array;

    public void Add(T value)
    {

    }

    public void Remove( T value)
    {

    }
}
```

## 总结

1. 声明泛型时 它只是一个类型的占位符
2. 泛型真正起作用的时候 是在使用它的时候
3. 泛型占位字母可以有n个用逗号分开
4. 泛型占位字母一般是大写字母
5. 不确定泛型类型时 获取默认值 可以使用default(占位字符)
6. 看到<>包裹的字母 那肯定是泛型

# 任务12：泛型约束 知识点

## 知识点一 什么是泛型约束

让泛型的类型有一定的限制，关键字：where

泛型约束一共有6种：

|              约束              |            关键字             |
| :----------------------------: | :---------------------------: |
|             值类型             |     where 泛型字母:struct     |
|            引用类型            |     where 泛型字母:class      |
|      存在无参公共构造函数      |     where 泛型字母:new()      |
|     某个类本身或者其派生类     |      where 泛型字母:类名      |
|       某个接口的派生类型       |     where 泛型字母:接口名     |
| 另一个泛型类型本身或者派生类型 | where 泛型字母:另一个泛型字母 |

## 知识点二 各泛型约束讲解

### 值类型约束

约束类型T必须是值类型

```C#
class Test1<T> where T:struct
{
    public T value;

    public void TestFun<K>(K v) where K:struct
    {

    }
}
```

### 引用类型约束

约束类型T必须是引用类型

```C#
class Test2<T> where T:class
{
    public T value;

    public void TestFun<K>(K k) where K:class
    {

    }
}
```

### 公共无参构造约束

约束类型T必须拥有公告无参构造函数（即可实例化，可new）

```C#
class Test3<T> where T:new()
{
    public T value;

    public void TestFun<K>(K k) where K : new()
    {

    }
}
```

### 类约束

约束类型T必须是某个类或者这个类的子类

```C#
class Test4<T> where T : Test1
{
    public T value;

    public void TestFun<K>(K k) where K : Test1
    {

    }
}
```

### 接口约束

约束类型必须是这个接口的子类

```C#
interface IFly
{

}

interface IMove:IFly
{

}

class Test4:IFly
{

}

class Test5<T> where T : IFly
{
    public T value;

    public void TestFun<K>(K k) where K : IFly
    {

    }
}
```

### 另一个泛型约束

约束类型T是U本身或者U的子类

```C#
class Test6<T,U> where T : U
{
    public T value;

    public void TestFun<K,V>(K k) where K : V
    {

    }
}
```

## 知识点三 约束的组合使用

约束可以组合使用，但有时不能同时存在两个约束，或者两个约束的顺序有次序

比如，new()约束一般写在其他约束前面。

```C#
class Test7<T> where T: class,new()
{

}
```

## 知识点四 多个泛型有约束

```C#
class Test8<T,K> where T:class,new() where K:struct
{

}
```

## 总结

泛型约束：让类型有一定限制

六种约束：class，struct，new()，类名，接口名，另一个泛型字母

注意：

1. 可以组合使用
2. 多个泛型约束 用where连接即可

# 任务14：List 知识点

## 知识点一 List的本质

List是一个C#为我们封装好的类，它的本质是一个可变类型的泛型数组。

List类帮助我们实现了很多方法，比如泛型数组的增删查改。

## 知识点二 声明

需要引用命名空间

```C#
using System.Collections.Generic;
```

```C#
List<int> list = new List<int>();
List<string> list2 = new List<string>();
List<bool> list3 = new List<bool>();
```

## 知识点三 增删查改

增

```C#
public void Add(T item);	//添加一个元素
public void AddRange(IEnumerable<T> collection);	//添加一个范围内的元素
public void Insert(int index, T item);	//在index处插入item
```

删

```C#
public bool Remove(T item);
public void RemoveAt(int index);
public void Clear();
```

查

```C#
public T this[int index] { get; set; }	//索引器
public bool Contains(T item);
public int IndexOf(T item);
public int LastIndexOf(T item);
```

改：使用索引器修改

## 知识点四 遍历

长度和容量

```C#
public int Count { get; }
public int Capacity { get; set; }
```

直接遍历

```C#
for (int i = 0; i < list.Count; i++)
{
    Console.WriteLine(list[i]);
}
```

foreach遍历

```C#
foreach (int item in list)
{
    Console.WriteLine(item);
}
```

# 任务16：Dictionary 知识点

## 知识点一 Dictionary的本质

可以将Dictionary理解为 拥有泛型的Hashtable；

它也是基于键的哈希代码组织起来的 键/值对；

键值对类型从Hashtable的object变为了可以自己制定的泛型。

## 知识点二 声明

需要引用命名空间 using System.Collections.Generic

```C#
Dictionary<int, string> dictionary = new Dictionary<int, string>();
```

## 知识点三 增删查改

增

注意：不能出现相同键

```C#
public void Add(TKey key, TValue value);
```

删：只能通过键去删除，删除不存在键 没反应。

```C#
public bool Remove(TKey key);
public void Clear();	//清空
```

查

```C#
//通过键查看值，找不到直接报错，和HashTable不一样，不会返回null了
public TValue this[TKey key] { get; set; }	//索引器
//查看是否存在，根据键检测
public bool ContainsKey(TKey key);
//根据值检测
public bool ContainsValue(TValue value);
```

改：通过索引器修改

## 知识点四 遍历

遍历所有键

```C#
foreach (int item in dictionary.Keys)
{
    Console.WriteLine(item);
    Console.WriteLine(dictionary[item]);
}
```

遍历所有值

```C#
foreach (string item in dictionary.Values)
{
    Console.WriteLine(item);
}
```

键值对一起遍历

```C#
foreach (KeyValuePair<int,string> item in dictionary)
{
    Console.WriteLine("键：" + item.Key + "值：" + item.Value);
}
```

# 任务18：顺序存储和链式存储 知识点

## 知识点一 数据结构

数据结构：

数据结构是计算机存储、组织数据的方式（规则）；

数据结构是指相互之间存在一种或多种特定关系的数据元素的集合；

比如自定义的一个 类 也可以称为一种数据结构 自己定义的数据组合规则

> 不要把数据结构想的太复杂，简单点理解，就是人定义的 存储数据 和 表示数据之间关系 的规则而已

常用的数据结构（前辈总结和制定的一些经典规则）

数组、栈、队列、链表、树、图、堆、散列表

## 知识点二 线性表

线性表是一种数据结构，是由n个具有相同特性的数据元素的有限序列

比如数组、ArrayList、Stack、Queue、链表等等

顺序存储和链式存储 是数据结构中两种 存储结构

## 知识点三 顺序存储

数组、Stack、Queue、List、ArrayList —— 顺序存储

只是 数组、Stack、Queue的 组织规则不同而已

顺序存储：用一组地址连续的存储单元依次存储线性表的各个数据元素

## 知识点四 链式存储

单向链表、双向链表、循环链表 —— 链式存储

链式存储(链接存储)：用一组任意的存储单元存储线性表中的各个数据元素

## 知识点五 自己实现一个最简单的单向链表

这里实现的链表有bug，没有处理移除尾结点的情况。

```C#
/// <summary>
/// 单向链表节点
/// </summary>
/// <typeparam name="T"></typeparam>
class LinkedNode<T>
{
    public T value;
    //这个存储下一个元素是谁 相当于钩子
    public LinkedNode<T> nextNode;

    public LinkedNode(T value)
    {
        this.value = value;
    }
}

/// <summary>
/// 单向链表类 管理 节点 管理 添加等等
/// </summary>
/// <typeparam name="T"></typeparam>
class LindedList<T>
{
    public LinkedNode<T> head;
    public LinkedNode<T> last;

    public void Add(T value)
    {
        //添加节点 必然是new一个新的节点
        LinkedNode<T> node = new LinkedNode<T>(value);
        if( head == null )
        {
            head = node;
            last = node;
        }
        else
        {
            last.nextNode = node;
            last = node;
        }
    }

    public void Remove(T value)
    {
        if( head == null )
        {
            return;
        }
        if( head.value.Equals(value) )
        {
            head = head.nextNode;
            //如果头节点 被移除 发现头节点变空
            //证明只有一个节点 那尾也要清空
            if( head == null )
            {
                last = null;
            }
            return;
        }
        LinkedNode<T> node = head;
        while(node.nextNode != null)
        {
            if( node.nextNode.value.Equals(value) )
            {
                //让当前找到的这个元素的 上一个节点
                //指向 自己的下一个节点
                node.nextNode = node.nextNode.nextNode;
                break;
            }
        }
    }
}
```

## 知识点六 顺序存储和链式存储的优缺点

从增删查改的角度去思考：

增：链式存储 计算上 优于顺序存储 （中间插入时链式不用像顺序一样去移动位置）

删：链式存储 计算上 优于顺序存储 （中间删除时链式不用像顺序一样去移动位置）

查：顺序存储 使用上 优于链式存储 （数组可以直接通过下标得到元素，链式需要遍历）

改：顺序存储 使用上 优于链式存储 （数组可以直接通过下标得到元素，链式需要遍历）

## 练习题三-实现双向链表

```C#
class LinkedNode<T>
{
    public T value;
    public LinkedNode<T> frontNode;
    public LinkedNode<T> nextNode;

    public LinkedNode(T value)
    {
        this.value = value;
    }
}

class LinkedList<T>
{
    private int count = 0;
    private LinkedNode<T> head;
    private LinkedNode<T> last;

    public int Count
    {
        get
        {
            return count;
        }
    }
    public LinkedNode<T> Head
    {
        get
        {
            return head;
        }
    }
    public LinkedNode<T> Last
    {
        get
        {
            return last;
        }
    }

    public void Add(T value)
    {
        //新加节点
        LinkedNode<T> node = new LinkedNode<T>(value);
        if( head == null )
        {
            head = node;
            last = node;
        }
        else
        {
            //添加到尾部
            last.nextNode = node;
            //尾部添加的节点 记录自己的上一个节点是谁
            node.frontNode = last;
            //让当前新加的变成最后一个节点
            last = node;
        }
        //加了一个节点
        ++count;
    }

    public void RemoveAt(int index)
    {
        //首先判断 有没有越界
        if( index >= count || index < 0)
        {
            Console.WriteLine("只有{0}个节点，请输入合法位置", count);
            return;
        }
        int tempCount = 0;
        LinkedNode<T> tempNode = head;
        while (true)
        {
            //找到了对应位置的节点 然后移除即可
            if ( tempCount == index )
            {
                //当前要移除的节点的上一个节点 指向自己的下一个节点
                if( tempNode.frontNode != null )
                {
                    tempNode.frontNode.nextNode = tempNode.nextNode;
                }
                if(tempNode.nextNode != null)
                {
                    tempNode.nextNode.frontNode = tempNode.frontNode;
                }
                //如果是头节点 那需要改变头节点的指向
                if (index == 0)
                {
                    //如果头节点被移除 那头节点就变成了头节点的下一个
                    head = head.nextNode;
                }
                else if( index == count - 1 )
                {
                    //如果尾节点被移除了 那尾结点就变成了尾结点的上一个
                    last = last.frontNode;
                }
                //移除了一个元素 就应该短一截
                --count;
                break;
            }
            //每次循环完过后 要让当前临时节点 等于下一个节点
            tempNode = tempNode.nextNode;
            ++tempCount;
        }
    }
}
```

# 任务20：LinkedList 知识点

## 知识点一 LinkedList

LinkedList是一个C#为我们封装好的类，它的本质是一个可变类型的泛型双向链表

## 知识点二 声明

需要引用命名空间

```C#
using System.Collections.Generic;
```

```C#
LinkedList<int> linkedList = new LinkedList<int>();
LinkedList<string> linkedList2 = new LinkedList<string>();
```

链表对象 需要掌握两个类

一个是链表本身 一个是链表节点类LinkedListNode

## 知识点三 增删查改

增

```C#
public LinkedListNode<T> AddLast(T value);	//尾部添加元素
public LinkedListNode<T> AddFirst(T value);	//头部添加元素
public LinkedListNode<T> AddAfter(LinkedListNode<T> node, T value);	//在某个节点后添加元素
public LinkedListNode<T> AddBefore(LinkedListNode<T> node, T value);//在某个节点前添加元素
```

删

```C#
public void RemoveFirst();	//移除头结点
public void RemoveLast();	//移除尾结点
public bool Remove(T value);	//移除指定元素
public void Remove(LinkedListNode<T> node);	//移除指定节点
public void Clear();	//清空元素
```

查

```C#
public LinkedListNode<T>? First { get; }	//头结点
public LinkedListNode<T>? Last { get; }		//尾结点
//找到第一个指定值的节点，无法直接通过下标获取中间元素，只有遍历查找指定位置元素
public LinkedListNode<T>? Find(T value);
//找到最后一个指定值的节点
public LinkedListNode<T>? FindLast(T value);
public bool Contains(T value);	//判断是否存在
```

改：要先得再改 得到节点 再改变其中的值

```C#
Console.WriteLine(linkedList.First.Value);
linkedList.First.Value = 10;
Console.WriteLine(linkedList.First.Value);
```

## 知识点四 遍历

LinkedListNode

```C#
public LinkedListNode<T>? Next { get; }	//属性，上一个节点
public LinkedListNode<T>? Previous { get; }	//属性，下一个节点
```

foreach遍历

```C#
foreach (int item in linkedList)
{
    Console.WriteLine(item);
}
```

通过节点遍历

```C#
//从头到尾
LinkedListNode<int> nowNode = linkedList.First;
while (nowNode != null)
{
    Console.WriteLine(nowNode.Value);
    nowNode = nowNode.Next;
}
//从尾到头
nowNode = linkedList.Last;
while (nowNode != null)
{
    Console.WriteLine(nowNode.Value);
    nowNode = nowNode.Previous;
}
```

# 任务22：泛型栈和队列 知识点

## 知识点一 回顾数据容器

变量

```C#
//无符号
//byte ushort uint ulong
//有符号
//sbyte short int long
//浮点数
//float double decimal
//特殊
//char bool string
```

复杂数据容器

```C#
//枚举 enum
//结构体 struct
//数组（一维、二维、交错） []  [,]  [][]
//类
```

数据集合（容器）

```C#
//using System.Collections;

//ArrayList  object数据列表
//Stack 栈  先进后出
//Queue 队列  先进先出
//Hashtable   哈希表  键值对
```

泛型数据集合

```C#
//using System.Collections.Generic;

//List  列表  泛型列表
//Dictionary 字典  泛型哈希表
//LinkedList 双向链表 
//Statck 泛型栈
//Queue 泛型队列
```

## 知识点二 泛型栈和队列

命名空间：using System.Collections.Generic;	

使用上 和之前的Stack和Queue一模一样

```C#
Stack<int> stack = new Stack<int>();
Queue<object> queue = new Queue<object>();
```

## 练习题

自己总结一下，数组、List、Dictionary、Stack、Queue、LinkedList

这些存储容器，对于我们来说应该如何选择他们来使用

普通线性表：
数组，List，LinkedList
数组：固定的不变的一组数据
List: 经常改变，经常通过下标查找
LinkedList：不确定长度的，经常临时插入改变，查找不多

先进后出：
Stack
对于一些可以利用先进后出存储特点的逻辑
比如：UI面板显隐规则

先进先出：
Queue
对于一些可以利用先进先出存储特点的逻辑
比如：消息队列，有了就往里放，然后慢慢依次处理

键值对：
Dictionary
需要频繁查找的，有对应关系的数据
比如一些数据存储  id对应数据内容
道具ID ——> 道具信息
怪物ID ——> 怪物对象
等等

# 任务24：委托 知识点

[C# 的委托与事件具体是怎么一回事_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1AT411U7H2/?spm_id_from=333.788&vd_source=02ee6d2f2e800f429c9d6d0d1b14955f)

## 知识点一 委托是什么

委托是 函数(方法)的容器 ，可以理解为表示函数(方法)的变量类型

用来 存储、传递函数(方法)

委托的本质是一个类，用来定义函数(方法)的类型（返回值和参数的类型）

不同的 函数(方法)必须对应和各自"格式"一致的委托

## 知识点二 基本语法

关键字 ： delegate
语法：访问修饰符 delegate 返回值 委托名(参数列表);

写在哪里？

可以声明在namespace和class语句块中

更多的写在namespace中

简单记忆委托语法 就是 函数申明语法前面加一个delegate关键字

## 知识点三 定义自定义委托

访问修饰默认不写 为public 在别的命名空间中也能使用

private 其它命名空间就不能用了，一般使用public

```C#
//申明了一个可以用来存储无参无返回值函数的容器
//这里只是定义了规则 并没有使用
delegate void MyFun();

//委托规则的申明 是不能重名（同一语句块中）
//表示用来装载或传递 返回值为int 有一个int参数的函数的 委托 容器规则
public delegate int MyFun2(int a);

//委托是支持 泛型的 可以让返回值和参数 可变 更方便我们的使用
delegate T MyFun3<T, K>(T v, K k);
```

## 知识点四 使用定义好的委托

记住，委托变量是**函数的容器**

注意：委托变量只能装载与本委托声明时，格式一致的函数。这里的格式是指**返回值与参数**

委托常用在：

1. 作为类的成员
2. 作为函数的参数

直接使用委托变量：

注意：使用委托，会将容器中的所有函数**全部都调用**，调用的顺序是添加的顺序

```C#
//定义了一个委托变量f，它的格式是无参无返回值
MyFun f = new MyFun(Fun);	//Fun是一个无参无返回值的函数名
f.Invoke();					//调用了Fun
f();						//调用了Fun
```

## 知识点五 委托变量可以存储多个函数(多播委托)

增加委托：

```C#
public void AddFun(MyFun fun, MyFun2 fun2)
{
    //fun是一个委托变量
    this.fun += fun;	//直接加
    this.fun2 += fun2;
}
```

> 注意：也可以直接加一个函数

```C#
MyFun ff = null;
//ff = ff + Fun;
ff += Fun;
ff += Fun3;
//注意，不能在初始化时直接+
//MyFun ff += Fun;	//error
```

删除委托：

> 同样的，可以直接减一个函数，指定删除

```C#
public void RemoveFun(MyFun fun, MyFun2 fun2)
{
    //this.fun = this.fun - fun;
    this.fun -= fun;	//直接减
    this.fun2 -= fun2;
}

//从容器中移除指定的函数
ff -= Fun;
//多减 不会报错 无非就是不处理而已
ff -= Fun;
ff();
//清空容器
ff = null;
```

## 知识点六 系统定义好的委托

使用系统自带委托 需要引用using System;

参数修饰符：in协变为参数，out逆变为返回值。

Action：无返回值

```C#
Action action = Fun;
action += Fun3;
action();
//可以传n个参数的  系统提供了 1到16个参数的委托 直接用就行了
//定义了一个Action委托变量，这个委托的参数有两个
Action<int, string> action2 = Fun6;
```

Func：有返回值，最后一个类型为返回值。

```C#
//定义了一个Func委托变量，这个委托的参数有两个
Func<int, string> funcString = Fun4;
Func<int> funcInt = Fun5;
```

## 总结

简单理解 委托 就是装载、传递函数的容器而已

可以用委托变量 来存储函数或者传递函数的

系统其实已经提供了很多委托给我们用

Action:没有返回值，参数提供了 0~16个委托给我们用

Func:有返回值，参数提供了 0~16个委托给我们用

# 任务26：事件 知识点

## 知识点一 事件是什么

事件是基于委托的存在，事件是委托的安全包裹；

让委托的使用更具有安全性，事件 是一种特殊的变量类型。

> 可以说，事件，就是类中的委托。

## 知识点二 事件的使用

声明语法：

```C#
访问修饰符 event 委托类型 事件名;
```

事件的使用：

1. 事件是作为 成员变量存在于类中
2. **委托**怎么用 事件就怎么用

事件相对于委托的区别:

1. 不能在类外部 赋值，即**不能使用=**，但是**可以在类外部+=，-=**
2. 不能再类外部 调用，但是可以通过**封装再调用**
3. 事件 是**不能作为临时变量**在函数中使用的！

注意：**它只能作为成员存在于类和接口以及结构体中**

```C#
class Test
{
    //委托成员变量 用于存储 函数的
    public Action myFun;
    //事件成员变量 用于存储 函数的
    public event Action myEvent;

    public Test()
    {
        //事件的使用和委托 一模一样 只是有些 细微的区别
        myFun = TestFun;
        myFun += TestFun;
        myFun -= TestFun;
        myFun();
        myFun.Invoke();
        myFun = null;

        myEvent = TestFun;
        myEvent += TestFun;
        myEvent -= TestFun;
        myEvent();
        myEvent.Invoke();
        myEvent = null;
    }

    public void DoEvent()
    {
        if(myEvent != null)
        {
            myEvent();
        }
    }

    public void TestFun()
    {
        Console.WriteLine("123");
    }
}
```

```C#
//事件是不能再外部赋值的
//t.myEvent = null;
//t.myEvent = TestFun;
//t.myEvent = t.myEvent + TestFun;	//注意，这样也不行
//虽然不能直接赋值 但是可以 加减 去添加移除记录的函数
t.myEvent += TestFun;
t.myEvent -= TestFun;

//事件不能在外部调用
//t.myEvent();
//只能在类的内部去封装 调用
t.DoEvent();

//事件 是不能作为临时变量在函数中使用的
//event Action ae = TestFun;
```

## 知识点三 为什么有事件

1. 防止外部随意置空委托
2. 防止外部随意调用委托
3. 事件相当于对委托进行了一次封装 让其更加安全

## 总结

事件和委托的区别：事件和委托的使用基本是一模一样的，事件就是特殊的委托（类中的委托）

主要区别：

1. 事件不能再外部使用赋值=符号，只能使用+ - 委托 哪里都能用
2. 事件 不能再外部执行 委托哪里都能执行
3. 事件 不能作为 函数中的临时变量的 委托可以

# 任务28：匿名函数 知识点

## 知识点一 什么是匿名函数

顾名思义，就是没有名字的函数

匿名函数的使用主要是配合委托和事件进行使用

脱离委托和事件 是不会使用匿名函数的

## 知识点二 基本语法

```C#
delegate (参数列表)
{
    //函数逻辑
};
```

何时使用？

1. 函数中传递委托参数时
2. 委托或事件赋值时

## 知识点三 使用

它的使用就是委托或者事件的使用，区别是，一声明匿名函数就必须保存到委托或者事件中。

### 无参无返回

注意：由于匿名函数是匿名的，所以，要使用它，**必须保存到委托或者事件中！**

这样声明匿名函数 只是在声明函数而已 还没有调用

真正调用它的时候 是这个委托容器啥时候调用 就什么时候调用这个匿名函数

```C#
Action A = delegate ()
{
    Console.WriteLine("匿名函数逻辑");
};

A();
```

### 有参

```C#
Action<int, string> b = delegate (int a, string b)
{
    Console.WriteLine(a);
    Console.WriteLine(b);
};

b(100, "123");
```

### 有返回值

注意，这个返回值是通过委托Func控制的

```C#
Func<string> c = delegate ()
{
    return "123123";
};

Console.WriteLine(c());
```

### 一般使用情况

一般情况会作为函数参数传递 或者 作为函数返回值

```C#
class Test
{
    public Action action;

    //作为参数传递时
    public void Dosomthing(int a, Action fun)
    {
        Console.WriteLine(a);
        fun();
    }

    //作为返回值
    public Action GetFun()
    {
        return delegate() {
            Console.WriteLine("函数内部返回的一个匿名函数逻辑");
        };
    }

    public void TestTTTT()
    {

    }
}
```

```C#
//作函数参数
Test t = new Test();
Action ac = delegate ()
{
    Console.WriteLine("随参数传入的匿名函数逻辑");
};
t.Dosomthing(50, ac);

//  返回值
Action ac2 = t.GetFun();
ac2();
//一步到位 直接调用返回的 委托函数
t.GetFun()();	//这里调用GetFun返回了一个匿名函数，然后调用了他
```

## 知识点四 匿名函数的缺点

添加到委托或事件容器中后 不记录 无法单独移除

因为匿名函数没有名字 所以没有办法指定移除某一个匿名函数

注意：同样逻辑的匿名函数，不是同一个函数。

```C#
//此匿名函数 非彼匿名函数 不能通过看逻辑是否一样就证明是一个 
//ac3 -= delegate ()
//{
//    Console.WriteLine("匿名函数一");
//};
```

## 总结

匿名函数 就是没有名字的函数

固定写法：

```C#
delegate(参数列表){}	
```

使用：主要是在 委托传递和存储时  为了方便可以直接使用该匿名函数

缺点是 没有办法指定移除

# 任务30：lambda表达式 知识点

## 知识点一 什么是lambda表达式

可以将lambad表达式 理解为匿名函数的简写。

它除了写法不同外，使用上和匿名函数一模一样，都是和委托或者事件 配合使用的。

## 知识点二 lambda表达式语法

```C#
//匿名函数
//delegate (参数列表)
//{

//};

//lambad表达式
//(参数列表) =>
//{
//    //函数体
//};
```

## 知识点三 使用

无参无返回

```C#
Action a = () =>
{
    Console.WriteLine("无参无返回值的lambda表达式");
};
a();
```

有参

```C#
Action<int> a2 = (int value) =>
{
    Console.WriteLine("有参数lambda表达式{0}", value);
};
a2(100);
```

甚至参数类型都可以省略 参数类型和委托或事件容器一致

```C#
Action<int> a3 = (value) =>
{
    Console.WriteLine("省略参数类型的写法{0}", value);
};
a3(200);
```

有返回值

```C#
Func<string, int> a4 = (value) =>
{
    Console.WriteLine("有返回值有参数的lambda表达式{0}", value);
    return 1;
};
Console.WriteLine(a4("123123"));
```

其它传参使用等和匿名函数一样
缺点也是和匿名函数一样的

## 知识点四 闭包

内层的函数可以引用包含在它外层的函数的变量；	

即使外层函数的执行已经终止

注意：该变量提供的值并非变量创建时的值，而是在**父函数范围内的最终值**。

```C#
class Test
{
    public event Action action;

    public Test()
    {
        int value = 10;
        //这里就形成了闭包
        //因为 当构造函数执行完毕时  其中申明的临时变量value的声明周期被改变了
        action = () =>
        {
            Console.WriteLine(value);
        };

        for (int i = 0; i < 10; i++)
        {
            //此index 非彼index
            int index = i;
            action += () =>
            {
                //注意，这里的index值是10，因为i的最终值是10
                Console.WriteLine(index);
            };
        }
    }

    public void DoSomthing()
    {
        action();
    }
}
```

> 注意，上方程序中的index值是10，因为i的最终值是10

# 任务32：委托 补充知识点 有返回值的委托存储多个函数 调用时如何获取多个返回值？

问题：当有返回值的委托容器，存储多个函数时，我们想要获取所有的返回值

```C#
Func<string> funTest = () => {
	Console.WriteLine("第一个函数");
	return "1";
};

funTest += () => {
	Console.WriteLine("第二个函数");
	return "2";
};

funTest += () => {
	Console.WriteLine("第三个函数");
	return "3";
};
Console.WriteLine(funTest());	//3
```

上述程序如果直接调用，只会输出一个3，因为第三个函数是最后执行的，也就只返回最后一个函数的返回值。

为了解决这个问题，我们可以遍历委托容器中的每个函数

使用**Func.GetInvocationList()**函数获取容器中的每个函数，然后使用foreach遍历就可以了。

```C#
foreach (Func<string> func in funTest.GetInvocationList()) {
	Console.WriteLine(func());
}
```

# 任务33：List排序 知识点

## 知识点一 List自带排序方法

list提供了排序方法

```C#
public void Sort();	//默认升序
//ArrayList中也有Sort排序方法
```

## 知识点二 自定义类的排序

如果需要自定义类支持排序，类需要继承接口IComparable\<ClassName\>

并且实现接口

```C#
public int CompareTo(ClassName other)；
```

### CompareTo函数

在这个函数当中，我们需要处理排序逻辑，通过这个函数的返回值，决定排序的规则。

返回值的含义：

小于0：放在传入对象的前面

等于0：保持当前的位置不变

大于0：放在传入对象的后面

可以简单理解 传入对象的位置 就是0；

如果你的返回为负数 就放在它的左边 也就前面；

如果你返回正数 就放在它的右边 也就是后面；

注意，这里作为参照的对象是传入的对象。

```C#
public int CompareTo(Item other)
{
    //降序排序
    //如果本身的钱比另一个大，放到另一个的前面
    if( this.money > other.money )
    {
        return -1;
    }
    else
    {
        return 1;
    }
}
```

## 知识点三 通过委托函数进行排序

我们可以通过在排序函数传入委托，也就是函数，来指定排序规则。

```C#
public delegate int Comparison<in T>(T x, T y);
public void Sort(Comparison<T> comparison);
```

comparison是一个委托变量，所以，我们需要传入一个委托或者一个函数，用来指定排序规则。

其中，这个函数或委托，是一个有两个T类型的参数，返回int。

```C#
//传入一个委托（也可以说是匿名函数）
shopItems.Sort(delegate (ShopItem a, ShopItem b)
               {
                   return a.id > b.id ? 1 : -1;
               });
//传入一个lambda表达式（其实就是函数或者说委托）
shopItems.Sort((a, b) =>{ return a.id > b.id ? 1 : -1;});
```

## 总结

系统自带的变量(int,float,double.....) 一般都可以直接Sort

自定义类SOrt有两种方式

1. 继承接口 IComparable
2. 在Sort中传入委托函数

# 任务35：协变逆变 知识点

要理解协变逆变，其实就是要遵循**里氏替换原则**。

## 知识点一 什么是协变逆变

协变：和谐的变化，自然的变化；和谐的变化，自然的变化。

所以 子类变父类，比如 string 变成 object，感受是和谐的。

逆变：逆常规的变化，不正常的变化；因为 里氏替换原则 父类可以装子类 但是子类不能装父类。

所以 父类变子类，比如 object 变成 string，感受是不和谐的。

协变和逆变是用来修饰泛型的

**协变：out** 

**逆变：in**

用于在泛型中 修饰 泛型字母的；只有**泛型接口和泛型委托**能使用

## 知识点二 作用

### 返回值 和 参数

用out修饰的泛型 只能作为返回值

```C#
delegate T TestOut<out T>();
```

用in修饰的泛型 只能作为参数

```C#
delegate void TestIn<in T>(T t);
```

## 知识点二 作用（结合里氏替换原则理解）

协变 out：父类总是能被子类替换，允许**子类返回值**委托赋值给**父类返回值**委托。

out是修饰返回值的。

out修饰返回值类型，可以使得系统帮我们判断**out修饰的这个类型的委托**的**返回值**是否可以存储到父类委托当中。

如果不添加out修饰符，是不允许**子类返回值**委托赋值给**父类返回值**委托。的。

```C#
//这里声明了一个Son委托变量os，委托函数返回Son对象
TestOut<Son> os = () =>
{
    return new Son();
};
//然后声明了一个Father委托变量of = os；
//由于是out协变，允许子类委托赋值给父类委托
//因为里氏替换原则，父类可以装子类。
TestOut<Father> of = os;
//实际上 返回的 是os里面装的函数 返回的是Son
Father f = of();
```

逆变 int：父类总是能被子类替换，允许**父类参数委托**赋值给**子类参数委托**

in是修饰参数的。

in修饰返回值类型，可以使得系统帮我们判断**in修饰的这个类型的委托**的**参数**是否可以存储到子类委托当中。

如果不添加in修饰符，是不允许**父类参数委托**赋值给**子类参数委托**的

```C#
//这里声明了一个Father委托变量if，参数类型为Father
TestIn<Father> iF = (value) =>
{

};
//然后声明了一个Son委托变量is，参数类型为Son
//由于是in逆变，允许父类委托赋值给子类委托
//因为里氏替换原则，父类可以装子类
TestIn<Son> iS = iF;
iS(new Son());//实际上 调用的是 iF
```

## 总结

协变 out

逆变 in

用来修饰 泛型替代符的  只能修饰接口和委托中的泛型

作用两点

1. out修饰的泛型类型 只能作为返回值类型 in修饰的泛型类型 只能作为 参数类型
2. 遵循里氏替换原则的  用out和in修饰的 泛型委托 可以相互装载（有父子关系的泛型）
3. 协变  父类参数泛型委托装子类参数泛型委托    逆变 子类泛型返回值委托装父类泛型返回值委托

# 任务37：多线程 知识点

[C# 多线程的使用 - 简书 (jianshu.com)](https://www.jianshu.com/p/36a65838fe46)

[多线程篇-线程安全-原子性、可见性、有序性解析 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/142929863)

## 知识点一 了解线程前先了解进程

进程（Process）是计算机中的程序关于某数据集合上的一次运行活动

系统进行资源分配和调度的基本单位，是操作系统结构的基础

说人话：打开一个应用程序就是在操作系统上开启了一个进程

进程之间可以相互独立运行，互不干扰

进程之间也可以相互访问、操作

## 知识点二 什么是线程

操作系统能够进行运算调度的最小单位。

它被包含在进程之中，是进程中的实际运作单位

一条线程指的是进程中一个单一顺序的控制流，一个进程中可以并发多个线程

我们目前写的程序 都在主线程中

简单理解线程：就是代码从上到下运行的一条“管道”

## 知识点三 什么是多线程

我们可以通过代码 开启新的线程

可以同时运行代码的多条“管道” 就叫多线程

## 知识点四 语法相关

线程类 Thread

需要引用命名空间 using System.Threading;

### 1.声明一个新的线程

注意：线程执行的代码 需要封装到一个函数中

新线程 将要执行的代码逻辑 被封装到了一个函数语句块中

```C#
Thread t = new Thread(NewThreadLogic);	//这里的参数是一个函数
```

### 2.启动线程

```C#
t.Start();
```

### 3.设置为后台线程

当前台线程都结束了的时候,整个程序也就结束了,即使还有后台线程正在运行

后台线程不会防止应用程序的进程被终止掉

如果不设置为后台线程 可能导致进程无法正常关闭

```C#
t.IsBackground = true;
```

### 4.关闭释放一个线程

如果开启的线程中不是死循环 是能够结束的逻辑 那么 不用刻意的去关闭它

如果是死循环 想要中止这个线程 有两种方式

#### 4.1-死循环中bool标识

定义一个全局标记（isRuning），在主线程控制线程运行。

```C#
static void NewThreadLogic()
{
    //新开线程 执行的代码逻辑 在该函数语句块中
    while(isRuning)
    {
        //Thread.Sleep(1000);
        //Console.WriteLine("新开线程代码逻辑");
        lock(obj)
        {
            Console.SetCursorPosition(10, 5);
            Console.ForegroundColor = ConsoleColor.Yellow;
            Console.Write("■");
        }
    }
}
```

#### 4.2-通过线程提供的方法

[Thread.Abort 方法 (System.Threading) | Microsoft Learn](https://learn.microsoft.com/zh-cn/dotnet/api/system.threading.thread.abort?view=net-7.0#system-threading-thread-abort)

注意：在.Net core版本中无法中止 会报错

> 此方法已过时。 在 .NET 5 及更高版本上，调用此方法会生成编译时警告。 此方法在 .NET 5 及更高版本和 .NET Core 的运行时引发 [PlatformNotSupportedException](https://learn.microsoft.com/zh-cn/dotnet/api/system.platformnotsupportedexception?view=net-7.0) 。

```C#
//终止线程
try
{
    t.Abort();
    t = null;
}
catch
{

}
```

### 5.线程休眠

让线程休眠多少毫秒  1s = 1000毫秒

在哪个线程里执行 就休眠哪个线程

```C#
Thread.Sleep(1000);
```

## 知识点五 线程之间共享数据

多个线程使用的内存是共享的，都属于该应用程序(进程)

所以要注意 当多线程 同时操作同一片内存区域时可能会出问题

可以通过加锁的形式避免问题

lock：对于对象，加互斥锁。

当我们在多个线程当中想要访问同样的东西 进行逻辑处理时

为了避免不必要的逻辑顺序执行的差错

```C#
lock(引用类型对象)
```

```C#
while (true)
{
    lock(obj)
    {
        Console.SetCursorPosition(0, 0);
        Console.ForegroundColor = ConsoleColor.Red;
        Console.Write("●");
    }
}
```

## 知识点六 多线程对于我们的意义

可以用多线程专门处理一些复杂耗时的逻辑

比如 寻路、网络通信等等

## 总结

多线程是多个可以同时执行代码逻辑的“管道”

可以通过代码开启多线程，用多线程处理一些复杂的可能影响主线程流畅度的逻辑

关键字 Thread

# 任务39：预处理器指令 知识点

## 知识点一 什么是编译器

编译器是一种翻译程序

它用于将源语言程序翻译为目标语言程序

源语言程序：某种程序设计语言写成的,比如C#、C、C++、Java等语言写的程序

目标语言程序:二进制数表示的伪机器代码写的程序

## 知识点二 什么是预处理器指令

预处理器指令 指导编译器 在实际编译开始之前对信息进行预处理

预处理器指令 都是以#开始

预处理器指令不是语句，所以它们不以分号;结束

目前我们经常用到的 折叠代码块 就是预处理器指令

## 知识点三 常见的预处理器指令

### #define，#undef

#define定义一个符号，类似一个没有值的变量

#undef取消define定义的符号，让其失效

两者都是写在**脚本文件最前面**

一般配合 if指令使用 或配合特性

```c#
//定义一个符号
#define Unity4
#define Unity5
#define Unity2017
#define Unity2019
//取消定义一个符号
#undef Unity4

#define IOS
#define Android
#define PC
```

### #if，#elif，#else，#endif

和if语句规则一样，一般配合#define定义的符号使用

用于告诉编译器进行编译代码的流程控制

```C#
            //如果发现有Unity4这个符号 那么其中包含的代码 就会被编译器翻译
            //可以通过 逻辑或 和 逻辑与 进行多种符号的组合判断
#if Unity4
            Console.WriteLine("版本为Unity4");
#elif Unity2017 && IOS
            Console.WriteLine("版本为Unity2017");
            //#warning 这个版本 不合法
            //#error 这个版本不准执行
#else
            Console.WriteLine("其它版本");
#endif
```

### #warning，#error

告诉编译器，是报警告还是报错误，一般还是配合if使用

## 总结

预处理器指令

可以让代码还没有编译之前就可以进行一些预处理判断

在Unity中会用来进行一些平台或者版本的判断

决定不同的版本或者不同的平台使用不同的代码逻辑

# 任务41：反射概念和关键类Type 知识点

反射是Unity工作的基本原理之一

## 知识点一 什么是程序集

程序集是经由编译器编译得到的，供进一步编译执行的那个中间产物

在WINDOWS系统中，它一般表现为后缀为·dll（库文件）或者是·exe（可执行文件）的格式

说人话：

程序集就是我们写的一个代码集合，我们现在写的所有代码

最终都会被编译器翻译为一个程序集供别人使用

比如一个代码库文件（dll）或者一个可执行文件(exe)

## 知识点二 元数据

元数据就是用来描述数据的数据

这个概念不仅仅用于程序上，在别的领域也有元数据

说人话：

程序中的**类，类中的函数、变量**等等信息就是 程序的 元数据

有关程序以及类型的数据被称为 元数据，它们保存在程序集中

## 知识点三 反射的概念

程序正在运行时，可以查看其它程序集或者自身的元数据。

一个运行的程序查看本身或者其它程序的元数据的行为就叫做反射

说人话：

在程序运行时，通过反射可以得到其它程序集或者自己程序集代码的各种信息

类，函数，变量，对象等等，实例化它们，执行它们，操作它们

## 知识点四 反射的作用

因为反射可以在程序编译后获得信息，所以它提高了程序的拓展性和灵活性

1. 程序运行时得到所有元数据，包括元数据的特性
2. 程序运行时，实例化对象，操作对象
3. 程序运行时创建新对象，用这些对象执行任务

## 知识点五 语法相关

### Type

```C#
Type(类的信息类)
```

它是反射功能的基础！

它是访问元数据的主要方式。 

使用 Type 的成员获取有关类型声明的信息

有关类型的成员（如构造函数、方法、字段、属性和类的事件）

### 获取Type

注意：对于同一个类型，获取的Type（类型）**是唯一**的！

也就是说，无论你通过什么方式获取Type，获取到的Type变量都是同一个。

1.物之父object中的 **GetType()**可以获取对象的Type

```C#
int a = 42;
Type type = a.GetType();
Console.WriteLine(type);
```

2.通过**typeof(关键字)** 传入类名 也可以得到对象的Type

```C#
Type type2 = typeof(int);
Console.WriteLine(type2);
```

3.通过类的名字 也可以获取类型

注意：类名必须包含命名空间 不然找不到

```C#
Type type3 = Type.GetType("System.Int32");
Console.WriteLine(type3);
```

### 获取程序集

type.Assembly

```C#
//可以通过Type可以得到类型所在程序集信息
Console.WriteLine(type.Assembly);
Console.WriteLine(type2.Assembly);
Console.WriteLine(type3.Assembly);
```

### 获取类中的所有公共成员

```C#
//获取类中的所有公共成员
public MemberInfo[] GetMembers();
```

```C#
MemberInfo[] infos = t.GetMembers();
```

需要引用命名空间 using System.Reflection;

```C#
//首先得到Type
Type t = typeof(Test);
//然后得到所有公共成员
//需要引用命名空间 using System.Reflection;
MemberInfo[] infos = t.GetMembers();
for (int i = 0; i < infos.Length; i++)
{
    Console.WriteLine(infos[i]);
}
```

### 获取类的公共构造函数并调用

1.获取所有构造函数

```C#
ConstructorInfo[] ctors = t.GetConstructors();
for (int i = 0; i < ctors.Length; i++)
{
    Console.WriteLine(ctors[i]);
}
```

2.获取其中一个构造函数 并执行

```C#
//获取构造函数，types表示参数
public ConstructorInfo? GetConstructor(Type[] types);
```

2-1得到无参构造

```C#
//得构造函数传入 Type数组 数组中内容按顺序是参数类型
//执行构造函数传入  object数组 表示按顺序传入的参数
public object Invoke(object?[]? parameters);	//这是ConstructorInfo类的一个成员
//  2-1得到无参构造
ConstructorInfo info = t.GetConstructor(new Type[0]);
//执行无参构造 无参构造 没有参数 传null
Test obj = info.Invoke(null) as Test;
Console.WriteLine(obj.j);
```

注意，此时调用的Invoke，返回一个Object，所以需要as。

2-2得到有参构造

```C#
ConstructorInfo info2 = t.GetConstructor(new Type[] { typeof(int) });
//注意：Invoke函数需要传入的是Object类型的参数
obj = info2.Invoke(new object[] { 2 }) as Test;
Console.WriteLine(obj.str);

ConstructorInfo info3 = t.GetConstructor(new Type[] { typeof(int), typeof(string) });
//注意：Invoke函数需要传入的是Object类型的参数
obj = info3.Invoke(new object[] { 4, "444444" }) as Test;
Console.WriteLine(obj.str);
```

### 获取类的公共成员变量

1.得到所有成员变量

```C#
FieldInfo[] fieldInfos = t.GetFields();
for (int i = 0; i < fieldInfos.Length; i++)
{
    Console.WriteLine(fieldInfos[i]);
}
```

2.得到指定名称的公共成员变量

```C#
FieldInfo infoJ = t.GetField("j");
Console.WriteLine(infoJ);
```

3.通过反射获取和设置对象的值

```C#
Test test = new Test();
test.j = 99;
test.str = "2222";
```

3-1通过反射 获取对象的某个变量的值

```C#
Console.WriteLine(infoJ.GetValue(test));
```

3-2通过反射 设置指定对象的某个变量的值

```C#
infoJ.SetValue(test, 100);
Console.WriteLine(infoJ.GetValue(test));
```

### 获取类的公共成员方法

通过Type类中的 GetMethod方法 得到类中的方法

MethodInfo 是方法的反射信息

```C#
Type strType = typeof(string);
MethodInfo[] methods = strType.GetMethods();
for (int i = 0; i < methods.Length; i++)
{
    Console.WriteLine(methods[i]);
}
```

1.如果存在方法重载 用Type数组表示参数类型

```C#
MethodInfo subStr = strType.GetMethod("Substring",
                new Type[] { typeof(int), typeof(int) });
```

2.调用该方法

注意：如果是静态方法 Invoke中的第一个参数传null即可

```C#
string str = "Hello,World!";
//第一个参数 相当于 是哪个对象要执行这个成员方法
object result = subStr.Invoke(str, new object[] { 7, 5 });
Console.WriteLine(result);

object flag = methodEquals.Invoke(null, new Object[] {
    "11", "11"
});
Console.WriteLine((bool)flag);
//输出True
```

### 其它

```C#
//Type;
//得枚举
//GetEnumName
//GetEnumNames

//得事件
//GetEvent
//GetEvents

//得接口
//GetInterface
//GetInterfaces

//得属性
//GetProperty
//GetPropertys
//等等
```

# 任务42：关键类Assembly和Activator 知识点

## Activator

用于快速实例化对象的类

用于将Type对象快捷实例化为对象

先得到Type

然后 快速实例化一个对象

```C#
//1.无参构造
Test testObj = Activator.CreateInstance(testType) as Test;
Console.WriteLine(testObj.str);
//2.有参数构造
testObj = Activator.CreateInstance(testType, 99) as Test;
Console.WriteLine(testObj.j);

testObj = Activator.CreateInstance(testType, 55, "111222") as Test;
Console.WriteLine(testObj.j);
```

主要是通过CreateInstance方法，快捷创建一个对象的实例。

```C#
public static object? CreateInstance(Type type, params object?[]? args);
//注意，我们必须在使用时使得构造函数的参数匹配，不然会报错
```

## Assembly

程序集类

主要用来加载其它程序集，加载后，才能用Type来使用其它程序集中的信息。

如果想要使用不是自己程序集中的内容 需要先加载程序集，比如 dll文件(库文件)。

dll：简单的把库文件看成一种代码仓库，它提供给使用者一些可以直接拿来用的变量、函数或类

### 三种加载程序集的函数

一般用来加载在同一文件下的其它程序集

```C#
Assembly asembly2 = Assembly.Load("程序集名称");
```

一般用来加载不在同一文件下的其它程序集

```C#
Assembly asembly = Assembly.LoadFrom("包含程序集清单的文件的名称或路径");
Assembly asembly3 = Assembly.LoadFile("要加载的文件的完全限定路径");
```

### 加载过程

1.先加载一个指定程序集

```C#
Assembly asembly = Assembly.LoadFrom(@"C:\Users\MECHREVO\Desktop\CSharp进阶教学\Lesson18_练习题\bin\Debug\netcoreapp3.1\Lesson18_练习题");
Type[] types = asembly.GetTypes();
for (int i = 0; i < types.Length; i++)
{
    Console.WriteLine(types[i]);
}
```

2.在加载程序集中的一个类对象 之后才能使用反射

```C#
Type icon = asembly.GetType("Lesson18_练习题.Icon");
MemberInfo[] members = icon.GetMembers();
for (int i = 0; i < members.Length; i++)
{
    Console.WriteLine(members[i]);
}
```

通过反射 实例化一个 icon对象

```C#
Type moveDir = asembly.GetType("Lesson18_练习题.E_MoveDir");
FieldInfo right = moveDir.GetField("Right");
```

直接实例化对象

```C#
object iconObj = Activator.CreateInstance(icon, 10, 5, right.GetValue(null));
```

得到对象中的方法 通过反射

```C#
MethodInfo move = icon.GetMethod("Move");
MethodInfo draw = icon.GetMethod("Draw");
MethodInfo clear = icon.GetMethod("Clear");
```

## 类库工程创建

我们可以自己创建类库，编译后，将生成dll文件。

我们可以直接引用dll文件，或者通过反射获取。

# 任务44：特性 知识点

## 知识点一 特性是什么

特性是一种允许我们向程序的程序集添加元数据的语言结构

它是用于保存程序结构信息的某种特殊类型的类

特性提供功能强大的方法以将声明信息与 C# 代码（类型、方法、属性等）相关联。

特性与程序实体关联后，即可在运行时使用反射查询特性信息

特性的目的是告诉编译器把程序结构的某组元数据嵌入程序集中

它可以放置在几乎所有的声明中（类、变量、函数等等申明）

说人话：特性本质是个类，我们可以利用特性类为元数据添加额外信息

比如一个类、成员变量、成员方法等等为他们添加更多的额外信息

之后可以通过反射来获取这些额外信息

## 知识点二 自定义特性

特性实质就是一个类，所以，只需要再声明类时继承Attribute基类，那么这个类就是一个特性。

特性命名规范：特性名Attribute

```C#
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Field, AllowMultiple = true, Inherited = false)]
//注意，类名中的Attribute在使用时可以省略,但是typeof时不能省略
//继承特性基类 Attribute
class MyCustomAttribute : Attribute
{
    //特性中的成员 一般根据需求来写
    public string info;

    public MyCustomAttribute(string info)
    {
        this.info = info;
    }

    public void TestFun()
    {
        Console.WriteLine("特性的方法");
    }
}
```

## 知识点三 特性的使用

### 基本语法

```C#
//[特性名(参数列表)]
//本质上 就是在调用特性类的构造函数
```

写在哪里？

类、函数、变量上一行，表示他们具有该特性信息

```C#
[MyCustom("这个是我自己写的一个用于计算的类")]
[MyCustom("这个是我自己写的一个用于计算的类")]
class MyClass
{
    [MyCustom("这是一个成员变量")]
    public int value;

    //[MyCustom("这是一个用于计算加法的函数")]
    //public void TestFun( [MyCustom("函数参数")]int a )
    //{

    //}
    public void TestFun(int a)
    {

    }
}
```

### 判断是否使用了某个特性

参数一：特性的类型

参数二：代表是否搜索继承链（属性和事件忽略此参数）

```C#
if( t.IsDefined(typeof(MyCustomAttribute), false) )
{
    Console.WriteLine("该类型应用了MyCustom特性");
}
```

### 获取Type元数据中的所有特性

```C#
object[] array = t.GetCustomAttributes(true);
for (int i = 0; i < array.Length; i++)
{
    if( array[i] is MyCustomAttribute )
    {
        Console.WriteLine((array[i] as MyCustomAttribute).info);
        (array[i] as MyCustomAttribute).TestFun();
    }
}
```

## 知识点四 限制自定义特性的使用范围

通过为特性类 加特性 限制其使用范围

```C#
[AttributeUsage(AttributeTargets.Class | AttributeTargets.Struct, AllowMultiple = true, Inherited = true)]
```

参数一：AttributeTargets —— 特性能够用在哪些地方

参数二：AllowMultiple —— 是否允许多个特性实例用在同一个目标上

参数三：Inherited —— 特性是否能被派生类和重写成员继承

## 知识点五 系统自带特性——过时特性

过时特性：Obsolete

用于提示用户 使用的方法等成员已经过时 建议使用新方法

一般加在函数前的特性

```c#
public ObsoleteAttribute(string? message, bool error);
```

```C#
//参数一：调用过时方法时 提示的内容
//参数二：true-使用该方法时会报错  false-使用该方法时直接警告
[Obsolete("OldSpeak方法已经过时了，请使用Speak方法", false)]
public void OldSpeak(string str)
{
    Console.WriteLine(str);
}
```

## 知识点六 系统自带特性——调用者信息特性

需要引用命名空间 using System.Runtime.CompilerServices;

哪个文件调用？

CallerFilePath特性

哪一行调用？

CallerLineNumber特性

哪个函数调用？

CallerMemberName特性

一般作为函数参数的特性

```C#
public void SpeakCaller(string str, [CallerFilePath]string fileName = "", 
                        [CallerLineNumber]int line = 0, 
                        [CallerMemberName]string target = "")
{
    //可以直接打印这些信息
    Console.WriteLine(str);
    Console.WriteLine(fileName);
    Console.WriteLine(line);
    Console.WriteLine(target);
}
```

## 知识点七 系统自带特性——条件编译特性

条件编译特性：Conditional

它会和预处理指令 #define配合使用

需要引用命名空间using System.Diagnostics;

主要可以用在一些调试代码上

有时想执行有时不想执行的代码

**只有define了conditionString，被特性修饰的东西才能执行**

```C#
public ConditionalAttribute(string conditionString);
```

## 知识点八 系统自带特性——外部Dll包函数特性

DllImport

用来标记非.Net(C#)的函数，表明该函数在一个外部的DLL中定义。

一般用来调用 C或者C++的Dll包写好的方法

需要引用命名空间 using System.Runtime.InteropServices

```C#
public DllImportAttribute(string dllName);
```

## 总结

特性是用于 为元数据再添加更多的额外信息（变量、方法等等）

我们可以通过反射获取这些额外的数据 来进行一些特殊的处理

自定义特性——继承**Attribute**类

系统自带特性：过时特性等

为什么要学习特性

Unity引擎中很多地方都用到了特性来进行一些特殊处理

# 任务46：迭代器 知识点

迭代器一定是可迭代对象。迭代器要求实现movenext方法。可迭代对象要求实现getIEnumerator方法，getIEnumerator方法返回的是该对象的迭代器。迭代器不负责维护可迭代对象的数据信息，只负责维护读取数据的位置。所以就是工厂和螺丝钉的关系

## 知识点一 迭代器是什么

迭代器（iterator）有时又称光标（cursor）

是程序设计的软件设计模式

迭代器模式提供一个方法顺序访问一个聚合对象中的各个元素

而又不暴露其内部的标识

在表现效果上看

是可以在容器对象（例如链表或数组）上遍历访问的接口

设计人员无需关心容器对象的内存分配的实现细节

可以用foreach遍历的类，都是实现了迭代器的

## 知识点二 标准迭代器的实现方法

关键接口：IEnumerator,IEnumerable

命名空间：using System.Collections;

可以通过同时继承IEnumerable和IEnumerator实现其中的方法

### IEnumerator

IEnumerator就是迭代器接口，拥有三个函数，用来实现遍历操作。

```C#
public interface IEnumerator
{
    //获取当前元素
    object? Current { get; }
    //检测下一个元素是否存在，如果不存在则不可继续遍历
    bool MoveNext();
    //重置下标
    void Reset();
}
```

### IEnumerable

IEnumerable的作用是获取IEnumerator，并重置下标。

一般Reset函数在GetEnumerator()中调用。

```C#
public interface IEnumerable {
    //获取迭代器，并且重置迭代器
    IEnumerator GetEnumerator();
}
```

### foreach本质

```C#
foreach (var item in list) { }
```

1. 先获取in后面这个对象的 IEnumerator，会调用对象其中的GetEnumerator方法 来获取
2. 执行得到这个IEnumerator对象中的 MoveNext方法
3. 只要MoveNext方法的返回值时true 就会去得到Current，然后复制给 item

### 标准迭代器的实现方法

标准迭代器的实现方法，其实就是实现IEnumerator，IEnumerable这两个接口。

注意：下标最开始应该是-1，因为开始遍历时，就会调用一次MoveNext();

```C#
class CustomList : IEnumerable, IEnumerator
{
    private int[] list;
    //从-1开始的光标 用于表示 数据得到了哪个位置
    private int position = -1;

    public CustomList()
    {
        list = new int[] { 1, 2, 3, 4, 5, 6, 7, 8 };
    }

    #region IEnumerable
    public IEnumerator GetEnumerator()
    {
        Reset();
        return this;
    }
    #endregion

    public object Current
    {
        get
        {
            return list[position];
        }
    }
    public bool MoveNext()
    {
        //移动光标
        ++position;
        //是否溢出 溢出就不合法
        return position < list.Length;
    }

    //reset是重置光标位置 一般写在获取 IEnumerator对象这个函数中
    //用于第一次重置光标位置
    public void Reset()
    {
        position = -1;
    }
}
```

## 知识点三 用yield return 语法糖实现迭代器

### yield return

yield return 是C#提供给我们的语法糖

所谓语法糖，也称糖衣语法

主要作用就是将复杂逻辑简单化，可以增加程序的可读性

从而减少程序代码出错的机会

在执行

```C#
yield return item;
```

之后，程序会返回之前调用的函数，当需要再次获取item时，又会回到yield return然后返回下一个元素。

### 用yield return 语法糖实现迭代器

关键接口：IEnumerable

命名空间：using System.Collections;

让想要通过foreach遍历的自定义类**只需要**实现接口中的方法GetEnumerator即可

```C#
class CustomList2 : IEnumerable
{
    private int[] list;

    public CustomList2()
    {
        list = new int[] { 1, 2, 3, 4, 5, 6, 7, 8 };
    }

    public IEnumerator GetEnumerator()
    {
        for (int i = 0; i < list.Length; i++)
        {
            //yield关键字 配合迭代器使用
            //可以理解为 暂时返回 保留当前的状态
            //一会还会在回来
            //C#的语法糖
            yield return list[i];
        }
        //yield return list[0];
        //yield return list[1];
        //yield return list[2];
        //yield return list[3];
        //yield return list[4];
        //yield return list[5];
        //yield return list[6];
        //yield return list[7];
    }
}
```

## 知识点四 用yield return 语法糖为泛型类实现迭代器

```C#
class CustomList<T> : IEnumerable
{
    private T[] array;

    public CustomList(params T[] array)
    {
        this.array = array;
    }

    public IEnumerator GetEnumerator()
    {
        for (int i = 0; i < array.Length; i++)
        {
            yield return array[i];
        }
    }
}
```

## 总结

迭代器就是可以让我们在外部直接通过foreach遍历对象中元素而不需要了解其结构

主要的两种方式

1. 传统方式 继承两个接口 实现里面的方法
2. 用语法糖 yield return 去返回内容 只需要继承一个接口即可

# 任务48：特殊语法 知识点

## 知识点一 var隐式类型

> 其实就是Cpp的auto

var是一种特殊的变量类型

它可以用来表示任意类型的变量

注意：

1. var不能作为类的成员 只能用于临时变量声明时，也就是 一般写在函数语句块中
2. var必须初始化（因为需要类型推导）

```C#
var i = 5;
var s = "123";
var array = new int[] { 1, 2, 3, 4 };
var list = new List<int>();
```

## 知识点二 设置对象初始值，大括号初始化法

声明对象时，可以通过直接写大括号的形式初始化公共成员变量和属性

```C#
Person p = new Person(100) { sex = true, Age = 18, Name = "唐老狮" };
Person p2 = new Person(200) { Age = 18 };
```

## 知识点三 设置集合初始值

声明集合对象时，也可以通过大括号 直接初始化内部属性

```C#
int[] array2 = new int[] { 1, 2, 3, 4, 5 };

List<int> listInt = new List<int>() { 1, 2, 3, 4, 5, 6 };

List<Person> listPerson = new List<Person>() {
    new Person(200),
    new Person(100){Age = 10},
    new Person(1){sex = true, Name = "唐老狮"}
};

Dictionary<int, string> dic = new Dictionary<int, string>()
{
    { 1, "123" },
    { 2, "222"}
};
```

## 知识点四 匿名类型

var 变量可以申明为自定义的匿名类型

```C#
var v = new { age = 10, money = 11, name = "小明" };
Console.WriteLine(v.age);
Console.WriteLine(v.name);
```

## 知识点五 可空类型

[C#中 ??、 ?、 ?: 、?.、?[ \] 问号 - 幽冥狂_七 - 博客园 (cnblogs.com)](https://www.cnblogs.com/youmingkuang/p/11459615.html)

1.值类型是不能赋值为 空的

```C#
int c = null;	//error
```

2.申明时 在值类型后面加? 可以赋值为空

```C#
int? c = 3;
```

3.判断是否为空

```C#
if( c.HasValue )
{
    Console.WriteLine(c);
    Console.WriteLine(c.Value);
}
```

4.安全获取可空类型值

4-1.如果为空 默认返回值类型的默认值

```C#
Console.WriteLine(value.GetValueOrDefault());
```

4-2.也可以指定一个默认值

```C#
Console.WriteLine(value.GetValueOrDefault(100));
```

### ?.，?[]

先检测对象是否为空，再执行方法

相当于是一种语法糖 能够帮助我们自动去判断o是否为空

```C#
//如果obj不为空，就执行ToString()
obj?.ToString();
//如果obj不为空，就执行[]
obj?[0];
```

## 知识点六 空合并操作符

空合并操作符 ??

语法：左边值 ?? 右边值

语义：如果左边值为null 就返回右边值 否则返回左边值

只要是可以为null的类型都能用

是三目运算符的一种特殊缩略写法。

```C#
int? intV = null;
//int intI = intV == null ? 100 : intV.Value;
int intI = intV ?? 100;
Console.WriteLine(intI);

string str = null;
str = str ?? "hahah";
Console.WriteLine(str);
```

## 知识点七 内插字符串

关键符号：$

用$来构造字符串，让字符串中可以拼接变量

```C#
string name = "唐老狮";
int age = 18;
Console.WriteLine($"好好学习,{name},年龄：{age}");
```

## 知识点八 单句逻辑简略写法

当循环或者if语句中只有 一句代码时 大括号可以省略

```C#
if (true)
    Console.WriteLine("123123");

for (int j = 0; j < 10; j++)
    Console.WriteLine(j);

while (true)
    Console.WriteLine("123123");
```

# 任务49：值和引用类型补充

## 知识回顾

值类型
无符号:byte,ushort,uint,ulong
有符号:sbyte,short,int,long
浮点数:float,double,decimal
特殊:char,bool
枚举:enum
结构体 :struct

引用类型：string，数组，class，interface，委托

值类型和引用类型的本质区别：值的具体内容存在栈内存上；引用的具体内容存在堆内存上

## 问题一 如何判断 值类型和引用类型

F12进到类型的内部去查看

是class就是引用

是struct就是值

## 问题二 语句块

语句块一共有以下几种：

命名空间
↓
类、接口、结构体
↓
函数、属性、索引器、运算符重载等（类、接口、结构体）
↓
条件分支、循环

上层语句块：类、结构体
中层语句块：函数
底层的语句块： 条件分支 循环等

我们的逻辑代码写在哪里？
函数、条件分支、循环 - 中底层语句块中

我们的变量可以申明在哪里？
上、中、底都能申明变量
上层语句块中：成员变量
中、底层语句块中：临时变量

## 问题三 变量的生命周期

编程时大部分都是 临时变量，在中底层申明的临时变量（函数、条件分支、循环语句块等）

语句块执行结束，没有被记录的对象将被回收或变成垃圾

值类型：被系统自动回收

引用类型：栈上用于存地址的房间被系统自动回收，堆中具体内容变成垃圾，待下次GC回收

想要不被回收或者不变垃圾，则必须将其记录下来

如何记录？

在更高层级记录或者，使用静态全局变量记录

## 问题四 结构体中的值和引用

结构体本身是值类型
前提：该结构体没有做为其它类的成员
在结构体中的值，栈中存储值具体的内容
在结构体中的引用，堆中存储引用具体的内容

引用类型始终存储在堆中，真正通过结构体使用其中引用类型时只是顺藤摸瓜

## 问题五 类中的值和引用

类本身是引用类型
在类中的值，堆中存储具体的值（托管值类型）
在类中的引用，堆中存储具体的值

值类型跟着大哥走，引用类型一根筋

## 问题六 数组中的存储规则

数组本身是引用类型

值类型数组，堆中房间存具体内容

引用类型数组，堆中房间存地址

## 问题七 结构体继承接口

利用里氏替换原则，用接口容器装载结构体存在装箱拆箱

```C#
TestStruct obj1 = new TestStruct();
obj1.Value = 1;
Console.WriteLine(obj1.Value);
TestStruct obj2 = obj1;
obj2.Value = 2;
//由于是值类型，obj1.value不会改变
Console.WriteLine(obj1.Value);
Console.WriteLine(obj2.Value);

ITest iObj1 = obj1;//装箱  value 1
ITest iObj2 = iObj1;
iObj2.Value = 99;
//由于是引用类型，iobj1.value会变成99
Console.WriteLine(iObj1.Value);
Console.WriteLine(iObj2.Value);

TestStruct obj3 = (TestStruct)iObj1;//拆箱
```

# 任务50：插入排序

## 知识点一 插入排序的基本原理

8 7 1 5 4 2 6 3 9
两个区域
排序区
未排序区
用一个索引值做分水岭

未排序区元素
与排序区元素比较
插入到合适位置
直到未排序区清空

## 知识点二 代码实现

```C#
//实现升序 把 大的 放在最后面
int[] arr = new int[] { 8, 7, 1, 5, 4, 2, 6, 3, 9 };

//前提规则
//排序开始前
//首先认为第一个元素在排序区中
//其它所有元素在未排序区中

//排序开始后
//每次将未排序区第一个元素取出用于和
//排序区中元素比较(从后往前)
//满足条件（较大或者较小）
//则排序区中元素往后移动一个位置。

//注意
//所有数字都在一个数组中
//所谓的两个区域是一个分水岭索引

//第一步
//能取出未排序区的所有元素进行比较
//i=1的原因：默认第一个元素就在排序区
for (int i = 1; i < arr.Length; i++)
{
    //第二步
    //每一轮
    //1.取出排序区的最后一个元素索引
    int sortIndex = i - 1;
    //2.取出未排序区的第一个元素
    int noSortNum = arr[i];
    //第三步
    //在未排序区进行比较
    //移动位置
    //确定插入索引
    //循环停止的条件
    //1.发现排序区中所有元素都已经比较完
    //2.发现排序区中的元素不满足比较条件了
    while (sortIndex >= 0 &&
           arr[sortIndex] > noSortNum)
    {
        //只要进了这个while循环 证明满足条件
        //排序区中的元素 就应该往后退一格
        arr[sortIndex + 1] = arr[sortIndex];
        //移动到排序区的前一个位置 准备继续比较
        --sortIndex;
    }
    //最终插入数字
    //循环中知识在确定位置 和找最终的插入位置
    //最终插入对应位置 应该循环结束后
    arr[sortIndex + 1] = noSortNum;
}

for (int i = 0; i < arr.Length; i++)
{
    Console.WriteLine(arr[i]);
}
```

```C#
int[] nums = new int[] { 3, 5, 6, 9, 0, 1, 2, 4, 6, 8 };
for (int i = 1; i < nums.Length; ++i)
{
    int sortedIndex = i - 1;
    int nowSortNum = nums[i];
    while (sortedIndex >= 0 && nums[sortedIndex] > nowSortNum)
    {
        nums[sortedIndex + 1] = nums[sortedIndex];
        --sortedIndex;
    }
    nums[sortedIndex + 1] = nowSortNum;
}
foreach (var item in nums)
{
    Console.Write(item + " ");

}
```

## 知识点三 总结

### 为什么有两层循环？

第一层循环：一次取出未排序区的元素进行排序
第二层循环：找到想要插入的位置

### 为什么第一层循环从1开始遍历？

插入排序的关键是分两个区域，已排序区 和 未排序区，默认第一个元素在已排序区

### 为什么使用while循环？

满足条件才比较
否则证明插入位置已确定
不需要继续循环

### 为什么可以直接往后移位置

每轮未排序数已记录

最后一个位置不怕丢

### 为什么确定位置后,是放在sortIndex + 1的位置

当循环停止时，插入位置应该是停止循环的索引加1处

### 基本原理

两个区域
用索引值来区分
未排序区与排序区
元素不停比较
找到合适位置
插入当前元素

### 套路写法

两层循环
一层获取未排序区元素
一层找到合适插入位置

### 注意事项

默认（假设）开头已排序，其实一个元素，就是有序的。
第二层循环外插入

# 任务51：希尔排序

## 知识点一 希尔排序的基本原理

希尔排序是，插入排序的升级版，必须先掌握插入排序

希尔排序的原理：将整个待排序序列，分割成为若干子序列，分别进行插入排序

总而言之：

希尔排序对插入排序的升级主要就是加入了一个步长的概念，通过步长每次可以把原序列分为多个子序列；对子序列进行插入排序，在极限情况下可以有效降低普通插入排序的时间复杂度，提升算法效率。

## 知识点二 代码实现

```C#
int[] arr = new int[] { 8, 7, 1, 5, 4, 2, 6, 3, 9 };
//学习希尔排序的前提条件 
//先掌握插入排序
//第一步：实现插入排序
//第一层循环 是用来取出未排序区中的元素的
//for (int i = 1; i < arr.Length; i++)
//{
//    //得出未排序区的元素
//    int noSortNum = arr[i];
//    //得出排序区中最后一个元素索引
//    int sortIndex = i - 1;
//    //进入条件
//    //首先排序区中还有可以比较的 >=0
//    //排序区中元素 满足交换条件 升序就是排序区中元素要大于未排序区中元素
//    while (sortIndex >= 0 &&
//        arr[sortIndex] > noSortNum)
//    {
//        arr[sortIndex + 1] = arr[sortIndex];
//        --sortIndex;
//    }
//    //找到位置过后 真正的插入 值
//    arr[sortIndex + 1] = noSortNum;
//}

//for (int i = 0; i < arr.Length; i++)
//{
//    Console.WriteLine(arr[i]);
//}

//第二步：确定步长
//基本规则：每次步长变化都是/2
//一开始步长 就是数组的长度/2
//之后每一次 都是在上一次的步长基础上/2
//结束条件是 步长 <=0 
//1.第一次的步长是数组长度/2  所以：int step = arr.length/2
//2.之后每一次步长变化都是/2  索引：step /= 2
//3.最小步长是1  所以：step > 0
for (int step = arr.Length / 2; step > 0; step/=2)
{
    //注意：
    //每次得到步长后 会把该步长下所有序列都进行插入排序

    //第三步：执行插入排序
    //i=1代码 相当于 代表取出来的排序区的第一个元素
    //for (int i = 1; i < arr.Length; i++)
    //i=step 相当于 代表取出来的排序区的第一个元素
    for (int i = step; i < arr.Length; i++)
    {
        //得出未排序区的元素
        int noSortNum = arr[i];
        //得出排序区中最后一个元素索引
        //int sortIndex = i - 1;
        //i-step 代表和子序列中 已排序区元素一一比较
        int sortIndex = i - step;
        //进入条件
        //首先排序区中还有可以比较的 >=0
        //排序区中元素 满足交换条件 升序就是排序区中元素要大于未排序区中元素
        while (sortIndex >= 0 &&
               arr[sortIndex] > noSortNum)
        {
            //arr[sortIndex + 1] = arr[sortIndex];
            // 代表移步长个位置 代表子序列中的下一个位置
            arr[sortIndex + step] = arr[sortIndex];
            //--sortIndex;
            //一个步长单位之间的比较
            sortIndex -= step;
        }
        //找到位置过后 真正的插入 值
        //arr[sortIndex + 1] = noSortNum;
        //现在是加步长个单位
        arr[sortIndex + step] = noSortNum;
    }
}
```

```C#
int[] nums = new int[] { 3, 5, 6, 9, 0, 1, 2, 4, 6, 8 };
for (int step = nums.Length / 2; step > 0; step /= 2)
{
    for (int i = step; i < nums.Length; i += step)
    {
        int sortedIndex = i - step;
        int nowSortNum = nums[i];
        while (sortedIndex >= 0 && nowSortNum > nums[sortedIndex])
        {
            nums[sortedIndex + step] = nums[sortedIndex];
            sortedIndex -= step;
        }
        nums[sortedIndex + step] = nowSortNum;
    }
}
```

## 知识点三 总结

### 基本原理

设置步长
步长不停缩小
到1排序后结束

### 具体排序方式

插入排序原理

### 套路写法

三层循环
一层获取步长
一层获取未排序区元素
一层找到合适位置插入

### 注意事项

步长确定后
会将所有子序列进行插入排序

# 任务52：归并排序

## 知识点一 归并排序基本原理

归并 = 递归 + 合并

数组分左右
左右元素相比较
满足条件放入新数组
一侧用完放对面

递归不停分
分完再排序
排序结束往上走
边走边合并
走到头顶出结果

归并排序分成两部分
1.基本排序规则
2.递归平分数组

递归平分数组：
不停进行分割
长度小于2停止
开始比较
一层一层向上比

基本排序规则：
左右元素进行比较
依次放入新数组中
一侧没有了另一侧直接放入新数组

## 知识点二 代码实现

### 唐老狮做法

```C#
//第一步：
//基本排序规则
//左右元素相比较
//满足条件放进去
//一侧用完直接放
public static int[] Sort(int[] left, int[] right)
{
    //先准备一个新数组
    int[] array = new int[left.Length + right.Length];
    int leftIndex = 0;//左数组索引
    int rightIndex = 0;//右数组索引

    //最终目的是要填满这个新数组
    //不会出现两侧都放完还在进循环 
    //因为这个新数组的长度 是根据左右两个数组长度计算出来的
    for (int i = 0; i < array.Length; i++)
    {
        //左侧放完了 直接放对面右侧
        if( leftIndex >= left.Length )
        {
            array[i] = right[rightIndex];
            //已经放入了一个右侧元素进入新数组
            //所以 标识应该指向下一个嘛
            rightIndex++;
        }
        //右侧放完了 直接放对面左侧
        else if( rightIndex >= right.Length )
        {
            array[i] = left[leftIndex];
            //已经放入了一个左侧元素进入新数组
            //所以 标识应该指向下一个嘛
            leftIndex++;
        }
        else if( left[leftIndex] < right[rightIndex] )
        {
            array[i] = left[leftIndex];
            //已经放入了一个左侧元素进入新数组
            //所以 标识应该指向下一个嘛
            leftIndex++;
        }
        else
        {
            array[i] = right[rightIndex];
            //已经放入了一个右侧元素进入新数组
            //所以 标识应该指向下一个嘛
            rightIndex++;
        }
    }

    //得到了新数组 直接返回出去
    return array;
}

//第二步：
//递归平分数组
//结束条件为长度小于2

public static int[] Merge(int[] array)
{
    //递归结束条件
    if (array.Length < 2)
        return array;
    //1.数组分两段  得到一个中间索引
    int mid = array.Length / 2;
    //2.初始化左右数组
    //左数组
    int[] left = new int[mid];
    //右数组
    int[] right = new int[array.Length - mid];
    //左右初始化内容
    for (int i = 0; i < array.Length; i++)
    {
        if (i < mid)
            left[i] = array[i];
        else
            right[i - mid] = array[i];
    }
    //3.递归再分再排序
    return Sort(Merge(left), Merge(right));
}
```

### 更简洁的做法

```C#
public static void MergeSort(int[] nums, int left, int right)
{
    if (left < right)
    {
        int center = left + (right - left) / 2;
        MergeSort(nums, left, center);
        MergeSort(nums, center + 1, right);
        Merge(nums, left, right);
    }
}

public static void Merge(int[] nums, int left, int right)
{
    int center = left + (right - left) / 2;
    int leftIndex = left;
    int rightIndex = center + 1;
    int index = 0;
    int[] tempNums = new int[right - left + 1];
    while (leftIndex <= center && rightIndex <= right)
    {
        if (nums[leftIndex] < nums[rightIndex])
        {
            tempNums[index++] = nums[leftIndex++];
        }
        else
        {
            tempNums[index++] = nums[rightIndex++];
        }
    }
    while (leftIndex <= center)
    {
        tempNums[index++] = nums[leftIndex++];
    }
    while (rightIndex <= right)
    {
        tempNums[index++] = nums[rightIndex++];
    }
    for (int i = 0; i < tempNums.Length; ++i)
    {
        nums[left++] = tempNums[i];
    }
}
```

## 知识点三 总结

理解递归逻辑
一开始不会执行Sort函数的
要先找到最小容量数组时
才会回头递归调用Sort进行排序

基本原理
归并 = 递归 + 合并
数组分左右
左右元素相比较
一侧用完放对面
不停放入新数组

**递归不停分**
**分完再排序**
**排序结束往上走**
**边走边合并**
**走到头顶出结果**

套路写法
两个函数
一个基本排序规则
一个递归平分数组

注意事项
排序规则函数 在 平分数组函数
内部 return调用

# 任务53：快速排序

## 知识点一 快速排序基本原理

选取基准
产生左右标识
左右比基准
满足则换位

排完一次
基准定位

左右递归
直到有序

## 知识点二 代码实现

快速排序是不稳定排序

[为什么快速排序是不稳定的_d4shman的博客-CSDN博客_快排是稳定排序吗](https://blog.csdn.net/wusuopubupt/article/details/22743315)

### 唐老狮写法

有bug，数组有相同元素的情况下，会死循环。

在查找时加<=解决

```C#
//第一步：
//申明用于快速排序的函数
public static void QuickSort(int[] array, int left, int right)
{
    //第七步：
    //递归函数结束条件
    if (left >= right)
        return;

    //第二步：
    //记录基准值
    //左游标
    //右游标
    int tempLeft, tempRight, temp;
    temp = array[left];
    tempLeft = left;
    tempRight = right;
    //第三步：
    //核心交换逻辑
    //左右游标会不同变化 要不相同时才能继续变化
    while(tempLeft != tempRight)
    {
        //第四步：比较位置交换
        //首先从右边开始 比较 看值有没有资格放到表示的右侧
        while (tempLeft < tempRight &&
               array[tempRight] > temp)
        {
            tempRight--;
        }
        //移动结束证明可以换位置
        array[tempLeft] = array[tempRight];

        //上面是移动右侧游标
        //接着移动完右侧游标 就要来移动左侧游标
        while (tempLeft <= tempRight &&
               array[tempLeft] < temp)
        {
            tempLeft++;
        }
        //移动结束证明可以换位置
        array[tempRight] = array[tempLeft];
    }
    //第五步：放置基准值
    //跳出循环后 把基准值放在中间位置
    //此时tempRight和tempLeft一定是相等的
    array[tempRight] = temp;

    //第六步：
    //递归继续
    QuickSort(array, left, tempRight - 1);
    QuickSort(array, tempLeft + 1, right);
}
```

### 优化写法

```C#
public static void QuickSort(int[] nums)
{
    RandonPatition(nums, 0, nums.Length - 1);
}

public static void RandonPatition(int[] nums, int left, int right)
{
    Random r = new Random();
    if (left < right)
    {
        int mark = r.Next(left, right + 1);
        int temp = nums[left];
        nums[left] = nums[mark];
        nums[mark] = temp;
        int index = Patition(nums, left, right);
        RandonPatition(nums, left, index - 1);
        RandonPatition(nums, index + 1, right);
    }
}

public static int Patition(int[] nums, int left, int right)
{
    int benchMark = nums[left];
    while (left != right)
    {
        while (left < right && nums[right] <= benchMark)
        {
            --right;
        }
        nums[left] = nums[right];
        while (left < right && nums[left] > benchMark)
        {
            ++left;
        }
        nums[right] = nums[left];
    }
    nums[right] = benchMark;
    return right;
}
```

# 任务54：堆排序

## 知识点一 堆排序基本原理

构建二叉树，大堆顶调整，堆顶往后方，不停变堆顶

关键规则：最大非叶子节点是 数组长度 / 2 - 1

父节点和叶子节点：父节点为i，左节点2i+1，右节点2i+2

## 知识点二 代码实现

堆排序的精髓在于，利用数组长度这个参数，每次对其他元素进行HeapCompare

使得每次排序，忽略最大/最小的元素，已达到排序的效果

### 唐老狮写法

```C#
//第一步：实现父节点和左右节点比较
/// <summary>
///
/// </summary>
/// <param name="array">需要排序的数组</param>
/// <param name="nowIndex">当前作为根节点的索引</param>
/// <param name="arrayLength">固定一个位置,那么长度就会减去1,是没有确定位置的数组元素长度</param>
static void HeapCompare(int[] array, int nowIndex, int arrayLength)
{
    //通过传入的索引 得到它对应的左右叶子节点的索引
    //可能算出来的会溢出数组的索引 我们一会再判断
    int left = 2 * nowIndex + 1;
    int right = 2 * nowIndex + 2;
    //用于记录较大数的索引
    int biggerIndex = nowIndex;
    //先比左 再比右
    //不能溢出
    if (left < arrayLength && array[left] > array[biggerIndex])
    {
        //认为目前最大的是左节点 记录索引
        biggerIndex = left;
    }
    //比较右节点
    if (right < arrayLength && array[right] > array[biggerIndex])
    {
        biggerIndex = right;
    }
    //如果比较过后 发现最大索引发生变化了 那就以为这要换位置了
    if (biggerIndex != nowIndex)
    {
        int temp = array[nowIndex];
        array[nowIndex] = array[biggerIndex];
        array[biggerIndex] = temp;
        //通过递归 看是否影响了叶子节点他们的三角关系
        HeapCompare(array, biggerIndex, arrayLength);
    }
}
//第二步：构建大堆顶
static void BuildBigHeap(int[] array)
{
    //从最大的非叶子节点索引 开始 不停的往前 去构建大堆顶
    for (int i = array.Length / 2 - 1; i >= 0; i--)
    {
        HeapCompare(array, i, array.Length);
    }
}
//第三步：结合大堆顶和节点比较 实现堆排序 把堆顶不停往后移动
static void HeapSort(int[] array)
{
    //构建大堆顶
    BuildBigHeap(array);
    //执行过后
    //最大的数肯定就在最上层
    //往屁股后面放 得到 屁股后面最后一个索引
    for (int i = array.Length - 1; i > 0; i--)
    {
        //直接把 堆顶端的数 放到最后一个位置即可
        int temp = array[0];
        array[0] = array[i];
        array[i] = temp;
        //重新进行大堆顶调整
        HeapCompare(array, 0, i);
    }
}
```

### 重写

```C#
public static void HeapCompare(int[] nums, int nowIndex, int len)
{
    int biggestIndex = nowIndex;
    int left = nowIndex * 2 + 1;
    int right = nowIndex * 2 + 2;
    if (left < len && nums[left] > nums[biggestIndex])
    {
        biggestIndex = left;
    }
    if (right < len && nums[right] > nums[biggestIndex])
    {
        biggestIndex = right;
    }
    if (biggestIndex != nowIndex)
    {
        int temp = nums[nowIndex];
        nums[nowIndex] = nums[biggestIndex];
        nums[biggestIndex] = temp;
        HeapCompare(nums, biggestIndex, len);
    }
}

public static void BuildHeap(int[] nums)
{
    for (int i = nums.Length / 2 - 1; i >= 0; --i)
    {
        HeapCompare(nums, i, nums.Length);
    }
}

public static void HeapSort(int[] nums)
{
    BuildHeap(nums);
    for (int i = nums.Length - 1; i >= 0; --i)
    {
        int temp = nums[0];
        nums[0] = nums[i];
        nums[i] = temp;
        //堆排序的精髓就在这里，利用数组长度这个参数
        //使得每次排序，忽略最大/最小的元素，已达到排序的效果
        HeapCompare(nums, 0, i);
    }
}
```

## 知识点三 总结

基本原理
构建二叉树
大堆顶调整
堆顶往后方
不停变堆顶

套路写法
3个函数
1个堆顶比较
1个构建大堆顶
1个堆排序

重要规则
最大非叶子节点索引：数组长度/2 - 1
父节点和叶子节点索引：父节点为i，左节点2i+1，右节点2i-1

注意：
堆是一类特殊的树，堆的通用特点就是父节点会大于或小于所有子节点；

我们并没有真正的把数组变成堆，只是利用了堆的特点来解决排序问题
