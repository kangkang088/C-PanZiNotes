# Cpp训练赛第二周 题解

# A	输出'Z'

根据题意，可以考虑分别处理第一行、中间buff、最后一行

因为第1行需要输出正向箭头，中间第2到n-1行需要输出斜线，最后一行（第n行）需要输出反向箭头

对于第一行，先输出n - 1 个“-”，在输出一个“>”

对于中间部分，使用两层循环控制输出

观察到案例中“/"的位置，第一次出现在n - 1列，第二次出现在n - 2列，直到等于2

使用一个标记slashMark，初始化为n - 1，输出时，第二行的列数为slashMark时，输出“/”，否则输出“.”

每行输出结束时，slashMark-1

对于最后一行，第一行反过来即可

```Cpp
#include <iostream>

using namespace std;

void Solution() {
    int n = 0;
    cin >> n;
    for (int i = 0; i < n - 1; ++i) {
        cout << "-";
    }
    cout << '>' << endl;
    int slashMark = n - 1;
    for (int i = 1; i < n - 1; ++i) {
        for (int j = 1; j <= n ; ++j) {
            if (j != slashMark) {
                cout << ".";
            }
            else {
                cout << "/";
            }    
        }
        cout << endl;
        --slashMark;
    }
    cout << '<';
    for (int i = 1; i < n; ++i) {
        cout << "-";
    }
    cout << endl;
}

int main() {
    int n = 0;
    cin >> n;
    while (n--) {
        Solution();
    }
}
```

# B	数组3

如题，模拟输出即可

> 4年一闰，百年不闰，400年再闰

```Cpp
#include <iostream>

using namespace std;

void NormalPrint() {
    cout << "1月份: 31天" << endl;
    cout << "2月份: 28天" << endl;
    cout << "3月份: 31天" << endl;
    cout << "4月份: 30天" << endl;
    cout << "5月份: 31天" << endl;
    cout << "6月份: 30天" << endl;
    cout << "7月份: 31天" << endl;
    cout << "8月份: 31天" << endl;
    cout << "9月份: 30天" << endl;
    cout << "10月份: 31天" << endl;
    cout << "11月份: 30天" << endl;
    cout << "12月份: 31天" << endl;
}

void LeapYearPrint() {
    cout << "1月份: 31天" << endl;
    cout << "2月份: 29天" << endl;
    cout << "3月份: 31天" << endl;
    cout << "4月份: 30天" << endl;
    cout << "5月份: 31天" << endl;
    cout << "6月份: 30天" << endl;
    cout << "7月份: 31天" << endl;
    cout << "8月份: 31天" << endl;
    cout << "9月份: 30天" << endl;
    cout << "10月份: 31天" << endl;
    cout << "11月份: 30天" << endl;
    cout << "12月份: 31天" << endl;
}

void Solution() {
    long long year = 0;
    cin >> year;
    if (year % 4 == 0)
    {
        if (year % 100 == 0)
        {
            if (year % 400 == 0) {
                LeapYearPrint();
            }
            else {
                NormalPrint();
            }
        }
        else {
            LeapYearPrint();
        }
    }
    else {
        NormalPrint();   
    }
}

int main() {
    Solution();
    return 0;
}
```

# C	有趣的二进制

如题，要求求出一个整数的补码有多少个1

> 不会补码的看这里[补码的计算方法 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/376848035)

所以，只要每次将这个数按位右移一位，判断当前数的最后一位是否为1，直到这个数为0即可

如何判断当前数最后一位是否为1：使用按位与（&），将当前数&1即可

> 注意：按位操作都是根据补码运算的，所以不需要将数取反+1再运算

> 注意：题目输入要求多组数据，所以使用while(cin)

> 注意：需要使用unsigned long long，因为要求64位二进制，且负整数右移时自动补1，将造成无限循环

```Cpp
#include <iostream>

using namespace std;

void Solution() {
    unsigned long long num = 0;
    while (cin >> num) {
        int ans = 0;
        while (num) {
            if (num & 1) {
                ++ans;
            }
            num >>= 1;
        }
        cout << ans << endl;
    }
}

int main() {
    Solution();
    return 0;
}
```

# D	长方体

如题，给出长方体一个顶点的三个面的面积，让你求周长

所以，如果有长方体边长x，y，z，则正面面积areaA = x * z, 侧面面积areaB = y * z，底面面积areaC = x * y

联立三个等式有x * x = areaA * areaC / areaB

求出x后，依次求出y和z，最后即可求出周长

```Cpp
#include <iostream>
#include <math.h>

using namespace std;

void Solution() {
	int areaA , areaB , areaC ;
	cin >> areaA >> areaB >> areaC;
	int x = sqrt(areaA * areaC / areaB);
	int y = areaC / x;
	int z = areaB / y;
	int ret = (x + y + z) * 4;
	cout << ret << endl;
}

int main()
{
	Solution();
	return 0;
}

```

# E	送分题

如题，要求使用给出的三个数，搭配 * 或者 + ，使得式子的值最大

所以，有数numA，numB，numC，直接考虑一共有几种乘法或加法的搭配情况即可

根据排列组合，求得情况有6种：

```cpp
numA + numB + numC;
numA * numB * numC;
(numA + numB) * numC;
numA * (numB + numC);
numA * numB + numC;
numA + numB * numC;
```

将六种情况记录到数组中，然后排序，输出最大的一个数即可

> 不会使用sort的看这里[C++中sort()函数的使用方法_kuimzzs的博客-CSDN博客_c++中sort](https://blog.csdn.net/kuimzzs/article/details/81395347)

```Cpp
#include <iostream>
#include <algorithm>

using namespace std;

void Solution() {
	int numA, numB, numC;
	cin >> numA >> numB >> numC;
	int rets[6] = { 0 };
	rets[0] = numA + numB + numC;
	rets[1] = numA * numB * numC;
	rets[2] = (numA + numB) * numC;
	rets[3] = numA * (numB + numC);
	rets[4] = numA * numB + numC;
	rets[5] = numA + numB * numC;
	sort(rets, rets + 6);
	cout << rets[5] << endl;
}

int main()
{
	Solution();
	return 0;
}
```

# F	3的倍数

## 思路一

如题，给出left和right，要求将left和right中间的数包括left、right连接起来，组成一个新的数

如left = 3，right = 5，则组成新的数是345,

让你判断这个新的数是否是3的倍数

考虑直接暴力求解，将数一个个连接起来，然后模除3判断是否等于0

显然不可行，因为数据范围在1 ~ 10^18（10的18次方）

想一想，假设有一个案例为left = 1， right = 10 ^ 18，你就需要将1 ~ 10 ^ 18所有数连接起来，这个组成的数的长度将不可估计，而且也需要连接10 ^ 18次，耗时超出了时间限制。

考虑另一种方法从三的倍数的特性出发

众所周知，3的倍数有一个特性，就是所有位上的数加起来等于3倍数，或分成几段后加起来等于3倍数

比如123， 1 + 2 + 3 = 6，6是3的倍数，所以，123是3的倍数

比如273， 27  + 3 = 30，30是3的倍数，所以，273是3的倍数

那么如何求这个组合的数的每一位数的和呢，已经不能将他们连接起来了

仔细查看题面，是连接中间所有数

也就是说，left = 1， right = 10，则组合数为1 2 3 4 5 6 7 8 9 10

显然，这是一个等差数列，第一项为left，最后一项为right，项的数量为right - left + 1

所以，使用等差数列求和公式

> [等差数列求和公式](https://gitee.com/Panzi_ssa/Personal_notes/blob/master/飞思/飞思训练赛/图片/等差数列求和公式.jpg)

即可求得所有分段上的数的和

又因为数据范围过大，使得他们的和可能也存储不下来

所以考虑直接判断式子上半部分，并且拆开来判断，只要一个符合是3的倍数即可 （一个数是3的倍数，乘上另一个数，最后所得的数一定也是3的倍数）

所以代码如下

```Cpp
#include <iostream>

using namespace std;

void Solution() {
    long long left = 0;
    long long right = 0;
    cin >> left >> right;
    if ((left + right) % 3 == 0 || (right - left + 1) % 3 == 0) {
        cout << "YES" << endl;
    }
    else {
        cout << "NO" << endl;
    }
}

int main() {
    int n = 0;
    cin >> n;
    while (n--) {
        Solution();
    }
    return 0;
}
```

## 思路二

由于题目要求是连续的数组成的数，那么考虑连续的数是否是三的倍数

比如

123,是，23不是

345是，34不是

567是，56不是

观察规律得，连续的3个数组成的数，一定是三的倍数

所以只需要考虑left - right中间有多少个连续的3个项即可，共有right - left + 1项，所以只要项数模除3==0即可

此时，还有一种情况，就是12，显然，这也是符合的，所以，还需判断（right + left）% 3 == 0

> 观察出，代码与思路一一致

