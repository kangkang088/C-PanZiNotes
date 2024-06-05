# Cpp训练赛第一周 题解

# A	Hello, algorithm

如题，随意输出一次评测结果的缩写

```Cpp
#include <iostream>

using namespace std;

int main() {
    cout << "AC" << endl;
    return 0;
}
```

# B	大炼丹师

如题，依次判断是否是符合条件的三角形

```Cpp
#include <iostream>

using namespace std;

void Solution() {
	long long a, b, c;
	cin >> a >> b >> c;
    //先判断能否组成三角形，再一次判断是什么三角形
	if ((a + b) > c && (a + c) > b && (b + c) > a) {
		if ((a * a + b * b) == c * c || (a * a + c * c) == b * b || (b * b + c * c) == a * a) {
			cout << "right" << endl;
		}
		else if (a == b && a == c && b == c) {
			cout << "equilateral" << endl;
		}
		else {
			cout << "normal" << endl;
		}
	}
	else {
		cout << "error" << endl;
	}
}

int main()
{
	int n = 0;
	cin >> n;
	while (n--) {
		Solution();
	}
	return 0;
}
```

# C	红鲤鱼与绿鲤鱼与驴

如题，按照要求输出

> 小tips，可以直接用"cin >> buf"作为while判断条件，这样只要没有输入，就不会运行了

```Cpp
#include <iostream>

using namespace std;

void Solution() {
	char buf = ' ';
	while (cin >> buf) {
		if (buf == '1') {
			cout << "hongliyu";
		}
		if (buf == '2') {
			cout << "lvliyu";
		}
		if (buf == '3') {
			cout << "lv";
		}
	}
	cout << endl;
}

int main()
{
	Solution();
	return 0;
}
```

# D	被鸽了的课本

根据题意计算比较即可

> 注意是减免a%

```Cpp
#include <iostream>

using namespace std;

int main() {
    double x, y, a;
    cin >> x >> y >> a;
    double school = (x + y) * (1.0 - 0.01 * a);
    double self = x + (y / 2.0);
    if (school < self) {
        cout << "Through school" << endl;
    }
    else {
        cout << "By myself" << endl;
    }
    
    return 0;
}
```

# E	AK

根据题意，需要找出第一个最后两个字符为"AK"的人，然后输出他的名字

注意，找到第一个答案后，不能直接返回，因为还有后续输入，所以，我们使用一个bool值getAnsFlag来记录答案是否已经出现，出现第一次时，置false，这样后续就不会覆盖第一个答案了

并且输出答案时，不用输出AK

```Cpp
#include <iostream>
#include <string.h>

using namespace std;

void Solution() {
	int n = 0;
	cin >> n;
	char str[101];
    char ans[101];
	bool getAnsflag = true;
	while (n--) {
		cin >> str;
        int len = strlen(str);
		if (str[len - 1] == 'K' && str[len - 2] == 'A' && getAnsflag) {
			strcpy(ans, str);
			getAnsflag = false;
		}
	}
    int ansLen = strlen(ans);
	for (int i = 0; i < ansLen - 2; ++i) {
		cout << ans[i];
	}
	cout << endl;
}

int main()
{
	Solution();
	return 0;
}
```

# F	扫雷

根据题意，需要标记每个不是雷格子的值为周围9宫格雷的数量

考虑使用一个大数组来存储数字矩阵

```Cpp
char matrix[1001][1001] = { 0 };
```

让下标从1开始进行输入，这样，就避免了数组越界问题

在刚开始输入时，使用一个getchar()，避免输入换行

```Cpp
	int n, m;
	cin >> n >> m;
	//下标从1开始
	for (int i = 1; i <= n; ++i) {
		getchar();
		for (int j = 1; j <= m; ++j) {
			matrix[i][j] = getchar();
		}
	}
```

再一个个遍历格子，遇到是雷直接输出，遇到是空格，则判断周围3*3的格子有没有雷，把周围雷的数量记录下来，输出即可

如：

|      |      |      |      |      |
| ---- | :--: | :--: | :--: | ---- |
|      |  *   |  *   |  *   |      |
|      |  *   |      |  *   |      |
|      |  *   |  *   |  *   |      |
|      |      |      |      |      |

当遍历到i == 2， j == 2时，开始扫描周围雷的数量，

那么，就需要从i - 1， j - 1 开始，依次遍历，直到i + 1, j + 1结束，记录遍历时遇到的雷的数量，然后直接输出

|      |      |      |      |      |
| ---- | :--: | :--: | :--: | ---- |
|      |  *   |  *   |  *   |      |
|      |  *   |  8   |  *   |      |
|      |  *   |  *   |  *   |      |
|      |      |      |      |      |

具体到代码上来

```Cpp
	//输出时，下标也从1开始
	for (int i = 1; i <= n; ++i) {
		for (int j = 1; j <= m; ++j) {
            //遇到雷，直接输出
			if (matrix[i][j] == '*') {
				cout << matrix[i][j];
			}
            //不是雷，开始遍历九宫格
			else {
				int count = 0;	//使用一个变量记录周围雷的数量
				for (int k = i - 1; k <= i + 1; ++k) {	//开始遍历，从i - 1开始，到i + 1
					for (int t = j - 1; t <= j + 1; ++t) {	//从j - 1 开始，到j + 1
						if (matrix[k][l] == '*') {	//遇到雷，计数器+1
							++count;
						}
					}
				}
				cout << count;//计算完毕，直接输出
			}
		}
		cout << endl;
	}
```

整套代码

```Cpp
#include <iostream>

using namespace std;

void Solution() {
	char matrix[1001][1001] = { 0 };
	int n, m;
	cin >> n >> m;
	for (int i = 1; i <= n; ++i) {
		getchar();
		for (int j = 1; j <= m; ++j) {
			matrix[i][j] = getchar();
		}
	}

	for (int i = 1; i <= n; ++i) {
		for (int j = 1; j <= m; ++j) {
			if (matrix[i][j] == '*') {
				cout << matrix[i][j];
			}
			else {
				int count = 0;
				for (int k = i - 1; k <= i + 1; ++k) {
					for (int t = j - 1; t <= j + 1; ++t) {
						if (matrix[k][t] == '*') {
							++count;
						}
					}
				}
				cout << count;
			}
		}
		cout << endl;
	}
}

int main()
{
	Solution();
	return 0;
}
```

