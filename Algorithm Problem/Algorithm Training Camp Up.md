# Algorithm Training Camp Up

# 1.最优装载问题（贪心）

有一天，海盗们截获了一艘装满各种各样古董的货船，每件古董都价值连城，一旦打碎就失去了价值。虽然海盗船足够大，但载重为c ，每件古董的重量为wi ，海盗们绞尽脑汁要把尽可能多的宝贝装上海盗船，该怎么办呢？

```Cpp
int Solution(vector<int>& w, int c) {
	cout << "w.size():" << w.size() << "c:" << c << endl;
	sort(w.begin(), w.end());
	int ans = 0;
	for (int i = 0; i < w.size(); ++i) {
		c -= w[i];
		if (c > 0) {
			++ans;
		}
		else {
			break;
		}
	}
	return ans;
}
```

# 2.归并排序

```Cpp
#include<iostream>
#include<vector>
#include<time.h>
#include<algorithm>
using namespace std;

void Merge(vector<int>& nums, int left, int right) {
	vector<int> temp(right - left + 1);
	int mid = left + (right - left) / 2;
	int i = left;
	int j = mid + 1;
	int index = 0;
	while (i <= mid && j <= right) {
		if (nums[i] < nums[j]) {
			temp[index++] = nums[i++];
		}
		else {
			temp[index++] = nums[j++];
		}
	}
	while (i <= mid) {
		temp[index++] = nums[i++];
	}
	while (j <= right) {
		temp[index++] = nums[j++];
	}
	index = 0;
	for (int i = left; i <= right; ++i) {
		nums[i] = temp[index++];
	}
}

void MergeSort(vector<int>& nums, int left, int right) {
	if (left < right) {
		int mid = left + (right - left) / 2;
		MergeSort(nums, left, mid);
		MergeSort(nums, mid + 1, right);
		Merge(nums, left, right);
	}
}

void PrintArray(vector<int>& nums) {
	for (int& item : nums) {
		cout << item << " ";
	}
	cout << endl;
}

int main() {
	srand(time(0));
	vector<int> nums;
	for (int i = 0; i < 10; ++i) {
		nums.push_back(rand());
	}
	PrintArray(nums);
	MergeSort(nums, 0, nums.size() - 1);
	PrintArray(nums);
	return 0;
}
```

# 3.快速排序

```Cpp
#include<iostream>
#include<vector>
#include<time.h>
#include<algorithm>
using namespace std;

int Partition(vector<int>& nums, int left, int right) {
	int key = nums[left];
	int i = left;
	int j = right;
	while (i < j) {
		while (i < j && nums[j] > key) {
			--j;
		}
		if (i < j) {
			swap(nums[i++], nums[j]);
		}
		while (i < j && nums[i] <= key) {
			++i;
		}
		if (i < j) {
			swap(nums[i], nums[j--]);
		}
	}
	return i;
}

int RandomPartition(vector<int>& nums, int left, int right) {
	int mark = rand() % (right - left + 1) + left;
	swap(nums[left], nums[mark]);
	return Partition(nums, left, right);
}

void QuickSort(vector<int>& nums, int left, int right) {
	if (left < right) {
		int mid = RandomPartition(nums, left, right);
		QuickSort(nums, left, mid - 1);
		QuickSort(nums, mid + 1, right);
	}
}

void PrintArray(vector<int>& nums) {
	for (int& item : nums) {
		cout << item << " ";
	}
	cout << endl;
}

int main() {
	srand(time(0));
	vector<int> nums;
	for (int i = 0; i < 10; ++i) {
		nums.push_back(rand());
	}
	PrintArray(nums);
	QuickSort(nums, 0, nums.size() - 1);
	PrintArray(nums);
	return 0;
}
```

# 4.间谍（HDU3527，哈希表）

http://acm.hdu.edu.cn/showproblem.php?pid=3527

```Cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <math.h>
#include <string>
#include <unordered_map>

using namespace std;

//X国的情报委员收到一份可靠的
//信息，信息表明Y国将派间谍去窃取X国的机密文件。X国指挥
//官手中有两份名单列表，一份是Y国派往X国的间谍名单列表，
//另一份是X国以前派往Y国的间谍名单列表。这两份名单列表可
//能有些重叠。因为间谍可能同时扮演两个角色，称之为“双重间
//谍”。因此，Y国可以把双重间谍送回X国。很明显，这对X国是
//有利的，因为双重间谍可以把Y国的机密文件带回，而不必担心
//被Y国边境拘留。所以指挥官决定抓住由Y国派出的间谍，让普
//通人和双重间谍进入。那么你能确定指挥官需要抓捕的间谍名
//单吗？
//http://acm.hdu.edu.cn/showproblem.php?pid=3527

int A, B, C;
void Solution() {
    unordered_map<string, int> allName;
    string temp = "";
    for (int i = 0; i < A; ++i) {
        cin >> temp;
        allName[temp]++;
    }
   vector<string> spyX(B);
    for (int i = 0; i < B; ++i) {
        cin >> spyX[i];
    }
    unordered_map<string, int> dSpy;
    for (int i = 0; i < C; ++i) {
        cin >> temp;
        dSpy[temp]++;
    }
    vector<string> ans;
    for (int i = 0; i < B; ++i) {
        if (allName[spyX[i]] == 1 && dSpy[spyX[i]] == 0) {
            ans.push_back(spyX[i]);
        }
    }
    if (ans.size() == 0) {
        cout << "No enemy spy" << endl;
    }
    else {
        for (int i = 0; i < ans.size() - 1; ++i) {
            cout << ans[i] << " ";
        }
        cout << ans[ans.size() - 1] << endl;
    }
}

int main()
{
    while (cin >> A >> B >> C) {
        Solution();
    }
    return 0;
}
```

# 5.Web导航（POJ1028，栈模拟）

[1028 -- Web Navigation (poj.org)](http://poj.org/problem?id=1028)

```Cpp
#include <iostream>
#include <vector>
#include <algorithm>
#include <math.h>
#include <string>
#include <stack>

using namespace std;

stack<string> back;
stack<string> forw;
string curUrl = "http://www.acm.org/";
vector<string> output;

void Solution(string& cmd) {
    if (cmd[0] == 'V') {
        back.push(curUrl);
        while (!forw.empty()) {
            forw.pop();
        }
        cin >> curUrl;
        output.push_back(curUrl);
        return;
    }
    if (cmd[0] == 'B') {
        if (back.empty()) {
            output.push_back("Ignored");
            return;
        }
        else {
            forw.push(curUrl);
            curUrl = back.top();
            back.pop();
            output.push_back(curUrl);
            return;
        }
    }

    if (cmd[0] == 'F') {
        if (forw.empty()) {
            output.push_back("Ignored");
            return;
        }
        else {
            back.push(curUrl);
            curUrl = forw.top();
            forw.pop();
            output.push_back(curUrl);
            return;
        }
    }
}

int main()
{
    string cmd = "";
    while (cin >> cmd) {
        if (cmd[0] == 'Q') {
            break;
        }
        Solution(cmd);
    }
    for (int i = 0; i < output.size(); ++i) {
        cout << output[i] << endl;
    }
    return 0;
}
```

