# Cpp训练赛第五周 题解

# A	阿宁的柠檬

如题，给定n个柠檬，一个柠檬酸度可能是 1到 a，甜度可能是 0到 b。快乐值是酸度和甜度之和。

所以最小快乐值就是n（每个柠檬的酸度是1，甜度是0）；

最大快乐值是a \* n + b * n（每个柠檬的酸度是n，甜度是n）。

> 注意：应该使用long long

```Cpp
#include <iostream> 

using namespace std; 

int main() {
    long long a, b, n;
    cin >> a >> b >> n;
    long long minHappy = n;
    long long maxHappy = a * n + b * n;
    cout << minHappy << " " << maxHappy << endl;
    return 0;
}
```

# B	字符数量

如题，需要记录一段文字当中小写字母出现的次数，考虑使用一个大小为26的数组记录小写字母出现的次数（因为26个字母）

没遇到一个小写字母，就递增一次记录数组的数据，最后在输入时，判断是大于0并输出，大于0即出现过

> 其实，这就是哈希表的思想
>
> [什么是哈希表？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/107326081)

```C#
#include <iostream>

using namespace std;

void Solution() {
    string str;
    int letters[26] = { 0 };
    while (cin >> str) {
        for (int i = 0; i < str.size(); ++i) {
            if (islower(str[i])) {
                ++letters[str[i] - 'a'];    
            }
        }
    }
    
    for (int i = 0; i < 26; ++i) {
        char temp = 'a';
        if (letters[i]) {
            temp += i;
            cout << temp << ":" << letters[i] << endl;
        }
    }
}

int main() {
    Solution();
    return 0;
}
```

另一种写法，使用STL（标准模板库）中的unordered_map（标准模板库中的哈希表）

```Cpp
#include <iostream>
#include <unordered_map>
using namespace std;

void Solution() {
    string str;
    unordered_map<char, int> letters;
    while (cin >> str) {
        for (int i = 0; i < str.size(); ++i) {
            if (islower(str[i])) {
                ++letters[str[i]];    
            }
        }
    }
    
    for (int i = 0; i < 26; ++i) {
        if (letters['a' + i]) {
            char temp = 'a' + i;
            cout << temp << ":" << letters['a' + i] << endl;
        }
    }
}

int main() {
    Solution();
    return 0;
}
```

# C	图形

如题，要求输出“\*”三角形，观察案例得知第 i 行的空格数为n - i - 1，第i行的 “\*"号数量为i \* 2+ 1

所以，直接模拟输出即可

```Cpp
#include <iostream>
#include <unordered_map>
using namespace std;

void Solution() {
    int n = 0;
    while (cin >> n) {
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < n - i - 1; ++j) {
                cout << " ";
            }
            for (int k = 0; k < i * 2 + 1; ++k) {
                cout << "*";
            }
            cout << endl;
        }
    }
}

int main() {
    Solution();
    return 0;
}
```

# D	音标

如题，给出多串小写字符串，每一串的每一个字母都需要找出一个**恰好**不大于它本身的小写元音字母。

所以先使用一个大小为6的字符数组存储元音字母，遍历每一串字符串，查找大于当前字母的元音字母，当查找到时，这个元音字母的前一个，也就是**恰好**不大于当前字母的元音字母。

注意，需要考虑边界问题，如果当前字母是‘a’，查找到的下标将是0，所以需要判断是否查找到的下标是0，如果是0，直接输入‘a’；

> 注意是多行输入，使用while(cin)，并且输出后需要输出换行

```Cpp
#include <iostream>
#include <string>

using namespace std;

void Solution() {
    string str;
    char vowel[6] = { 'a', 'e', 'i', 'o', 'u', 'y'};
    while (cin >> str) {
        for (int i = 0; i < str.size(); ++i) {
            int j = 0;
            //查找大于当前字母的元音字母
            while (str[i] >= vowel[j] && j < 6) {
                ++j;
            }
            //边界特判
            if (j != 0) {
                cout << vowel[j - 1];
            }
            else {
                cout << 'a';
            }
        }
        cout << endl;
    }
}

int main() {
    Solution();
    return 0;
}
```

# E	[NOIP2017]图书管理员

如题，给定一组图书编号，多组后缀长度和图书编号的后缀，要求求得所需图书的图书编号后缀在这组图书编号中最小的一个。

考虑直接查找，先将所有图书编号存入是数组，将这组编号排序。

当输入后缀长度和图书编号的后缀时，遍历图书编号数组，查找后缀，此时，查找到的第一个图书编号就是所需编号（因为已经排过序了，第一个就是最小的），记录答案并输出，无答案则输出-1。

如何查找后缀？

由于给定了后缀的长度，所以，只需要"图书编号 % pow(10, 后缀长度) "即可求得当前图书编号对应长度的后缀。

比如图书编号为 123456， 后缀长度为2， 后缀为56

那么只需要 123456 % pow(10, 2) == 123456 % 100即可求得56，也就是对应长度的后缀。

```Cpp
#include <iostream>  
#include <algorithm>
#include <math.h>

using namespace std;

void Solution() {
    long long n, q;
    cin >> n >> q;
    int* booksNum = new int[n];	//图书编号数组
    for (int i = 0; i < n; ++i) {
        cin >> booksNum[i];
    }
    sort(booksNum, booksNum + n);
    for (int i = 0; i < q; ++i) {
        int codeLen;	//后缀长度
        int requireCode;//所需要的图书编号
        cin >> codeLen >> requireCode;
        
        bool getAnsFlag = false;
        int tempMod = pow(10, codeLen);
        int ret = 0;
        for (int i = 0; i < n; ++i) {
            if (booksNum[i] % tempMod == requireCode) {
                getAnsFlag = true;
                ret = i;
                break;
            }
        }
        if (getAnsFlag) {
            cout << booksNum[ret] << endl;
        }
        else {
            cout << "-1" << endl;
        }
    }
}

int main(){
    Solution();    
    return 0;
}
```

# F	牛牛与后缀表达式

如题，给定一个后缀表达式，要你求出计算结果。显然，这是一道用栈就能解决的问题。

> 不会STL stack（栈）的看这里[C++ STL Stack常用方法详解_蔚蓝不远的博客-CSDN博客_c++ stl stack常用方法](https://blog.csdn.net/weixin_44723496/article/details/107379359)
>
> 如果你还是不会，没关系，我会用一个数组模拟栈。

遍历字符数组，只需要每次将遇到的数字入栈，当遇到操作符时，出栈左操作数（lhs）和右操作数（rhs），再根据操作符计算并将计算结果再压入栈，计算到最后，栈顶元素一定是结果。

比如：1#2#+

先将1入栈，再将2入栈，遇到操作符+，先将2出栈作为右操作符（rhs），再将1出栈作为左操作符（lhs），根据操作符+号运算，将结果3压入栈，此时遍历结束，栈顶元素就是表达式结果。

> 注意：由于栈是先进后出，入栈时是先左操作数，再右操作数，所以先出栈的是右操作数，再左操作数。

如果数字是多位怎么办？

题目已经说明，数字使用#号结束，使用一个循环遍历计算即可，可以将此段代码封装为一个函数。

> 注意使用long long

## 使用数组模拟栈

考虑使用一个top指针模拟栈顶位置，入栈top + 1，nums[top] = num，出栈top - 1，nums[top] = num，空栈top == -1；

```Cpp
class Solution {
public:
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 给定一个后缀表达式，返回它的结果
     * @param str string字符串 
     * @return long长整型
     */
    //得到数字的函数
    long long GetNum(string& str, int& i) {
        long long num = 0;
        while (str[i] != '#' && i < str.size()) {
            num = num * 10 + str[i] - '0';
            ++i;
        }
        return num;
    }
    
    long long legalExp(string str) {
        // write code here
        long long* nums = new long long[1001];
        int top = -1;	//初始时，栈空
        int i = 0;
        long long ret = 0;
        while (i < str.size()) {
            int num = 0;
            //查找操作数
            while (isdigit(str[i])) {
                long long num = GetNum(str, i);
                ++i;	//这里需要++，因为一个数后面可能还有一个数
                //入栈操作数
                ++top;	
                nums[top] = num;
            }
            long long rhs = nums[top]; //出栈右操作数
            --top;
            long long lhs = nums[top]; //出栈左操作数
            --top;
            //根据操作符计算结果并入栈
            switch(str[i]) {
                case '+': ++top; nums[top] = lhs + rhs; break;
                case '-': ++top; nums[top] = lhs - rhs; break;
                case '*': ++top; nums[top] = lhs * rhs; break;
                case '/': ++top; nums[top] = lhs / rhs; break;
            }
            ++i;
        }
        return nums[top];
    }
};
```

## 使用Cpp STL stack

```Cpp
class Solution {
public:
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 给定一个后缀表达式，返回它的结果
     * @param str string字符串 
     * @return long长整型
     */
    //得到数字的函数
    long long GetNum(string& str, int& i) {
        long long num = 0;
        while (str[i] != '#' && i < str.size()) {
            num = num * 10 + str[i] - '0';
            ++i;
        }
        return num;
    }
    
    long long legalExp(string str) {
        // write code here
        stack<long long> nums;	//STL stack(栈)
        int i = 0;
        long long ret = 0;
        while (i < str.size()) {
            int num = 0;
            //查找操作数
            while (isdigit(str[i])) {
                long long num = GetNum(str, i);
                ++i;	//这里需要++，因为一个数后面可能还有一个数
                nums.push(num);	//入栈操作数
            }
            long long rhs = nums.top(); 	//出栈右操作数
            nums.pop();
            long long lhs = nums.top(); 	//出栈左操作数
            nums.pop();
            //根据操作符计算结果并入栈
            switch(str[i]) {
                case '+': nums.push(lhs + rhs); break;
                case '-': nums.push(lhs - rhs); break;
                case '*': nums.push(lhs * rhs); break;
                case '/': nums.push(lhs / rhs); break;
            }
            ++i;
        }
        return nums.top();
    }
};
```

