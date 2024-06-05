# Cpp训练赛第七、第八周 题解

# A	反向输出一个四位数

如题，直接使用字符串方向输出即可

```Cpp
#include <iostream>

using namespace std;

void Solution() {
    string str;
    cin >> str;
    for (int i = 0; i < str.size(); ++i) {
        cout << str[str.size() - i - 1];
    }
    cout << endl;
    
}

int main() {
    Solution();
    return 0;
}
```

# B	四季

如题，直接计算输出即可

```CPP
#include <iostream>

using namespace std;

void Solution() {
    long long date;
    cin >> date;
    date %= 100;
    switch(date / 3) {
        case 1: cout << "spring" << endl; break;
        case 2: cout << "summer" << endl; break;
        case 3: cout << "autumn" << endl; break;
        case 4:
        case 0: cout << "winter" << endl; break;
    }
    
}

int main() {
    Solution();
    return 0;
}
```

# C	[NOIP2017]成绩

如题，由于案例全是10的倍数，所以直接模拟输出即可

```Cpp
#include <iostream>

using namespace std;

void Solution() {
    int a, b, c;
    cin >> a >> b >> c;
    a *= 0.2;
    b *= 0.3;
    c *= 0.5;
    cout << a + b + c << endl;
}

int main() {
    Solution();
    return 0;
}
```

# D	[NOIP2006]明明的随机数

如题，给定一组数据，要求排序并且去除相同的数据。

考虑直接排序，初始时index = 0，i = 1，遍历数组，index记录当前数，检查nums[i]与nums[index]是否相同，不同++index并且赋值，相同不操作。知道遍历完成，index + 1就是长度

```Cpp
#include <iostream>
#include <algorithm>

using namespace std;

void Solution() {
    int N = 0;
    cin >> N;
    int* nums = new int[N];
    for (int i = 0; i < N; ++i) {
        cin >> nums[i];
    }
    sort(nums, nums + N);
    int index = 0;
    for (int i = 1; i < N; ++i) {
        if (nums[i] != nums[index]) {
            ++index;
            nums[index] = nums[i];
        }
    }
    cout << index + 1 << endl;
    for (int i = 0; i <= index; ++i) {
        cout << nums[i] << " ";
    }
    cout << endl;
}

int main() {
    Solution();
    return 0;
}
```

# E	[NOIP2005]校门外的树

如题，给定L + 1颗树，再给定M行闭区间\[left, right\]，使得区间内的树消除。让你计算M行区间后，还有多少颗树。

考虑使用一个标记数组marks，长度为L + 1，每当给定一个区间，就标记这个区间。所有区间遍历完成后，再计算标记数组中还有多少数没有被标记即可计算得答案。

```Cpp
#include <iostream>
#include <algorithm>

using namespace std;

void Solution() {
    int L, M;
    cin >> L >> M;
    bool* marks = new bool[L + 1];
    for (int i = 0; i < M; ++i) {
        int left = 0, right = 0;
        cin >> left >> right;
        for (int j = left; j <= right; ++j) {
            marks[j] = true;
        }
    }
    int ret = 0;
    for (int i = 0; i <= L; ++i) {
        if (!marks[i]) {
            ++ret;
        }
    }
    cout << ret << endl;
}

int main() {
    Solution();
    return 0;
}
```

# F	[NOIP2011]铺地毯

给定n张地毯的左下角坐标和每张地毯在x轴y轴上的长度，一个查询坐标，要求你求出最后这个查询坐标上的地毯是哪一张。

考虑直接查询，从后向前查询地毯覆盖的矩形区域，每当在这个矩形范围内，直接输出，没有查找到，输出-1。

如何计算这个矩形区域？

由于给定左下角坐标和地毯在x轴y轴上的长度，所以，这个区域就在[x1, x2], [y1, y2]

即x >= x1 && x <= x2 && y >= y1 && y <= y2，其中，（x1，y1）是左下角坐标，（x2，y2）是右上角坐标。

```Cpp
#include <iostream>
#include <algorithm>

using namespace std;

void Solution() {
    int n = 0;
    cin >> n;
    int** nums = new int* [n];
    for (int i = 0; i < n; ++i) {
        nums[i] = new int[4];
    }
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < 4; ++j) {
            cin >> nums[i][j];
        }
    }
    int x, y;
    cin >> x >> y;
    for (int i = n - 1; i >= 0; --i) {
        int x1 = nums[i][0];
        int y1 = nums[i][1];
        int x2 = nums[i][0] + nums[i][2];
        int y2 = nums[i][1] + nums[i][3];
        if ( x >= x1 && x <= x2 && y >= y1 && y <= y2) {
            cout << i + 1 << endl;
            return;
        }
    }
    cout << -1 << endl;
}

int main() {
    Solution();
    return 0;
}
```

