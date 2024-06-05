# Cpp训练赛第六周 题解

# A	时间转换

如题，给定秒数，转换为具体时间，众所周知1hour = 60 minute， 1minute = 60 second。

所以，根据公式直接计算即可。

```Cpp
#include <iostream>

using namespace std;

void Solution() {
    long long num;
    cin >> num;
    long long hour = num / 3600;
    long long minute = (num - hour * 3600) / 60;
    long long second = (num - hour * 3600 - minute * 60);
    cout << hour << " " << minute << " " << second << endl;
}

int main() {
    Solution();
    return 0;
}
```

# B	杨辉三角

如题，给定杨辉三角的行数，要求你输出n行杨辉三角

经典的动态规划题目，除了每行第一个数和对角线上的数，其他的任意一个数都有nums\[i\]\[j\] = nums\[i - 1\]\[j\] + nums\[i - 1\]\[j - 1\];

> 其实上面这个式子就是这道题目的状态转移方程或者说递推式

所以，直接模拟计算，然后输出即可

```Cpp
#include<iostream>

using namespace std;

void Solution() {
    int n = 0;
    cin >> n;
    int** nums = new int* [n];
    for (int i = 0; i < n; ++i) {
        nums[i] = new int [i + 1];
    }
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j <= i; ++j) {
            if (j == i || j == 0) {
                nums[i][j] = 1;
            } 
            else {
                nums[i][j] = nums[i - 1][j] + nums[i - 1][j - 1];
            }
        }
    }
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j <= i; ++j) {
            cout << nums[i][j] << " ";
        }
        cout << endl;
    }
}

int main() {
    Solution();
    return 0;
}
```

# C	字符金字塔

如题，和上场比赛一题类似，分类讨论输出，只不过重新需要考虑输出的字母；

观察得知，输出的字符前半段从A递增，后半段递减，

使用一个cnt为当前需要输出的字母的个数，cnt每次递增2；

先从A开始，输出cnt / 2 递增的字母；

再从A + cnt / 2 - 1开始，输出cnt / 2 - 1个递减的字母。

```Cpp
#include <iostream>

using namespace std;

void Solution() {
    char buf;
    cin >> buf;
    int len = buf - 'A' + 1;
    int cnt = 1;
    for (int i = 0; i < len; ++i) {
        for (int k = 0; k < len - i - 1; ++k) {
            cout << " ";
        }
        for (int t = 0; t <= cnt / 2; ++t) {
            char temp = 'A' + t;
            cout << temp;
        }
        for (int l = cnt / 2 - 1; l >= 0; --l) {
            char temp = 'A' + l;
            cout << temp;
        }
        cnt += 2;
        cout << endl;
    }
}

int main() {
    Solution();
    return 0;
}
```

# D	回文对称数

给定一个整数n，要求求1 - n中回文数并输出。

由于最多10W个数，考虑直接暴力，遍历1 - n，每一个数，检查一次是否是回文数，是则输出，不是跳过。

如何检查是否是回文数？

先将该数使用to_string函数转换为字符串，再使用两个下标left = 0， right = str.size() - 1，循环判断str[left] == str[right]，一旦遇到不等于直接返回false，当遍历全部字符时，返回true。

> 其实， 这叫做双指针，指使用两个下标遍历数组，遍历的过程中，对两个下标指向的数据进行判断处理。

```Cpp
#include <iostream>

using namespace std;

bool Check(int num) {
    string str = to_string(num);
    int left = 0;
    int right = str.size() - 1;
    while (left < right) {
        if (str[left] != str[right]) {
            return false;
        }
        ++left;
        --right;
    }
    return true;
}

void Solution() {
    int n = 0;
    cin >> n;
    for (int i = 1; i <= n; ++i) {
        if (Check(i)) {
            cout << i << endl;
        }
    }
}

int main() {
    Solution();
    return 0;
}
```

# E	牛牛的三角形

如题，给定一组数据，让你选择其中三个数，使得三个数字可以组成一个三角形。

## 暴力

考虑暴力，使用三个for，遍历每一种3个数的组合，如果可以组成三角形直接输出，如果不能，继续下一个。

```Cpp
#include <iostream>
#include <algorithm>

using namespace std;

void Solution() {
    int n = 0;
    cin >> n;
    unsigned long long* nums = new unsigned long long[n];
    for (int i = 0; i < n; ++i) {
        cin >> nums[i];
    }
    for (int i = 0; i < n; ++i) {
        for (int j = i + 1; j < n; ++j) {
            for (int k = j + 1; k < n; ++k) {
                unsigned long long a = nums[i];
                unsigned long long b = nums[j];
                unsigned long long c = nums[k];
                if (a + b > c && a + c > b && b + c > a) {
                    cout << nums[i] << " " << nums[j] << " " << nums[k] << endl;
                    return;
                }
            }
        }
    }
    cout << "No solution" << endl;
}

int main() {
    Solution();
    return 0;
}
```

## 优化

由于时间复杂度过高，考虑另一种解决方案。

由于给定数据，我们可以将这组数据从小到大排序，从右向左遍历数组；

选择可变动左端点left为0，不变右端点right为当前数的前一个(i - 1)；

再次遍历数组，因为数组已经排过序，nums[i] > nums[right] > nums[left]；

所以有nums[i] + nums[right] > nums[left]，nums[i] + nums[left] > nums[right]；

所以当nums[left] + nums[right] > nums[i] 时，这一定可以组成一个三角形，此时输出即可。

```Cpp
#include <iostream>
#include <algorithm>

using namespace std;

void Solution() {
    int n = 0;
    cin >> n;
    unsigned long long* nums = new unsigned long long[n];
    for (int i = 0; i < n; ++i) {
        cin >> nums[i];
    }
    sort(nums, nums + n);
    for (int i = n - 1; i > n / 2; --i) {
        int left = 0;
        int right = i - 1;
        while (left < right) {
            if (nums[left] + nums[right] > nums[i]) {
                cout << nums[left] << " " << nums[right] << " " << nums[i] << endl;
                return;
            }
            ++left;
        }
    }
    cout << "No solution" << endl;
}

int main() {
    Solution();
    return 0;
}
```

# F	吐泡泡

如题，给定一组字符串，连续的小泡泡可以与小泡泡合并为一个大泡泡，连续的两个大泡泡会爆炸消失，一大一小无操作。

如ooOOo，ooOOo -> OOOo，OOOo -> Oo。

显然，这是一道使用栈模拟的题目，需要维护一个没有连续大小泡泡的栈。

首先，遍历字符串，当栈空或者栈顶泡泡和当前字符不一样时，将泡泡入栈；

当栈不为空，判断泡泡种类，如果是大泡泡并且栈顶是大泡泡，出栈一个大泡泡；

如果是小泡泡并且栈顶是小泡泡，将栈顶变为大泡泡，出栈，并再次判断栈顶是否为大泡泡，如果是大泡泡，出栈这个大泡泡，如果是小泡泡，入栈一个大泡泡。

遍历完成后，将所有栈内元素出栈，并且逆序输出即可（因为栈先进后出）

为什么合成大泡泡后只需要再判断一次栈顶元素？

因为我们维护的是一个没有连续大泡泡和连续小泡泡的栈，会引发连续泡泡的只有小泡泡变为大泡泡，所有，当再次判断一次大泡泡后，就不可能再有大泡泡。

> 注意：题目有多行输出。

```Cpp
#include <iostream>
#include <algorithm>
#include <stack>

using namespace std;

void Solution(string& str) {
    stack<char> sta;
    for (int i = 0; i < str.size(); ++i) {
        //如果栈空或者栈顶元素与当前泡泡不一样，入栈泡泡
        if (sta.empty() || sta.top() != str[i]) {
            sta.push(str[i]);
            continue;
        }
        //如果是小泡泡并且栈顶是小泡泡，将栈顶变为大泡泡，出栈
        if(!sta.empty() && sta.top() == str[i] && str[i] == 'o'){
            sta.pop();
            //并再次判断栈顶是否为大泡泡，如果是大泡泡，出栈这个大泡泡，如果是小泡泡，入栈一个大泡泡。
            if(!sta.empty() && sta.top() == 'O') {
                sta.pop();
            }
            else {
                sta.push('O');
            }
        }
        //如果是大泡泡并且栈顶是大泡泡，出栈一个大泡泡
        else if(!sta.empty() && sta.top() == str[i] && str[i] == 'O'){
            sta.pop();
        }
        
    }
    
    string ret = "";
    //出栈所有元素
    while (!sta.empty()) {
        ret += sta.top();
        sta.pop();
    }
    //逆序输出
    for (int i = ret.size() - 1; i >= 0; --i) {
        cout << ret[i];
    }
    cout << endl;
}

int main() {
    string str = "";
    while (cin >> str) {
        Solution(str);
    }
    return 0;
}
```

