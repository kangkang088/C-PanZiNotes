# Cpp训练赛第三周 题解

# A	这是一道签到题

按题意输出即可

```Cpp
#include <iostream>

using namespace std;

void Solution() {
	cout << "zhe" << endl;
	cout << "shi" << endl;
	cout << "yi" << endl;
	cout << "dao" << endl;
	cout << "qian" << endl;
	cout << "dao" << endl;
	cout << "ti" << endl;
}
int main() {
	Solution();
    return 0;
}

```

# B	圆

如题，考虑什么情况下圆不想交。

1. 两圆距离太远，圆心距大于两个圆的半径和
2. 两圆距离包含，圆心距小于两个圆半径的差的绝对值

两者满足其一，则不想交

> 注意：圆心距等于半径和也算相交，所以不能用=

```Cpp
#include <iostream>
#include <math.h>

using namespace std;

void Solution() {
	long long x1, y1, r1, x2, y2, r2;
	cin >> x1 >> y1 >> r1 >> x2 >> y2 >> r2;
	long long distance = sqrt(pow(x1 - x2, 2) + pow(y1 - y2, 2));
	if (distance > r1 + r2 || distance < abs(r1 - r2)) {
        cout << "NO" << endl;
    }
    else {
        cout << "YES" << endl;
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

# C	数字游戏

如题，按题意模拟即可

```Cpp
#include <iostream>
#include <math.h>

using namespace std;

void Solution() {
	int n = 0;
    cin >> n;
    int score = 0;
    while (n != 1) {
        if (n % 2) {
            n = n * 3 + 1;
        }
        else {
            n /= 2;
        }
        ++score;
    }
    cout << score << endl;
}
int main() {
	Solution();
    return 0;
}
```

# D	矩阵转置

如题，需要将矩阵转置输出

使用另一个行列交换的数组，将原矩阵的行元素变为新矩阵的列元素，原矩阵的列元素变为为新矩阵的行元素即可

> 你还记得如何使用指针创建和释放二维数组吗？

```Cpp
#include <iostream>
#include <math.h>

using namespace std;

void Solution() {
    int rowLen, colLen;
    cin >> rowLen >> colLen;

    //创建二维数组
    int** matrix = new int* [rowLen];
    int** newMatrix = new int* [colLen];

    for (int i = 0; i < rowLen; ++i) {
        matrix[i] = new int[colLen];
    }
    
    for (int i = 0; i < colLen; ++i) {
        newMatrix[i] = new int[rowLen];
    }

    //输入
    for (int i = 0; i < rowLen; ++i) {
        for (int j = 0; j < colLen; ++j) {
            cin >> matrix[i][j];
        }
    }

    //转置
    for (int j = 0; j < colLen; ++j) {
        for (int i = 0; i < rowLen; ++i) {
            newMatrix[j][i] = matrix[i][j];
        }
    }

    //输出
    for (int j = 0; j < colLen; ++j) {
        for (int i = 0; i < rowLen; ++i) {
            cout << newMatrix[j][i] << " ";
        }
        cout << endl;
    }
    
    //释放
    for (int i = 0; i < rowLen; ++i) {
        delete[] matrix[i];
    }
    for (int j = 0; j < colLen; ++j) {
        delete[] newMatrix[j];
    }
    
    delete[] matrix;
    matrix = nullptr;
    delete[] newMatrix;
    newMatrix = nullptr;
}

int main() {
    Solution();
    return 0;
}
```

## 优化

由于不需要返回矩阵，所以，不需要重新赋值再输出，直接按列优先输出即可

```Cpp
#include <iostream>
#include <math.h>

using namespace std;

void Solution() {
	int rowLen, colLen;
    cin >> rowLen >> colLen;
    
    //创建二维数组
    int** nums = new int*[rowLen];
    for (int i = 0; i < rowLen; ++i) {
        nums[i] = new int[colLen];
    }
    
    //输入
    for (int i = 0; i < rowLen; ++i) {
        for (int j = 0; j < colLen; ++j) {
            cin >> nums[i][j];
        }
    }
    
    //输出
    for (int j = 0; j < colLen; ++j) {
        for (int i = 0; i < rowLen; ++i) {
            cout << nums[i][j] << " ";
        }
        cout << endl;
    }
    
    //释放
    for (int i = 0; i < rowLen; ++i) {
        delete[] nums[i];
    }
    delete[] nums;
    nums = nullptr;
}

int main() {
	Solution();
    return 0;
}
```

# E	挂科

如题，给出班级人数、高树和大雾的挂科人数，要求输出同时挂高树和大雾的最大可能人数和最小可能人数。

最大可能人数：

同时挂科的最大可能人数，就是两门科目挂科人数的最小值。

最小可能人数：

同时挂科的最小可能人数，就是两门科目挂科人数之和减去班级人数。

```Cpp
#include <iostream>

using namespace std;

void Solution() {
    int n = 0;
    int x, y;
    cin >> n >> x >> y;
    cout << min(x, y) << " ";
    if (x + y <= n) {
        cout << 0 << endl;
    }
    else {
        cout << x + y - n << endl;
    }
}

int main() {
    Solution();
}
```

# F	约瑟夫环

如题，经典的约瑟夫环问题。

考虑使用一个长度为n 的bool数组标记第**i**个人是否出队。

从编号k开始，使用循环并使用一个count来记录当前的报数，当count == m，将这个人的标记改为false，代表他出队，并且将剩余人数减一。当剩余人数为1时，查找标记数组，输出这个人的编号。

如何循环数组？

将k递增，使用k % n，这样就避免了k超出范围

```Cpp
#include <iostream>

using namespace std;

void Solution() {
    int n, k, m;
    cin >> n >> k >> m;
    
    //使用一个bool数组marks记录第i个人是否出队
    bool* marks = new bool[n];
    //初始化为true，表示还在队伍中，false表示出队
    for (int i = 0; i < n; ++i) {
        marks[i] = true;
    }
    
    int leftCount = n;    //剩余人数
    int count = 0;        //报数器
    while (leftCount > 1) {    //剩余人数 > 1就继续报数
        //开始报数
        while (count < m) {
            if (marks[k % n]) {    //如果这个人还没出队，报数
                ++count;
                ++k;
            }
            else {
                ++k;            //如果这个人出队了，跳过他
            }
        }
        //注意，这里是k - 1，因为报数报到m时，k也递增了
        marks[(k - 1) % n] = false;    //将报到m的人出队
        count = 0;    //重置报数器
        --leftCount;  //剩余人数-1
    }
    
    //遍历标记数组，查看答案
    for (int i = 0; i < n; ++i) {
        if (marks[i]) {
            cout << i << endl;
            break;
        }
    }
    delete[] marks;
    marks = nullptr;
}

int main() {
    Solution();
}
```

