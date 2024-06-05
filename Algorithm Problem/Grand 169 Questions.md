# Grand 169 Questions

作者：盘子ssa，QQ（2426966358），2023年1月22日

## 题目类型整理

## 哈希表

# 第一周

# 第七题-242. 有效的字母异位词

[242. 有效的字母异位词 - 力扣（Leetcode）](https://leetcode.cn/problems/valid-anagram/description/)

根据题意，要求我们比较两个字符串中字母出现次数是否相同。

所以，我们需要分别记录s字符串和t字符串中，每一个字母出现的次数。

具体来说，使用两个长度为26的int型数组，遍历两个字符串，将字母出现次数记录下来；

然后，通过遍历两个记录数组，比较这两个数组当中的内容，是否相同就可以了。

> 其实，这就是哈希表的思想，只不过事先确定了哈希表的元素个数，并且哈希表的键是已知的。

```C#
public class Solution {
    public bool IsAnagram(string s, string t) {
        int[] cntS = new int[26];
        int[] cntT = new int[26];
        for (int i = 0; i < s.Length; ++i) {
            ++cntS[s[i] - 'a'];
        }
        for (int i = 0; i < t.Length; ++i) {
            ++cntT[t[i] - 'a'];
        }
        for (int i = 0; i < 26; ++i) {
            if (cntS[i] != cntT[i]) {
                return false;
            }
        }
        return true;
    }
}
```

# 第八题-704. 二分查找

[704. 二分查找 - 力扣（Leetcode）](https://leetcode.cn/problems/binary-search/description/)

经典的查找算法，二分查找是运用在有序序列中的一种查找算法，通过确定左边界和右边界，判定目标值和中间值是否相同，逐步的缩小查找范围，最终找到查找内容。

具体来说，就是有一个左边界left，右边界right，判断两边界的中点mid是否是查找内容，是则返回，不是则根据mid的大小，来缩小边界，mid < target则left变为mid + 1，反之right = mid - 1。每次缩小查找范围一半，直到最终查找到target。

> 注意：我们需要每次更新mid，因为left和right每查找一次也都在更新。

## 为什么需要left <= right?

为了防止数组长度为奇数且nums[right] == target或nums[left] == target的情况出现。

```C#
public class Solution {
    public int Search(int[] nums, int target) {
        int left = 0;
        int right = nums.Length - 1;
        while (left <= right) {
            int mid = (left + right) / 2;
            if (nums[mid] == target) {
                return mid;
            }
            if (nums[mid] < target) {
                left = mid + 1;
            }
            else {
                right = mid - 1;
            }
        }
        return -1;
    }
}
```

# 第九题-733. 图像渲染

[733. 图像渲染 - 力扣（Leetcode）](https://leetcode.cn/problems/flood-fill/description/)

经典的搜索练习题

我们记image\[sr\]\[sc\]值为oldColor

根据题意，我们需要将image\[sr\]\[sc\]相邻四个方向的，并且一样是oldColor的方格，全部涂成newColor

再将这四个方格相邻的四个方向的，并且一样是oldColor的方格

全部涂成newColor（赋值），直到某一个方格不再是oldColor。

## 特殊情况

考虑特殊情况，一开始image\[sr\]\[sc\]，也就是oldColor就是newColor，我们就不需要再进行涂色了，因为已经涂好了。

## 深度优先搜索

很明显，我们可以使用深度优先搜索（递归）完成这个问题

每遇到一个值为oldColor的方格，就调用一次这个函数，进行涂色并遍历这个方格的四个方向，直到某一个方格不再是oldColor。

```C#
public class Solution {
    int[,] dir = new int[4, 2] { 
        {1, 0}, {-1, 0}, {0, 1}, {0, -1}
    };
    int m;
    int n;
    public void Dfs(int[][] image, int x, int y, int oldColor, int newColor) {
        if (image[x][y] == oldColor) {
            image[x][y] = newColor;
            for (int i = 0; i < 4; ++i) {
                int nx = x + dir[i, 0];
                int ny = y + dir[i, 1];
                if (nx >= 0 && ny >= 0 && nx < m && ny < n) {
                    Dfs(image, nx, ny, oldColor, newColor);
                }
            }
        }
    }

    public int[][] FloodFill(int[][] image, int sr, int sc, int color) {
        if (image[sr][sc] == color) {
            return image;
        }
        m = image.GetLength(0);
        n = image[0].Length;
        Dfs(image, sr, sc, image[sr][sc], color);
        return image;
    }
}
```

## 广度优先搜索

很明显，我们可以使用队列来模拟以上递归行为

将每一个是oldColor的方格的坐标入队并涂色为newColor

搜索这个坐标的四个方向，如果仍然是oldColor就再入队，并涂色。

```C#
public class Solution {
    int[,] dir = new int[4, 2]{
        {1, 0}, {-1, 0}, {0, 1}, {0, -1}
    };
    int colLen;
    int rowLen;

    public int[][] FloodFill(int[][] image, int sr, int sc, int color) {
        if (image[sr][sc] == color) {
            return image;
        }
        colLen = image[0].Length;
        rowLen = image.GetLength(0);
        Queue<int[]> que = new Queue<int[]>();
        que.Enqueue(new int[] {sr, sc});
        int oldColor = image[sr][sc];
        image[sr][sc] = color;
        while (que.Count != 0) {
            int[] curCell = que.Dequeue();
            int x = curCell[0];
            int y = curCell[1];
            for (int i = 0; i < 4; ++i) {
                int nx = x + dir[i, 0];
                int ny = y + dir[i, 1];
                if (nx >= 0 && ny >= 0 && nx < rowLen && ny < colLen && image[nx][ny] == oldColor) {
                    que.Enqueue(new int[]{nx, ny});
                    image[nx][ny] = color;
                }
            }
        }
        return image;
    }
}
```

# 第10题-235. 二叉搜索树的最近公共祖先

## 常规做法，后序遍历

[235. 二叉搜索树的最近公共祖先 - 力扣（Leetcode）](https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-search-tree/)

寻找p和q的最近公共祖先，首先需要查找到p或者q。

我们使用后续遍历查找，一旦查找到p或者q或者nullptr，直接返回当前root并记录为left和rihgt。

查找过后

判断当记录的right == nullptr 时，说明右子树没有p或者q，即不存在公共祖先，返回left；

当记录的left== nullptr 时，说明左子树没有p或者q，即不存在公共祖先，返回right。

如果两者都不是nullptr，说明当前root就是两者的最近公共祖先，直接返回root。

在p为q的祖先的情况下，这种方法仍然适用，因为p为q的祖先，由于判断查找到p或者q或者nullptr就直接返回，

所以p会一直作为答案返回回去。

> 此方法适用于所有二叉树，因为只是使用了树的特性。

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */

public class Solution {
    public TreeNode LowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == p || root == q || root == null) {
            return root;
        }
        TreeNode left = LowestCommonAncestor(root.left, p, q);
        TreeNode right = LowestCommonAncestor(root.right, p, q);
        if (left == null) {
            return right;
        }
        if (right == null) {
            return left;
        }
        return root;
    }
}
```

## 使用二叉搜索树的特性

因为是二叉搜索树，所以根节点一定大于左子树的所有节点，一定小于右子树的所有节点。

所以，我们可以直接根据此特性查找他们的最近公共祖先：

假设p的值为0，q的值为4

如果当前节点的值**大于p和q的值**，那么他们的最近公共祖先一定在当前节点的左子树

因为还有比q更小的数在他们中间。

如果当前节点的值**小于p和q的值**，那么他们的最近公共祖先一定在当前节点的右子树

因为还有比p更大的数在他们中间。

如果当前节点的值**>=p，小于<=q的值**，那么这个节点就是他们的最近公共祖先。

对于p是q的祖先情况，由于查找到p时，就已经满足第三个条件了，就直接返回了。

> 此方法只适用于具有二叉搜索性质的树

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */

public class Solution {
    public TreeNode LowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root.val > p.val && root.val > q.val) {
            return LowestCommonAncestor(root.left, p, q);
        }
        if (root.val < p.val && root.val < q.val) {
            return LowestCommonAncestor(root.right, p, q);
        }
        return root;
    }
}
```

# 第11题-110. 平衡二叉树

[110. 平衡二叉树 - 力扣（Leetcode）](https://leetcode.cn/problems/balanced-binary-tree/)

根据题意，我们需要判断一颗树是否是平衡二叉树

平衡二叉树就是指：**每个节点** 的左右两个子树的高度差的绝对值不超过 1 。

## 方法一，直接计算高度

很容易想到，我们可以计算每一个节点的子树的高度，然后判断高度差，进而判断是否平衡。

具体的，我们需要计算每一个节点的高度，然后再判断这个节点的左右子树是否也是平衡。

我们可以使用递归，先判断当前节点的左子树高度和右子树高度的差值，再判断这个节点的**左右子树**是否也是平衡；

递归的结束条件就是当该节点为nullptr。

计算树的高度可以定义一个Height函数来解决。

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    int Height(TreeNode root) {
        if (root == null) {
            return 0;
        }
        else {
            return Math.Max(Height(root.left), Height(root.right)) + 1;
        }
    }

    public bool IsBalanced(TreeNode root) {
        if (root == null) {
            return true;
        }
        else {
            return Math.Abs(Height(root.left) - Height(root.right)) <= 1 && IsBalanced(root.left) && IsBalanced(root.right);
        }
    }
}
```

## 方法二，后续遍历

我们也可以使用后续遍历来计算子树的高度，并通过返回的数值，进而判断是否是平衡二叉树。

具体的，记录左子树的高度leftHeight，记录右子树的高度rightHeight；

当两子树的高度差大于1时，**直接返回-1**作为**不是**平衡二叉树的标记；

否则返回他们的子树的**高度**，作为**是**平衡二叉树的标记。

这是因为，我们已经知道有两子树的高度差大于1了，这棵树已经不是平衡二叉树了。

并且leftHeight，rightHeight也需要判断是否为-1，因为当前树的子树的子树不平衡，整棵树也就不平衡了。

> 其实，这种方法和第一种方法差不多，只不过是将递归发生在Height函数，而没有发生在IsBalanced函数而已。

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    int height(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int leftHeight = height(root.left);
        int rightHeight = height(root.right);
        if (leftHeight == -1 || rightHeight == -1 || Math.Abs(leftHeight - rightHeight) > 1) {
            return -1;
        }
        else {
            return Math.Max(leftHeight, rightHeight) + 1;
        }
    }

    public bool IsBalanced(TreeNode root) {
        return height(root) >= 0;
    }
}
```

# 第12题-141. 环形链表

[141. 环形链表 - 力扣（Leetcode）](https://leetcode.cn/problems/linked-list-cycle/)

## 方法一，哈希表

很容易想到，判断是否有环，只需要判断某个环中的节点是否重复出现过。

判断是否重复出现过，我们就可以使用哈希表来解决。

具体的，我们遍历这个链表，将没有存到哈希表中的节点存到哈希表当中，一旦遇到已经保存过的节点，直接返回true，因为有环。如果直到遍历完链表还是没有遇到重复节点，返回false。

### 特殊情况

1. 当链表为空时，会直接返回false。
2. 当只有一个节点且无环时，会返回false。

```C#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public bool HasCycle(ListNode head) {
        Dictionary<ListNode, int> dic = new Dictionary<ListNode, int>();
        while(head != null) {
            if (!dic.ContainsKey(head)) {
                dic.Add(head, 1);
            }
            else {
                return true;
            }
            head = head.next;
        }
        return false;
    }
}
```

## 方法二，快慢指针

使用快慢指针

想象一下，两个人在一个操场在同一起点同时开始跑步（操场就是一个环）；

如果A比B跑的快，那么经过一段时间过后，他们一定会在操场的某一个点相遇（就相当于A超过了B好长一段距离）。

> 具体的，可以去搜索一下Floyd 判圈算法，明白这个道理就好。

快慢指针就是运用以上思想，使用一个slow = head，一个fast = head。

遍历这个链表，slow每次走一步，fast每次走两步，当两者相遇时，则一定有环；

当slow或者fast跑到链表终点时，一定无环。

由于是fast跑的最快，所以，遍历链表时，可以直接判断fast和fast.next是否为空。

### 特殊情况

1. 只有一个节点，但是没环，我需要进行特判，直接返回false。
2. 当链表为空时，需要特殊判断，直接返回false。

```C#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public bool HasCycle(ListNode head) {
        if (head == null || head.next == null) {
            return false;
        }
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                return true;
            }
        }
        return false;
    }
}
```

# 第13题-232. 用栈实现队列

[232. 用栈实现队列 - 力扣（Leetcode）](https://leetcode.cn/problems/implement-queue-using-stacks/)

队列即先进先出

## 双栈模拟队列

考虑到栈的特性，先进后出，为了模拟队列的先进先出。

我们可以使用一个输入栈，用来保存Push时的数据。

使用一个输出栈，用来在Pop或者Peek时，输出数据。

当Pop或者Peek，并且输出栈为空时，我们将输入栈所有数据出栈，并存储进输出栈，再返回输出栈栈顶元素即可。其实，这是做了一次倒转的操作。

### 为什么需要判断输出栈为空才进行倒转？

因为一次判空，进行倒转后，输出栈的输出顺序就固定了，不能改变。

如果每次Pop或者Peek都将输入站倒转到输出栈，就会发生错位。

```C#
public class MyQueue {
    Stack<int> inSta;
    Stack<int> outSta;
    public MyQueue() {
        inSta = new Stack<int>();
        outSta = new Stack<int>();
    }
    
    public void Push(int x) {
        inSta.Push(x);
    }
    
    public int Pop() {
        if (outSta.Count == 0) {
            while (inSta.Count != 0) {
                outSta.Push(inSta.Pop());
            }
        }
        return outSta.Pop();
    }
    
    public int Peek() {
        if (outSta.Count == 0) {
            while (inSta.Count != 0) {
                outSta.Push(inSta.Pop());
            }
        }
        return outSta.Peek();
    }
    
    public bool Empty() {
        return outSta.Count == 0 && inSta.Count == 0;
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.Push(x);
 * int param_2 = obj.Pop();
 * int param_3 = obj.Peek();
 * bool param_4 = obj.Empty();
 */
```

# ----------------------------------

# 第二周

# 第1题-278. 第一个错误的版本

[278. 第一个错误的版本 - 力扣（Leetcode）](https://leetcode.cn/problems/first-bad-version/)

根据题意，给定1到n个数，每个数代表一个版本。

我们需要查找到，第一个错误的版本。

注意到，第一个错误的版本之前的版本都是正确的；第一个错误的版本之后的版本都是错误的。

很容易想到，可以直接暴力查找，遍历1到n，每次都检查这个版本是否正确，一遇到第一个错误的版本就返回。

时间复杂度为O(n)。

但是根据题目提示，提示我们应该尽量减少版本检查函数api的调用次数，不然会超时。

所以，考虑另一种查找算法。

注意到，版本号为1到n，是一个有序序列，并且第一个错误的版本**之前的版本都是正确**的。

所以，我们可以使用**二分查找**。

具体的，二分查找时，判断mid是否是错误版本。

是则说明第一个错误的版本在\[left, mid\]，因为第一个错误的版本之后的版本都是错误的。

不是则说明第一个错误的版本在\[mid + 1, right]，因为第一个错误的版本之前的版本都是正确的。

最后当left == right时，就是查找到了第一个错误的版本，返回即可。

使用二分查找的时间复杂度为O(logn)。

```C#
/* The isBadVersion API is defined in the parent class VersionControl.
      bool IsBadVersion(int version); */

public class Solution : VersionControl {
    public int FirstBadVersion(int n) {
        int left = 1;
        int right = n;
        while (left < right) {
            int mid = left + (right - left) / 2;
            if (base.IsBadVersion(mid)) {
                right = mid;
            }
            else {
                left = mid + 1;
            }
        }
        return left;
    }
}
```

# 第2题-383. 赎金信

[383. 赎金信 - 力扣（Leetcode）](https://leetcode.cn/problems/ransom-note/)

根据题意，我们需要判断判断 `ransomNote` 能不能由 `magazine` 里面的字符构成；

`magazine` 中的每个字符只能在 `ransomNote` 中**使用一次**。

判断字符是否在出现过，很容易想到，可以使用哈希表来解决。

我们记录`magazine`里面所有出现过的字符，然后遍历`ransomNote`中的所有字符；

判断`ransomNote`中的字符是否出现在记录里，如果有字符未出现返回false，否则将记录-1。

为了方便，我们可以直接使用长度为26的数组来记录。

因为题目说明了`ransomNote` 和`magazine` 全都由小写英文字母组成。

```C#
public class Solution {
    public bool CanConstruct(string ransomNote, string magazine) {
        int[] hashTable = new int[26];
        foreach (char item in magazine) {
            hashTable[item - 'a']++;
        }
        foreach (char item in ransomNote) {
            hashTable[item - 'a']--;
            if (hashTable[item - 'a'] < 0) {
                return false;
            }
        }
        return true;
    }
}
```

# 第3题-70. 爬楼梯

[70. 爬楼梯 - 力扣（Leetcode）](https://leetcode.cn/problems/climbing-stairs/)

经典的动态规划入门题。

根据题意，我们拥有两种爬楼梯的方式：一次爬一级，一次爬两级。

考虑爬一级台阶，有1种方法（爬一次一级）；

考虑爬二级台阶，有2种方法（爬两次一级，爬一次两级）；

考虑爬三级台阶，我们要到三级台阶，首先要到一级台阶或者到二级台阶；

然后再爬两次一级或者一次两级或者一次一级就能到达三级台阶。

因为这三种方法是在前三种方法的基础上的，并且只有三种可能，所以，不能添加爬楼梯的方法数。

而到一级或者二级台阶分别有1种和2种方法，所以爬三级台阶的方法数一共有1 + 2 = 3种。

这三种分别是

1. **爬一次一级，爬一次一级**，爬一次一级
2. **爬一次一级**，爬一次两级
3. **爬一次两级**，爬一次一级

由上述推断，我们发现，爬到当前级数的方法数，只与爬到前两个（cur - 1，cur - 2）级数的方法数有关。

所以，可以总结出递推式**F(x) = F(x - 1) + F(x - 2)，x为级数，x >= 3**

所以有了以上的递推式。

如此，我们就可以将F(x - 2) 设为a，F(x - 1)设为b，初始时，a = 1，b = 2。

然后使用循环，依次递推出F(n)，如果n == 1 或 n == 2，就直接返回1或2。

> 我们可以发现，这其实就是斐波那契数列

```C#
public class Solution {
    public int ClimbStairs(int n) {
        if (n == 1 || n == 2) {
            return n;
        }
        int a = 1;
        int b = 2;
        int ret = 0;
        for (int i = 3; i <= n; ++i) {
            ret = a + b;
            a = b;
            b = ret;
        }
        return ret;
    }
}
```

# 第4题-409. 最长回文串

[409. 最长回文串 - 力扣（Leetcode）](https://leetcode.cn/problems/longest-palindrome/)

根据题意，我们需要将一个字符串中的字符重新组合，使得它们组成一个新的字符串。

这个新的字符串是一个回文串，并且是能组成的回文串当中最长的一个。

如果有不能使用的个别字符，我们需要将它们抛弃。

注意：我们只需要返**回回文串的长度**。

## 如何将原有字符转换为回文字符串？

我们知道，回文字符串中的字符，可能除了中心字符外

其他字符都是成对出现的，即除了中心字符外，其他都是偶数。

如此，我们只需要标记一下，中心字符使用奇数个，然后其他字符全部都使用偶数个数就好了

具体的，我们记录每个字符出现的个数，设立一个**centerFlag**作为中心字符使用奇数个数的标记。

遍历我们的记录数组，判断centerFlag是否使用过。

未使用，我们就将某个**奇数个数**的字符作为中心字符，并加到长度中去。

否则则使用字符个数的**偶数个数**，并加到长度中去。

由于最中心字符也就**只有一个**，所以这样组合成的字符串是最长的回文串。

由于题目说明只有字母，所以根据ASCII码表，我们可以使用一个长度为128的数组记录字母出现的个数。

因为字母的ASCII码值最多也就到97 + 26 = 123。

```C#
public class Solution {
    public int LongestPalindrome(string s) {
        int[] count = new int[128];
        foreach (char item in s) {
            count[item]++;
        }
        int ret = 0;
        bool centerFlag = true;
        for (int i = 0; i < 128; ++i) {
            if (centerFlag && count[i] % 2 == 1) {
                ret += count[i];
                centerFlag = false;
            }
            else {
                ret += count[i] / 2 * 2;
            }
        }
        return ret;
    }
}
```

# 第5题-206. 反转链表

[206. 反转链表 - 力扣（Leetcode）](https://leetcode.cn/problems/reverse-linked-list/)

## 迭代

根据题意，要翻转整个链表，首先需要翻转每一个节点。

那么，翻转每一个节点，我们需要记录下来三个节点

当前节点curNode，前一个节点preNode，后一个节点next。

因为，当前节点只与这两个节点有关。

然后，我们需要将当前节点的下一个节点连接到前一个节点；也就是curNode.next = preNode;

为了继续翻转，我们还需要将preNode和curNode更新，也就是：preNode = curNode; curNode = next; 

最后，我们需要返回preNode，因为这时候，preNode就是新的头结点。

注意：我们不修改val，只修改next，就能实现翻转。初始化时preNode = nullptr。

```C#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public ListNode ReverseList(ListNode head) {
        ListNode curNode = head;
        ListNode preNode = null;
        while (curNode != null) {
            ListNode next = curNode.next;
            curNode.next = preNode;
            preNode = curNode;
            curNode = next;
        }
        return preNode;
    }
}
```

## 递归

很明显，上述循环可以使用递归来实现。

而递归函数的参数，就是在循环外部定义的两个变量，即curNode和preNode。

递归函数的出口，就是curNode == null，最终我们需要返回preNode，即新的头结点。

```C#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public ListNode Helper(ListNode preNode, ListNode curNode) {
        if (curNode == null) {
            return preNode;
        }
        ListNode next = curNode.next;
        curNode.next = preNode;
        return Helper(curNode, next);
    }

    public ListNode ReverseList(ListNode head) {
        return Helper(null, head);
    }
}
```

# 第6题-169. 多数元素

[169. 多数元素 - 力扣（Leetcode）](https://leetcode.cn/problems/majority-element/)

根据题意，我们需要查找到数组当中出现次数>= 数组长度 / 2的元素。

## 哈希表

看到出现次数，我们很容易想到，记录每一个数出现的次数，然后遍历记录数组；

最后返回出现次数>= 数组长度 / 2的元素即可。

> 注意：根据题意我们可以发现，多数元素只可能**有一个**。
>
> 因为出现次数大于 n / 2的元素只可能有一个。

```C#
public class Solution {
    public int MajorityElement(int[] nums) {
        Dictionary<int, int> hashTable = new Dictionary<int, int>();
        foreach (int item in nums) {
            if (hashTable.ContainsKey(item)) {
                hashTable[item]++;
            }
            else {
                hashTable.Add(item, 1);
            }
        }
        foreach (int item in hashTable.Keys) {
            if (hashTable[item] > nums.Length / 2) {
                return item;
            }
        }
        return 1;
    }
}
```

## 直接排序

由于根据题意我们可以发现，多数元素只可能有一个，并且出现次数**大于** n / 2。

所以，我们可以直接对于数组进行排序，然后直接返回中位数。

因为排序之后，数组的中位数，一定是多数元素（因为多数元素出现次数**大于 n / 2**）。

```C#
public class Solution {
    public int MajorityElement(int[] nums) {
       	Array.Sort(nums);
       	return nums[nums.Length / 2];
    }
}
```

# 第7题-67. 二进制求和

[67. 二进制求和 - 力扣（Leetcode）](https://leetcode.cn/problems/add-binary/)

## 从后方开始模拟计算

根据题意，需要模拟计算二进制加法。

计算加法，就需要从后方开始，一位一位的计算，并且需要对进位进行标识。

还需要注意两个字符串长度不一致的问题。

所以，我们从后方开始计算，使用一个标记记录进位。	

当计算完之后，我们需要判断a或者b字符串是否遍历完全，如果没遍历完，我们需要再将他们放到答案当中去。

在都遍历完之后，还需要判断是否还有进位，因为这时候也有可能有进位。

```C#
public class Solution {
    public string AddBinary(string a, string b) {
        int aIndex = a.Length - 1;
        int bIndex = b.Length - 1;
        StringBuilder ret = new StringBuilder();
        int carry = 0;
        while (aIndex >= 0 && bIndex >= 0) {
            int tempRet = (a[aIndex--] - '0' + b[bIndex--] - '0') + carry;
            ret.Append(Convert.ToChar(tempRet % 2 + '0'));
            carry = tempRet / 2;
        }
        while (aIndex >= 0) {
            int tempRet = (a[aIndex--] - '0') + carry;
            carry = tempRet / 2;
            ret.Append(Convert.ToChar(tempRet % 2 + '0'));
        }
        while (bIndex >= 0) {
            int tempRet = (b[bIndex--] - '0') + carry;
            carry = tempRet / 2;
            ret.Append(Convert.ToChar(tempRet % 2 + '0'));
        }
        if (carry == 1) {
            ret = new StringBuilder(ret.ToString() + "1");
        }
        char[] temp = ret.ToString().ToCharArray();
        Array.Reverse(temp);
        return new String(temp);
    }
}
```

# 第8题-543. 二叉树的直径

[543. 二叉树的直径 - 力扣（Leetcode）](https://leetcode.cn/problems/diameter-of-binary-tree/description/)

根据题意，二叉树的直径是任意两个结点路径长度中的最大值。

两结点之间的路径长度是它们之间**边的数目**。

任意两个结点路径长度中的最大值

一定可以看作是以某个节点**作为根节点**，并**作为路径中间的**（经过的）节点，**左右两颗子树**的**深度之和**。

如此，我们只需要以当前节点作为根节点，求得左右两颗子树的深度，并求和；

取左右两颗子树的**深度之和的最大值**即可。

具体的，我们使用一个全局变量ret作为答案，使用**后续遍历**，求得以当前节点为根节点，**左右两颗子树**的深度。

然后用左右两颗子树的深度之和和答案比较，取最大值即可。

## 为什么左右两颗子树的深度之和可以作为答案？

因为我们求得的**左右两颗子树的深度之和**，就是以当前节点**作为路径中间的**（经过的）节点，能求得的最大路径的长度。

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    int ret = 0;
    public int Depth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int left = Depth(root.left);
        int right = Depth(root.right);
        ret = Math.Max(ret, left + right);
        return Math.Max(left, right) + 1;
    }
    public int DiameterOfBinaryTree(TreeNode root) {
        Depth(root);
        return ret;
    }
}
```

# 第9题-876. 链表的中间结点

[876. 链表的中间结点 - 力扣（Leetcode）](https://leetcode.cn/problems/middle-of-the-linked-list/)

## 使用额外空间

查找链表的中间节点，很容易想到，我们可以将链表结点全部存储到一个容器当中，然后返回这个容器的中心值即可。

注意：因为题目说明，链表一定有结点，所以我们不用在开头判空。

```C#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public ListNode MiddleNode(ListNode head) {
        List<ListNode> list = new List<ListNode>();
        while (head != null) {
            list.Add(head);
            head = head.next;
        }
        return list[list.Count / 2];
    }
}
```

## 快慢指针

第一种解法使用了额外的空间，并且需要遍历全部链表。

而使用快慢指针可以不使用额外空间，并且只需要遍历链表的一半。

我们使用slow和fast作为快慢指针，遍历链表，slow走一步，fast走两步。

当fast到达链表末尾时，slow一定在链表的中心结点。

很明显，这是因为slow的速度是fast的一半。

注意：因为题目说明，链表一定有结点，所以我们不用在开头判空。

```C#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public ListNode MiddleNode(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
}
```

# 第10题-104. 二叉树的最大深度

[104. 二叉树的最大深度 - 力扣（Leetcode）](https://leetcode.cn/problems/maximum-depth-of-binary-tree/description/)

## dfs

显然，和第8题一样，计算二叉树的最大深度，只需要递归计算两子树的深度，求最大值再加1（1是本身这层的深度）就好了。

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    public int MaxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int left = MaxDepth(root.left);
        int right = MaxDepth(root.right);
        return Math.Max(left, right) + 1;
    }
}
```

## bfs

任何求深度的问题，我们都可以使用层次遍历，也就是广度优先搜索来完成

具体的，就是使用队列，利用队列先进先出的特点，将每一层的节点都单独拿出来遍历。

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    public int MaxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int maxDepth = 0;
        Queue<TreeNode> que = new Queue<TreeNode>();
        que.Enqueue(root);
        while (que.Count != 0) {
            TreeNode curNode;
            int curLen = que.Count;
            for (int i = 0; i < curLen; ++i) {
                curNode = que.Dequeue();
                if (curNode.left != null) que.Enqueue(curNode.left);
                if (curNode.right != null) que.Enqueue(curNode.right);
            }
            ++maxDepth;
        }
        return maxDepth;
    }
}
```

# 第11题-217. 存在重复元素

[217. 存在重复元素 - 力扣（Leetcode）](https://leetcode.cn/problems/contains-duplicate/)

## 排序

根据题意，我们需要判断数组中是否有重复元素出现。

那么，我们可以将数组排序，然后遍历数组，判断当前元素是否和下一个元素想等，是返回true。

```C#
public class Solution {
    public bool ContainsDuplicate(int[] nums) {
        Array.Sort(nums);
        for (int i = 0; i < nums.Length - 1; ++i) {
            if (nums[i] == nums[i + 1]) {
                return true;
            }
        }
        return false;;
    }
}
```

## 哈希表

根据题意，我们需要判断数组中是否有重复元素出现。

很容易想到，我们可以使用哈希表来记录每一个元素，如果某一个元素重复出现，直接返回true。

```C#
public class Solution {
    public bool ContainsDuplicate(int[] nums) {
        Dictionary<int, int> hashTable = new Dictionary<int, int>();
        foreach (int item in nums) {
            if (hashTable.ContainsKey(item)) {
                return true;  
            }
            else {
                hashTable.Add(item, 1);
            }
        }
        return false;;
    }
}
```

# 第12题-252. 会议室

[252. 会议室 - 力扣（Leetcode）](https://leetcode.cn/problems/meeting-rooms/)

题目描述
给定一个会议时间安排的数组，每个会议时间都会包括开始和结束的时间 [[s1,e1],[s2,e2],...] (si < ei)，请你判断一个人是否能够参加这里面的全部会议。

示例 1:

```C#
输入: [[0,30],[5,10],[15,20]]
输出: false
```


示例 2:

```C#
输入: [[7,10],[2,4]]
输出: true
```

代码:

```C#
class Solution {
public:
    bool canAttendMeetings(vector<vector<int>>& intervals) {
        
    }
};
```

## 排序，判断区间是否重合

因为要求要一个人能参加**所有**会议。

所以，我们需要检查给定的时间区间是否有重合的地方，如果有重合，说明不能参加所有会议。

为了简便的检查时间区间是否有重合，我们可以先将给定的区间按开始时间排序，然后检查是否有重合即可。

```C#
public bool canAttendMeetings(List<List<int>> intervals)
{
    intervals.Sort((List<int> lhs, List<int> rhs) =>
                   {
                       return lhs[0] < rhs[0] ? -1 : 1;
                   });
    for (int i = 0; i < intervals.Count - 1; ++i)
    {
        if (intervals[i][1] > intervals[i + 1][1])
        {
            return false;
        }
    }
    return true;
}
```

# ----------------------------------

# 第三周

# 第1题-13. 罗马数字转整数

[13. 罗马数字转整数 - 力扣（Leetcode）](https://leetcode.cn/problems/roman-to-integer/submissions/399385929/)

根据题意，要求我们根据给定的罗马数字转整数。

我们需要遍历整个字符串，然后计算他们的累加和，最终得出答案。

罗马数字对应规则如下

```C#
字符          数值
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

- `I` 可以放在 `V` (5) 和 `X` (10) 的左边，来表示 4 和 9。
- `X` 可以放在 `L` (50) 和 `C` (100) 的左边，来表示 40 和 90。 
- `C` 可以放在 `D` (500) 和 `M` (1000) 的左边，来表示 400 和 900。

## 哈希表，无优化

观察得知，罗马数字可能由两个字符或者一个字符构成；

罗马数字转整数，主要的难点在于，如何解决由两个字符构成的罗马数字。

对于由一个字符构成的罗马数字，我们可以使用哈希表进行处理。

对于由两个字符构成的罗马数字，直接在遇到`I` ，`X`，`C` 时，判断下一个字符是否是 `V` `X`,`L` `C`,  `D`  `M` 

以此来判断是否是 4 和 9；40 和 90；400 和 900。

具体的，我们使用哈希表存储单个字符对应的罗马数字，使用ret来累加记录答案。

在遍历字符串时，使用一个cur记录当前字符，使用一个next记录下一个字符，依次判断，然后计算累加和即可。

```C#
public class Solution {
    public int RomanToInt(string s) {
        Dictionary<char, int> hash = new Dictionary<char, int>() {
            {'I', 1},
            {'V', 5},
            {'X', 10},
            {'L', 50},
            {'C', 100},
            {'D', 500},
            {'M', 1000},
        };
        int ret = 0;
        for (int i = 0; i < s.Length; ++i) {
            char cur = s[i];
            char next = ' ';
            if (i + 1 < s.Length) {
                next = s[i + 1];
            }
            if (cur == 'I' && (next == 'V' || next == 'X')) {
                ret += hash[next] - hash[cur];
                ++i;
            }
            else if (cur == 'X' && (next == 'L' || next == 'C')) {
                ret += hash[next] - hash[cur];
                ++i;
            }
            else if (cur == 'C' && (next == 'D' || next == 'M')) {
                ret += hash[next] - hash[cur];
                ++i;
            }
            else {
                ret += hash[cur];
            }
        }
        return ret;
    }
}
```

## 哈希表，优化判断

通过观察，我们可以得知：

如果罗马数字是由两个字符构成的，则第一个字符对应数值一定小于第二个字符对应数值。

并且，我们需要减去第一个字符的对应数值，加上第二个字符的对应数值。

根据上述规律，我们可以直接在遍历时判断当前字符对应数值是否小于第二个数值，是则减去当前数值。

```C#
public class Solution {
    public int RomanToInt(string s) {
        Dictionary<char, int> hash = new Dictionary<char, int>() {
            {'I', 1},
            {'V', 5},
            {'X', 10},
            {'L', 50},
            {'C', 100},
            {'D', 500},
            {'M', 1000},
        };
        int ret = 0;
        for (int i = 0; i < s.Length; ++i) {
            int cur = hash[s[i]];
            if (i + 1 < s.Length && cur < hash[s[i + 1]]) {
                ret -= cur;
            }
            else {
                ret += cur;
            }
            
        }
        return ret;
    }
}
```

# 第2题-844. 比较含退格的字符串

## 从左栈模拟

根据题意，需要判断退格后的字符串，是否仍然相同。

所以，我们可以遍历两个字符串，直接模拟退格的操作，产生两个个新的不含退格（\#号）的字符串。

最后比较两个字符串是否相等即可。

具体的，遍历字符串，遇到不是\#号，是正常字符，将其添加到新字符串末尾；

否则将新字符串中的最后一个删除。

由于需要频繁的插入末尾元素，删除末尾元素，我们使用栈来存储新的字符串。

最后先判断栈长度是否相同，再将元素出栈并比较是否相等，返回答案即可。

```C#
public class Solution {
    public bool BackspaceCompare(string s, string t) {
        Stack<char> tempS = new Stack<char>();
        Stack<char> tempT = new Stack<char>();
        foreach (char item in s) {
            if (item != '#') {
                tempS.Push(item);
            }
            else if (tempS.Count != 0){
                tempS.Pop(); 
            }
        }
        
        foreach (char item in t) {
            if (item != '#') {
                tempT.Push(item);
            }
            else if (tempT.Count != 0){
                tempT.Pop(); 
            }
        }
        while (tempS.Count != 0 && tempT.Count != 0) {
            if (tempS.Pop() != tempT.Pop()) {
                return false;
            }
        }
        return tempS.Count == tempT.Count;
    }
}
```

# 第3题-338. 比特位计数

根据题意，要求我们计算出0~n的每个数的二进制1的个数。

## 暴力

首先考虑计算一个数的二进制1的个数。

假设当前数为n，我们可以让n & 1，这样就计算得出，n的二进制（从右往左数）的第一位是否为1。

如果n & 1，说明有一个1，我们记一次数。

然后第一位已经计算过了，我们就将n >>= 1，右移一位，取下一位的二进制数，循环，知道n为0为止。

而计算0~n的每个数的二进制1的个数，我们也只需要使用一个循环来计算。

```C#
public class Solution {
    public int CountOne(int n) {
        int ret = 0;
        while (n != 0) {
            if ((n & 1) != 0) {
                ++ret;
            }
            n >>= 1;
        }
        return ret;
    }

    public int[] CountBits(int n) {
        int[] ans = new int[n + 1];
        for (int i = 0; i <= n; ++i) {
            ans[i] = CountOne(i);
        }
        return ans;
    }
}
```

## 动态规划，利用已经计算好的二进制1个数

由于我们在计算n的二进制1个数时，n / 2的二进制个数一定是已经计算好的。

所以，我们可以利用n / 2的二进制个数，来计算出当前数的二进制1个数。

由于二进制的特性，如果n是偶数，n的二进制1个数，一定等于n / 2的二进制1个数。

如果n是奇数，n的二进制1个数，一定等于n / 2的二进制个数 + 1。

> 还有其他关于二进制计算的方法，大家感兴趣可以去

```C#
public class Solution {
    public int[] CountBits(int n) {
        int[] ans = new int[n + 1];
        for (int i = 1; i <= n; ++i) {
            if (i % 2 == 0) {
                ans[i] = ans[i / 2];
            }
            else {
                ans[i] = ans[i / 2] + 1;
            }
        }
        return ans;
    }
}
```

# 第4题-100. 相同的树

[100. 相同的树 - 力扣（Leetcode）](https://leetcode.cn/problems/same-tree/description/)

## 递归

要判断两棵树是否相同，需要判断它们的结构和节点值是否全部相同。

首先考虑判断一个节点是否相同：

不同的情况（包括了结构判断）：

1. p为null，q不为null
2. p不为null，q为null
3. p.val != q.val

相同的情况：

1. p == null, q == null
2. p.val == q.val

判断完当前节点是否相同后，我们还需要考虑它们的左右两个子节点是否相同；

既然如此，我们直接递归调用两次这个函数，用以判断左右两子节点是否相同即可。

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    public bool IsSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) {
            return true;
        }
        else if (p == null || q == null) {
            return false;
        }
        else if (p.val != q.val) {
            return false;
        }
        else {
            return IsSameTree(p.left, q.left) && IsSameTree(p.right, q.right);
        }
    }
}
```

## 层次遍历

考虑使用迭代来完成。

判断两棵树是否相同，很显然，我们可以使用层次遍历来完成。

使用两个队列来同时对两棵树进行层次遍历，判断当前层的元素和结构是否完全相同即可。

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    public bool IsSameTree(TreeNode p, TreeNode q) {
        Queue<TreeNode> pQue = new Queue<TreeNode>();
        Queue<TreeNode> qQue = new Queue<TreeNode>();
        if (p != null) {
            pQue.Enqueue(p);
        }
        if (q != null) {
            qQue.Enqueue(q);
        }
        while (pQue.Count != 0 && qQue.Count != 0) {
            int pLen = pQue.Count;
            int qLen = qQue.Count;
            if (pLen != qLen) {
                return false;
            }
            for (int i = 0; i < pLen; ++i) {
                TreeNode tempP = pQue.Dequeue();
                TreeNode tempQ = qQue.Dequeue();
                if (tempP.val != tempQ.val) {
                    return false;
                }
                if (tempP.left != null && tempQ.left == null) {
                    return false;
                }
                if (tempP.left == null && tempQ.left != null) {
                    return false;
                }
                if (tempP.right != null && tempQ.right == null) {
                    return false;
                }
                if (tempP.right == null && tempQ.right != null) {
                    return false;
                }

                if (tempP.left != null) pQue.Enqueue(tempP.left);
                if (tempP.right != null) pQue.Enqueue(tempP.right);
                if (tempQ.left != null) qQue.Enqueue(tempQ.left);
                if (tempQ.right != null) qQue.Enqueue(tempQ.right);
            }
        }
        return pQue.Count == qQue.Count;
    }
}
```

# 第5题-191. 位1的个数

## 暴力，循环右移计算1的个数

如本周第三题中，计算二进制1的个数时采用的暴力方法一样，直接使用循环右移的方式计算二进制中1的个数

```C#
public class Solution {
    public int HammingWeight(uint n) {
        int ret = 0;
        while (n != 0) {
            if ((n & 1) == 1) {
                ++ret;
            }
            n >>= 1;
        }
        return ret;
    }
}
```

## 暴力优化，n & (n - 1)计算1的个数

n & (n - 1)，恰好是这个数最后一个为1的位上的1去除之后的结果。

比如：

5 & (5 - 1)，即0101 & 0100 = 0100.

6 & (6 - 1)，即0110 & 0101 = 0100.

利用这个方法，我们可以加速计算n的二进制1的个数。

我们只需要判断当前数的是否为 > 0的数，然后每次对其进行n = n & (n - 1)的操作，每做一次操作，答案递增一次即可。

```C#
public class Solution {
    public int HammingWeight(uint n) {
        int ret = 0;
        while (n != 0) {
            n &= n - 1;
            ++ret;
        }
        return ret;
    }
}
```

# 第6题-14. 最长公共前缀

[14. 最长公共前缀 - 力扣（Leetcode）](https://leetcode.cn/problems/longest-common-prefix/description/)

要查找所有字符串的最长公共前缀，我们可以取第一个字符串作为标准，遍历第一个字符串的所有字符。

与其他每个字符串的对应位置进行比较，如果其他的某个字符长度不够，或者对应位置不相等，则直接返回第一个字符串的0到遍历位置的字符。

特殊情况：

1. 字符串数组里面没有字符，直接返回空字符串；

2. 字符串数组里面只有一个字符串，直接返回这个字符；

3. 字符串数组当中全是同样的字符

   由于全是同样的字符，无法在循环里面直接返回，所以，需要在最后返回一个strs\[0\]；

   由于最后会直接返回一个strs\[0\]，所以第二条特殊情况就可以不用判断了。

```C#
public class Solution {
    public string LongestCommonPrefix(string[] strs) {
        if (strs.Length == 0) {
            return "";
        }
        for (int i = 0; i < strs[0].Length; ++i) {
            for (int j = 1; j < strs.Length; ++j) {
                if (i == strs[j].Length || strs[0][i] != strs[j][i]) {
                    return strs[0].Substring(0, i);
                }
            }
        }
        return strs[0];
    }
}
```

# 第7题-136. 只出现一次的数字

## 哈希表（不符合题目要求）

要判断一个数只出现一次，很容易想到，我们可以使用哈希表来计数，然后遍历哈希表。

找出只出现一次的那个数。

```C#
public class Solution {
    public int SingleNumber(int[] nums) {
        Dictionary<int, int> hash = new Dictionary<int, int>();
        for (int i = 0; i < nums.Length; ++i) {
            if (hash.ContainsKey(nums[i])) {
                hash[nums[i]]++;
            }
            else {
                hash.Add(nums[i], 1);
            }
        }
        foreach (int key in hash.Keys) {
            if (hash[key] == 1) {
                return key;
            }
        }
        return 1;
    }
}
```

## 异或运算

使用哈希表不符合题目要求的O（1）空间复杂度，需要考虑另外的方法。

题目说明了其他数一定出现两次，我们可以利用这点解题。

三个数当中，有两个相同的数，要使得他们进行几次运算，最后变成其中某一个数，很容易想到使用位运算异或。

比如：1,2,2

2 ^ 2 = 0，0 ^ 1 = 1

得出1就是最终的答案。

具体的，使用一个ret记录答案，遍历数组。在遍历过程中，对每一个数与ret进行一次异或操作。

当遍历完数组，ret一定就是只出现过一次的那个数。

### 不是说要异或两个相同的数吗？为什么数组没有排序就可以使用这种方法？

由于题目说明了其他每个数一定出现两次。

举个例子：1，2，3，6，1，6，3，2，9

异或过程：1 ^ 2 ^ 3 ^ 6 ^ 1 ^ 6 ^ 3 ^ 2 ^ 9

我们可以将过程看成（1 ^ 2 ^ 3 ^ 6）^ （ 1 ^ 6 ^ 3 ^ 2 ）^ 9

这样其实也是两个相同的数在异或，所以最后都会变为0，

```C#
public class Solution {
    public int SingleNumber(int[] nums) {
        int ret = 0;
        for (int i = 0; i < nums.Length; ++i) {
            ret ^= nums[i];
        }
        return ret;
    }
}
```

# 第8题-234. 回文链表

## 使用额外空间，借助栈

要判断链表是否回文，需要从左到右，从右到左遍历依次判断结点值是否相同。

要从左到右遍历单向链表，我们可以直接遍历；

但是从右到左遍历单向链表，不能直接遍历。

所以，我们可以考虑将链表存储到栈当中，再通过出栈来反向遍历链表。

> 由于使用了额外的栈空间，不符合进阶要求

```C#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public bool IsPalindrome(ListNode head) {
        if (head == null) {
            return true;
        }
        ListNode tempNode = head;
        Stack<ListNode> sta = new Stack<ListNode>();
        while (tempNode != null) {
            sta.Push(tempNode);
            tempNode = tempNode.next;
        }
        tempNode = head;
        while (sta.Count != 0 && tempNode != null) {
            if (sta.Pop().val != tempNode.val) {
                return false;
            }
            tempNode = tempNode.next;
        }
        return sta.Count == 0;

    }
}
```

## 快慢指针+反转链表

由于进阶要求不能使用额外空间，我们的所有操作必须原地处理。

第一种方法，其实是求得一个反转的链表，并且可以只使用了这个链表的一半。

所以，考虑使用快慢指针，求得链表中心点，然后将链表分为两部分。

将右半部分反转，再进行回文判断。

例如：1-2-3-3-2-1，分为两部分1-2-3，3-2-1，反转第二部分变为1-2-3

再将这两部分判断是否回文即可。

```C#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    ListNode ReverseList(ListNode head) {
        if(head == null) {
            return head;
        }
        ListNode pre = null;
        ListNode cur = head;
        while (cur != null) {
            ListNode next = cur.next;
            cur.next = pre;
            pre = cur;
            cur = next;
        }
        return pre;
    }

    public bool IsPalindrome(ListNode head) {
        if (head == null) {
            return true;
        }
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        slow = ReverseList(slow);
        while (head != null && slow != null) {
            if (head.val != slow.val) {
                return false;
            }
            head = head.next;
            slow = slow.next;
        }
        return true;
    }
}
```

# 第9题-283. 移动零

## 两次遍历，覆盖0

考虑使用一个index来记录不是0的数的下标。

遍历数组，遇到不是0，则将值赋值给nums\[index\]，遇到是0则跳过。

最后，我们需要对末尾修改后是0的元素进行赋0，也就是从index开始进行赋值0（此时的index刚好是末尾0开始位置）

例子：1 0 2 3 0 4 变为 1 2 3 4 0 4，再变为 1 2 3 4 0 0。

```C#
public class Solution {
    public void MoveZeroes(int[] nums) {
        int index = 0;
        for (int i = 0; i < nums.Length; ++i) {
            if(nums[i] != 0) {
                nums[index++] = nums[i];
            }
        }
        for (int i = index; i < nums.Length; ++i) {
            nums[i] = 0;
        }
    }
}
```

## 优化，双指针，将不是0的数放在0的左边

我们可以应用快速排序的思想，将不是0的数放在0的左边。

使用一个left记录最近是0的下标，遍历数组，如果不是0，将**当前数**和**nums\[left\]**交换。

初始时，left = 0，因为自己和自己交换不影响结果。

比如：1 0 3 2

第一次交换swap(nums[0], nums[0])，1 0 3 2，left = 1;

第二次交换swap(nums[1], nums[2])，1 3 0 2，left = 2;

第三次交换swap(nums[2], nums[3])，1 3 2 0，left = 3;	遍历结束。

```C#
public class Solution {
    public void MoveZeroes(int[] nums) {
        int left = 0;
        for (int i = 0; i < nums.Length; ++i) {
            if (nums[i] != 0) {
                int temp = nums[i];
                nums[i] = nums[index];
                nums[left] = temp;
                ++left;
            }
        }
    }
}
```

### 进一步优化，i > left

可以看到，上述方法如果数组当中的数全都不是0，则需要每次都和当前数自己交换一次。

所以我们可以添加一个条件，只有**i > left**时才进行交换。

此时可以直接赋值了，因为nums[left] 一定是0。

```C#
public class Solution {
    public void MoveZeroes(int[] nums) {
        int left = 0;
        for (int i = 0; i < nums.Length; ++i) {
            if (nums[i] != 0) {
                if (i > left) {
                    nums[left] = nums[i];
                    nums[i] = 0;
                }
                ++left;
            }
        }
    }
}
```

# 第10题-101. 对称二叉树

## 递归

判断一棵二叉树是否轴对称，需要判断它们的结构和对应值是否相同。

判断左子节点和右子节点是否对称，可以使用第三周第4题-100.相同的树中提到的方法；

先判断是否都为空，再判断是否有空，再判断是否值相同。

和"相同的树"一样，再递归调用两次函数并且相与，判断其他节点是否对称即可。

只不过这是，由于需要判断轴对称，传入的参数应该也是对称的。

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    bool Helper(TreeNode left, TreeNode right) {
        if (left == null && right == null) {
            return true;
        }
        else if (left == null || right == null) {
            return false;
        }
        else if (left.val != right.val) {
            return false;
        }
        return Helper(left.left, right.right) && Helper(right.left, left.right);       
    }

    public bool IsSymmetric(TreeNode root) {
        if (root == null) {
            return true;
        }
        return Helper(root.left, root.right);
    }
}
```

## 队列迭代实现

我们可以使用队列，模拟上述递归操作。

我们需要比较左右子节点，那么，我们就先将左右子节点入队。

每循环一次，就将当前队头两个节点出队，对它们的结构进行判断。

还需要将两个节点的左右两个子节点也按顺序入队，以待下一次循环检查他们的结构。

注意：

这时候如果left和right都为空，我们不能直接返回true，而是跳过接下来的操作。

因为在循环中left和right，只说明当前结构正确，其他结构可能不正确。

并且left和right都为空，接下来的子节点入队等操作也就不用做了，所以直接continue。

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    public bool IsSymmetric(TreeNode root) {
        Queue<TreeNode> que = new Queue<TreeNode>();

        que.Enqueue(root.left);
        que.Enqueue(root.right);
        while (que.Count != 0) {
            TreeNode left = que.Dequeue();
            TreeNode right = que.Dequeue();

            if (left == null && right == null) {
                continue;
            }
            else if (left == null || right == null) {
                    return false;
            }
            else if (left.val != right.val) {
                return false;
            }
            que.Enqueue(left.left);
            que.Enqueue(right.right);
            que.Enqueue(right.left);
            que.Enqueue(left.right);
        }
        return true;
    }
}
```

# 第11题-268. 丢失的数字

## 哈希表

很容易想到，我们可以使用哈希表来找到丢失的数字。

将给定数组当中所有数字存储到哈希表当中，然后遍历哈希表，找出丢失的数字即可。

由于这里已经知道了一共只有n + 1个数，并且数字范围在\[0, n\]，所以我们可以直接定义一个长度为n + 1数组代替字典。

```C#
public class Solution {
    public int MissingNumber(int[] nums) {
        int[] hashTable = new int[nums.Length + 1];
        for (int i = 0; i < nums.Length; ++i) {
            hashTable[nums[i]] = 1;
        }
        for (int i = 0; i < hashTable.Length; ++i) {
            if (hashTable[i] == 0) {
                return i;
            }
        }
        return 0;
    }
}
```

## 数学

我们可以将【0，n 】中的所有数使用通项公式求和，然后将给定的数组中的所有数求和。

使用之前计算出来的总和减去数组的中数字的和即可求得丢失的这个数字。

```C#
public class Solution {
    public int MissingNumber(int[] nums) {
        int allSum = (0 + nums.Length) * (nums.Length + 1) / 2;
        int sum = 0;
        for (int i = 0; i < nums.Length; ++i) {
            sum += nums[i];
        }
        return allSum - sum;
    }
}
```

## 异或位运算

如果数据过大，使用数学方法可能导致溢出，而使用异或位运算既不使用额外空间，也不会溢出。

由于异或需要两个相同的数才能消除，所以，我们分遍历两次【0，n】

第一次，遍历并按位异或给定数组当中的数。

第二次，遍历并按位异或【0，n】，此时n = nums.Length。

这样，丢失的数字只出现了一次，而其他数字由于遍历了两次，其他数字就一定会因为异或而最终变为0。

```C#
public class Solution {
    public int MissingNumber(int[] nums) {
        int ret = 0;
        for (int i = 0; i < nums.Length; ++i) {
            ret ^= nums[i];
        }
        for (int i = 0; i <= nums.Length; ++i) {
            ret ^= i;
        }
        return ret;
    }

}
```

# 第12题-9. 回文数

## 转换成字符串

显然，我们可以直接将这个数字转换为字符串，然后使用双指针判断其是否是回文数。

```C#
public class Solution {
    public bool IsPalindrome(int x) {
        string num = x.ToString();
        int left = 0;
        int right = num.Length - 1;
        while (left < right) {
            if (num[left] != num[right]) {
                return false;
            }
            ++left;
            --right;
        }
        return true;
    }
}
```

## 反转数字的一半

我们可以反转数字的一半，将这一半数字与原来的一半数字进行比较，判断是否回文。

### 如何反转数字的一半？

每次取x的个位，添加到新的数字当中，判断其是否大于x。

记反转数字为reverseNum，使用一个while，条件为(x > reverseNum)，每次循环进行以下操作。

```C#
reverseNum = reverseNum * 10 + x % 10;
x = x / 10;
```

这样每次取x的个位，添加到新的数字当中，即可反转x的一半。

注意：

最后返回时，需要判断x == reverseNum || x == reverseNum / 10;

因为，如果 x = 121

x的长度是奇数，我们最终会得到x = 1，reverseNum = 12。

并且长度为奇数的回文数，中间数对于回文的判断没有影响，所以，最终返回x == reverseNum / 10即可。

### 特殊情况

1. 题目要求，如果x 为负数，则直接返回false。

2. 如果x末位有0但是，不是0，直接返回false。

   因为如果x末尾有0，比如，110，最终，reverseNum = 1，x = 1，返回true，不是正确答案。

# 第13题-108. 将有序数组转换为二叉搜索树

## 递归

二叉搜索树的中序遍历一定是有序的，也就是说，左子节点一定比当前节点小，右子节点一定比当前节点大。

所以，我们只需要每次选择nums[mid]作为当前节点的值，然后递归的让左节点选择左半边中间值，右节点选择右半边中间值即可。

构建时，构建的当前节点值为nums[mid]，左节点值为nums[(left + mid - 1) / 2]，右节点值为nums[(mid + 1 + right) / 2]。

由于是二分的遍历的数组，所以这样构建出来的二叉搜索树一定是高度平衡的。

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    TreeNode Dfs(int[] nums, int left, int right) {
        if (left > right) {
            return null;
        }
        int mid = (left + right) / 2;
        TreeNode root = new TreeNode(nums[mid]);
        root.left = Dfs(nums, left, mid - 1);
        root.right = Dfs(nums, mid + 1, right);
        return root;
    }

    public TreeNode SortedArrayToBST(int[] nums) {
        return Dfs(nums, 0, nums.Length - 1);
    }
}
```

## 队列模拟

显然，上述方法可以使用队列模拟。

递归函数传入参数有3个，但是nums是已知的，我们需要保存节点还有左右两个边界。

所以需要3个队列存储对应值，在模拟操作时，需要判断边界，当超出范围是，不应该再进行入队操作。

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    TreeNode Dfs(int[] nums, int left, int right) {
        if (left > right) {
            return null;
        }
        int mid = (left + right) / 2;
        TreeNode root = new TreeNode(nums[mid]);
        root.left = Dfs(nums, left, mid - 1);
        root.right = Dfs(nums, mid + 1, right);
        return root;
    }

    public TreeNode SortedArrayToBST(int[] nums) {
        Queue<TreeNode> que = new Queue<TreeNode>();
        Queue<int> leftQue = new Queue<int>();
        Queue<int> rightQue = new Queue<int>();
        int mid = (0 + nums.Length - 1) / 2;
        que.Enqueue(new TreeNode(nums[mid]));
        TreeNode ans = que.Peek();
        leftQue.Enqueue(0);
        rightQue.Enqueue(nums.Length - 1);
        while (que.Count != 0) {
            TreeNode root = que.Dequeue();
            int left = leftQue.Dequeue();
            int right = rightQue.Dequeue();
            mid = (left + right) / 2;
            root.val = nums[mid];
            if (left <= mid - 1) {
                root.left = new TreeNode();
                que.Enqueue(root.left);
                leftQue.Enqueue(left);
                rightQue.Enqueue(mid - 1);
            }
            if (right >= mid + 1) {
                root.right = new TreeNode();
                que.Enqueue(root.right);
                leftQue.Enqueue(mid + 1);
                rightQue.Enqueue(right);
            }
        }
        return ans;
    }
```

# ----------------------------------

# 第四周

# 第1题-190. 颠倒二进制位

## 暴力

很容易想到，我们可以计算出n的最低位，然后将其左移32 - i - 1位。

这样，就颠倒了n的最低位，依次循环，直到n == 0即可。

```C#
public class Solution {
    public uint reverseBits(uint n) {
        uint ret = 0;
        for (int i = 0; i < 32 && n > 0; ++i) {
            ret |= (n & 1) << (31 - i);
            n >>= 1;
        }
        return ret;
    }
}
```

## 分治位运算

> 笑死，根本想不到，我是废物
>
> [190. 颠倒二进制位 - 力扣（Leetcode）](https://leetcode.cn/problems/reverse-bits/solutions/685436/dian-dao-er-jin-zhi-wei-by-leetcode-solu-yhxz/)

这个是源码级的算法。

```C#
public class Solution {
    private static uint M1 = 0x55555555; // 01010101010101010101010101010101
    private static uint M2 = 0x33333333; // 00110011001100110011001100110011
    private static uint M4 = 0x0f0f0f0f; // 00001111000011110000111100001111
    private static uint M8 = 0x00ff00ff; // 00000000111111110000000011111111

    public uint reverseBits(uint n) {
        n = n >> 1 & M1 | (n & M1) << 1;
        n = n >> 2 & M2 | (n & M2) << 2;
        n = n >> 4 & M4 | (n & M4) << 4;
        n = n >> 8 & M8 | (n & M8) << 8;
        return n >> 16 | n << 16;
    }
}
```

# 第2题-572. 另一棵树的子树

[572. 另一棵树的子树 - 力扣（Leetcode）](https://leetcode.cn/problems/subtree-of-another-tree/)

## 暴力DFS

寻找子树，那么，我们就假设每一个节点都是这颗子树，判断以这个节点为根节点的子树是否和给定的树一样。

如果是返回true，不是就继续**递归判断左节点和右节点**。

检查两颗数是否相同，之前的题目当中已经出现过了。

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    bool CheckSame(TreeNode root, TreeNode subRoot) {
        if (root == null && subRoot == null) {
            return true;
        }
        else if (root == null || subRoot == null) {
            return false;
        }
        else if (root.val != subRoot.val) {
            return false;
        }
        return CheckSame(root.left, subRoot.left) && CheckSame(root.right, subRoot.right);
    }

    bool Dfs(TreeNode root, TreeNode subRoot) {
        if (root == null) {
            return false;
        }
        return CheckSame(root, subRoot) || Dfs(root.left, subRoot) || Dfs(root.right, subRoot);
    }

    public bool IsSubtree(TreeNode root, TreeNode subRoot) {
        return Dfs(root, subRoot);
    }
}
```

## 官方解法二-KMP

## 官方解法三-树哈希

> 捏妈！
>
> [572. 另一棵树的子树 - 力扣（Leetcode）](https://leetcode.cn/problems/subtree-of-another-tree/solutions/233896/ling-yi-ge-shu-de-zi-shu-by-leetcode-solution/)

# 第3题-2124. 检查是否所有 A 都在 B 之前

[2124. 检查是否所有 A 都在 B 之前 - 力扣（Leetcode）](https://leetcode.cn/problems/check-if-all-as-appears-before-all-bs/)

## 暴力

我们遍历字符串，遇到a，就检查a前面有没有b，如果有，返回false。

```C#
public class Solution {
    public bool CheckString(string s) {
        int lastA = -1;
        int firB = s.Length;
        for (int i = 0; i < s.Length; ++i) {
            if (s[i] != 'a') {
                continue;
            }
            for (int j = i - 1; j >= 0; --j) {
                if (s[j] == 'b'){
                    return false;
                }
            }
        }
        return true;
    }
}
```

## 最后一个a的位置与第一个b的位置比较

如果有b在a前面的情况，则**第一个b**的位置，一定在**最后一个a**的位置之前。

我们可以利用这点，找到最后一个a的位置与第一个b的位置，比较并返回即可。

这里值得注意的是，lastA需要初始化为-1，firB需要初始化为s.Length。

为了应对只有a或者只有b的特殊情况。

```C#
public class Solution {
    public bool CheckString(string s) {
        int lastA = -1;
        int firB = s.Length;
        for (int i = 0; i < s.Length; ++i) {
            if (s[i] == 'a') {
                lastA = i;
            }
            else if (i < firB) {
                firB = i;
            }
        }
        return lastA < firB;
    }
}
```

## 直接查找"ba"的位置

由于如果b在a前面，则一定有子字符串"ba"出现，所以，我们可以直接返回字符串是否包含"ba"。

```C#
public class Solution {
    public bool CheckString(string s) {
        return !s.Contains("ba");
    }
}
```

# 第4题-53. 最大子数组和

> 从这题开始，就全是中等题和困难题啦

## 暴力

要找出一个最大的连续子数组和，首先，我们需要确定这个子数组的左边界和右边界。

我们可以使用双for暴力的查找这个区间，显然，这会超时。

```C#
public class Solution {
    public int MaxSubArray(int[] nums) {
        int ans = int.MinValue;
        for (int i = 0; i < nums.Length; ++i) {
            int curSum = 0;
            for (int j = i; j < nums.Length; ++j) {
                curSum += nums[j];
                ans = Math.Max(curSum, ans);
            }
        }
        return ans;
    }
}
```

## 动态规划

在暴力的解法当中，主要耗时在计算区间和。

那么，我们就需要想办法使得之前计算过的区间和得以利用。

我们可以发现，每一个前缀和就是一个区间和，并且在计算下一个前缀和时，只需要**加上当前数**。

但是，前缀和不一定是最大的子数组，所以，我们需要确定：以当前数字结尾的子数组，是否是最大子数组。

所以dp[i]：**以nums[i]结尾的最大子数组和**。

那么，dp[i] = max(dp[i - 1] + nums[i], nums[i]);

因为，如果所有数字都是正数，那么dp[i] = dp[i - 1] + nums[i]；

但是数组当中有负数，所以，之前的计算和不一定大于当前数字，需要和当前数比较。

其实，这就是重新确定了左边界，而当前数就是右边界。

所以，以nums[i]结尾的最大子数组和，一定是以nums[i - 1]结尾的子数组和 + 当前数。

而如果加上当前数不大于当前数，说明之前的计算结果都无效，需要抛弃。

初始时，dp[0]需要=nums[0]，因为一个数的时候，自己就是以自己结尾的区间和。

注意：我们不能在最后直接返回dp[n - 1]，因为dp[i]是以nums[i]结尾的最大子数组和，不是整个数组的最大子数组和。

所以需要一个ans，记录最大的子数组和，每次计算一次dp[i]，就更新一次答案。

```C#
public class Solution {
    public int MaxSubArray(int[] nums) {
        int[] dp = new int[nums.Length];
        dp[0] = nums[0];
        int ans = nums[0];
        for (int i = 1; i < nums.Length; ++i) {
            dp[i] = Math.Max(dp[i - 1] + nums[i], nums[i]);
            ans = Math.Max(dp[i], ans);
        }
        return ans;
    }
}
```

## 动态规划空间优化

我们可以注意到，dp[i]至于dp[i - 1]和nums[i]有关；

所以，我们可以利用一个标记curSum作为滚动变量，记录dp[i]。

而抛弃dp[i - 1]的时机，其实是dp[i - 1] < 0。

因为这个区间和如果小于0，是负数，加上当前数也不会变大了，当前数可能反而更大一些，所以当curSum < 0 时，需要重置curSum为0。

```C#
public class Solution {
    public int MaxSubArray(int[] nums) {
        int curSum = 0;
        int ans = int.MinValue;
        for (int i = 0; i < nums.Length; ++i) {
            if (curSum < 0) {
                curSum = 0;
            }
            curSum += nums[i];
            ans = Math.Max(curSum, ans);            
        }
        return ans;
    }
}
```

# 第5题-57. 插入区间

有区间一\[left, right\]，区间二\[s1, r1\]。

如果两个区间没有交集，则区间一一定在区间二的左边或者右边。

即right < s1或者r1 < left。

如果有交集，则直接合并区间，这个区间的左右边界为

left = Min(s1, left)；right = Max(s2, right)

我们可以设置一个是否插入的标记inserted，当插入区间在当前区间的左边并且还没有插入，则先把插入区间添加到答案，再添加当前区间，并将插入标记置为真；

当插入区间在当前区间的右边，则直接将当前区间添加到答案。

如果两个情况不满足，说明两者有交集，则根据上述式子更新左右边界。

如果遍历完成之后还没有插入，说明插入区间在最后，直接添加到答案的最后。

```C#
public class Solution {
    public int[][] Insert(int[][] intervals, int[] newInterval) {
        List<List<int>> ret = new List<List<int>>();
        int left = newInterval[0];
        int right = newInterval[1];
        bool inserted = false;
        foreach (var item in intervals) {
            if (right < item[0]) {
                if (!inserted) {
                    ret.Add(new List<int>() {left, right});
                    inserted = true;
                }
                ret.Add(new List<int>(item));
            }
            else if (item[1] < left) {
                ret.Add(new List<int>(item));
            }
            else {
                left = Math.Min(item[0], left);
                right = Math.Max(item[1], right);
            }
        }
        if (!inserted) {
            ret.Add(new List<int>() {left, right});
        }
        int[][] ans = new int[ret.Count][];
        for (int i = 0; i < ret.Count; ++i) {
            ans[i] = new int[2]{ret[i][0], ret[i][1]};
        }
        return ans;
    }
}
```

# 第6题-542. 01 矩阵

[542. 01 矩阵 - 力扣（Leetcode）](https://leetcode.cn/problems/01-matrix/description/)

## 多源BFS

给定一个只有0和1的矩阵，要求输出一个新的矩阵，新的矩阵当中，每个格子上的值为当前格子到最近的0的值。

普通的树BFS是单源的遍历，所以不需要对节点进行访问记录。

而题目当中给定的0是可能有多个的，所以，我们需要先将所有0的位置入队，其他元素置为-1作为访问标记。

然后BFS，遍历队列当中每一个元素的上下左右四个位置，如果此位置为-1，那么说明其不是0且未访问。

那么，它和最近的0的距离就是当前元素的值 + 1，`mat[x][y] + 1`；并且还需要将其入队，以供迭代的计算下一层的数值使用。

比如，当前位置是0，它的上下左右四个位置的值只要未访问且不是0，就应该为1，即：`mat[x][y] + 1`。

当前位置是1，它的上下左右四个位置的值只要未访问且不是0，就应该为2，即：`mat[x][y] + 1`。

下面的写法当中是直接使用原矩阵即mat，来标记是否访问。

如果需要不修改原矩阵，则需要定义另外两个矩阵visited和dist，分别记录当前点是否访问，当前点的答案。

```C#
public class Solution {
    public int[][] UpdateMatrix(int[][] mat) {
        Queue<int[]> que = new Queue<int[]>();
        int n = mat.Length;
        int m = mat[0].Length;
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                if (mat[i][j] == 0) {
                    que.Enqueue(new int[]{i, j});
                }
                else {
                    mat[i][j] = -1;
                }
            }
        }
        int[] dx = new int[] {0, 0, 1, -1};
        int[] dy = new int[] {1, -1, 0, 0};
        while (que.Count != 0) {
            int[] point = que.Dequeue();
            int x = point[0];
            int y = point[1];
            for (int i = 0; i < 4; ++i){
                int nx = x + dx[i];
                int ny = y + dy[i];
                if (nx >= 0 && nx < n && ny >= 0 && ny < m && mat[nx][ny] == -1) {
                    que.Enqueue(new int[] {nx, ny});
                    mat[nx][ny] = mat[x][y] + 1;
                }
            }
        }
        return mat;
    }
}
```

# 第7题-973. 最接近原点的 K 个点

## 按与原点的距离排序

因为要求与原点最近的K个点，那么，我们直接根据与原点的距离进行升序排序，再取前K点即可。

```C#
public class Solution {
    public int[][] KClosest(int[][] points, int k) {
        List<int[]> list = new List<int[]>();
        for (int i = 0; i < points.GetLength(0); ++i) {
            list.Add(points[i]);
        }
        list.Sort((a, b) => {
            double disA = Math.Sqrt((a[0] * a[0]) + (a[1] * a[1]));
            double disB = Math.Sqrt((b[1] * b[1]) + (b[0] * b[0]));
            return disA < disB ? -1 : 1;
        });
        int[][] ret = new int[k][];
        for (int i = 0; i < k; ++i) {
            ret[i] = list[i];
        }
        return ret;
    }
}
```

## 快速选择

> 寄
>
> [973. 最接近原点的 K 个点 - 力扣（Leetcode）](https://leetcode.cn/problems/k-closest-points-to-origin/solutions/477916/zui-jie-jin-yuan-dian-de-k-ge-dian-by-leetcode-sol/)

# 第8题-3. 无重复字符的最长子串

[3. 无重复字符的最长子串 - 力扣（Leetcode）](https://leetcode.cn/problems/longest-substring-without-repeating-characters/description/)

## 滑动窗口+哈希表

由于需要求的是连续的无重复的最长子串，那么，我们可以维护一个无重复的滑动窗口；

从0开始遍历字符串，left表示左边界，right表示右边界，初始时right需要等于-1。

使用哈希表，每一次将左边界值擦除，然后一直添加元素，直到有重复元素出现。

添加完成之后，更新答案。

```C#
public class Solution {
    public int LengthOfLongestSubstring(string s) {
        HashSet<char> hashSet = new HashSet<char>();
        int ans = 0;
        int right = -1;
        int n = s.Length;
        for (int left = 0; left < s.Length; ++left) {
            if (left != 0) {
                hashSet.Remove(s[left - 1]);
            }
            while (right + 1 < n && !hashSet.Contains(s[right + 1])) {
                hashSet.Add(s[right + 1]);
                ++right;
            }
            ans = Math.Max(right - left + 1, ans);
        }
        return ans;
    }
}
```

# 第9题-15. 三数之和

[15. 三数之和 - 力扣（Leetcode）](https://leetcode.cn/problems/3sum/?utm_source=LCUS&utm_medium=ip_redirect&utm_campaign=transfer2china)

## 排序+哈希表

根据题意，要求从一组数值当中，找到三个数的和为0，还需要返回所有的组合，并且不能重复组合，不能使用重复元素。

那么，为了去重，我们需要先将数组排序，在选数的时候，就可以直接判断前两个数是否相同，相同则不用继续；不同则选数。

首先，第一层循环从0开始遍历，选择第一个数，判断前一个元素是否相同，不相同，选择第二三个数。

第二层循环从i + 1开始查找，为了得到答案，我们需要使用一个哈希表，存储第二层当中已经遍历过的数（每次都需要重新声明一个新的哈希表，因为是重新选数）。

第二层循环当中，首先去重。然后计算c = 0 - num[i] - nums[j]，得到第三个数。判断这个数c是否存在于哈希表当中，存在则说明有一个答案，保存答案并且去除c（因为c已经使用过了）。

否则添加num[j]到哈希表当中，作为备选元素。

这样，每次使用num[i]作为第一个数，使用nums[j]作为第二个数，使用c作为第三个数。

在使用第三个数c时，将其从备选数当中去除，由于数组已经排序，哈希表不存储多个相同元素，就不会得出重复的答案。

```C#
public class Solution {
    public IList<IList<int>> ThreeSum(int[] nums) {
        IList<IList<int>> ret = new List<IList<int>>();
        Array.Sort(nums);
        int n = nums.Length;
        for (int i = 0; i < n; ++i) {
            if (nums[i] > 0) break;
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            HashSet<int> hashSet = new HashSet<int>();        
            for (int j = i + 1; j < n; ++j) {
                if (j > i + 2 && nums[j] == nums[j - 1] && nums[j] == nums[j - 2]) {
                    continue;
                }
                int c = 0 - nums[j] - nums[i];
                if (hashSet.Contains(c)) {
                    ret.Add(new List<int>(){c, nums[i], nums[j]});
                    hashSet.Remove(c);
                }
                else {
                    hashSet.Add(nums[j]);
                }
            }
        }
        return ret;
    }
}
```

## 排序+二分查找

我们可以优化上述方法当中的内层循环。

因为数组已经有序，那么，我们可以直接从右向左查找第三个数。

首先外层循环和上面的方法一样，如果大于0或者相等，我们需要中断和跳出循环。

然后，使用third变量 = n - 1，表示从右边界开始查找；target = 0 - nums[fir]，表示内层循环需要查找的值，然后开始第二层循环。

由于第三个数在右边界，所以，我们只需要判断nums[sec] 和 nums[sec - 1]是否相同并跳出一次循环。

然后，我们需要查找第三个数，也就是如果nums[sec] + nums[third] > target，我们就需要--third，以得到一个符合目标的数。

while完成后，我们需要判断sec == third，因为如果sec == third，说明已经不可能再出现答案了。

所有的num[sec] + num[third]都比target大，那么后面的sec也不可能比target小，所以需要直接中断循环。

然后判断nums[sec] + nums[third]是否等于target，等于说明有一组答案。

以此循环，得到最终的答案列表。

> 这里的优化，主要是把第三个数的查找，从使用哈希表到使用二分查找。
>
> 之前使用哈希表，无论是否还可能有答案，都会遍历完二层循环，这样则不会。
>
> 并且没有了哈希表remove和add的开销。

```C#
public class Solution {
    public IList<IList<int>> ThreeSum(int[] nums) {
        IList<IList<int>> ret = new List<IList<int>>();
        Array.Sort(nums);
        int n = nums.Length;
        for (int fir = 0; fir < n; ++fir) {
            if (nums[fir] > 0) break;
            if (fir > 0 && nums[fir] == nums[fir - 1]) continue;
            int third = n - 1;
            int target = 0 - nums[fir];
            for (int sec = fir + 1; sec < n; ++sec) {
                if (sec > fir + 1 && nums[sec] == nums[sec - 1]) {
                    continue;
                }
                while (sec < third && nums[sec] + nums[third] > target) --third;
                if (sec == third) break;
                if (nums[sec] + nums[third] == target) {
                    List<int> temp = new List<int>(){nums[fir], nums[sec], nums[third]};
                    ret.Add(temp);
                }
            }
        }
        return ret;
    }
}
```

# 第10题-102. 二叉树的层序遍历

显然，这题可以直接使用队列实现。

初始时，如果root不为空，将其添加到队列。

然后遍历队列，每次都先记录一下队列长度，也就是二叉树这一层元素的个数，因为遍历节点的时候会添加下一层节点，队列的长度会改变。

然后将这一层的所有元素出队，记录到答案当中，中途遇某这个节点有左右两个子节点，就将他们添加到队列当中。

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    public IList<IList<int>> LevelOrder(TreeNode root) {
        Queue<TreeNode> que = new Queue<TreeNode>();
        if (root != null) que.Enqueue(root);
        IList<IList<int>> ret = new List<IList<int>>();
        while (que.Count != 0) {
            TreeNode curNode;
            int len = que.Count;
            List<int> tempList = new List<int>();
            for (int i = 0; i < len; ++i) {
                curNode = que.Dequeue();
                tempList.Add(curNode.val);
                if (curNode.left != null) que.Enqueue(curNode.left);
                if (curNode.right != null) que.Enqueue(curNode.right);
            }
            ret.Add(tempList);
        }
        return ret;
    }
}
```

# -----------------------------------

# 第5周

# 第1题-133. 克隆图

## 深度优先搜索DFS

要获取一个图的克隆，我们需要完全克隆图的结构和节点值。

由于是一个无向图，两个相连的节点存在互相的邻接点，为了防止重复访问邻接点导致的死循环，我们需要使用一个哈希表，记录已经访问过得节点。

为了方便的记录，我们直接以原图的节点为键，新图对应节点为值。

当遇到已经访问过的节点时，直接返回新图对应节点。

未访问过则创建一个新的节点，将原图节点和新节点添加到哈希表当中。

然后遍历邻接点，遍历邻接点时，递归调用函数，以访问其他节点。

最后返回本节点即可。

> 注意：当遇到一个未访问过的节点时，应当立刻将原图节点和新图节点放入哈希表，以防递归时重复访问，造成死循环。

```C#
/*
// Definition for a Node.
public class Node {
    public int val;
    public IList<Node> neighbors;

    public Node() {
        val = 0;
        neighbors = new List<Node>();
    }

    public Node(int _val) {
        val = _val;
        neighbors = new List<Node>();
    }

    public Node(int _val, List<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
}
*/

public class Solution {
    Dictionary<Node, Node> hash = new Dictionary<Node, Node>();

    public Node CloneGraph(Node node) {
        if (node == null) return null;
        if (hash.ContainsKey(node)) {
            return hash[node];
        }
        Node newNode = new Node(node.val);
        hash.Add(node, newNode);
        for (int i = 0; i < node.neighbors.Count; ++i) {
            newNode.neighbors.Add(CloneGraph(node.neighbors[i]));
        }
        return newNode;
    }
}
```

## 广度优先搜索BFS

显然，我们可以使用队列来模拟上述递归操作。

初始时，将第一个节点入队，并将第一个节点和新图节点添加到哈希表。

然后遍历队列，每次出队队头元素，遍历邻接点，如果邻接点未访问过，添加原图节点和创建新图节点到哈希表，并添加到队列；

然后通过哈希表添加新图当前节点的邻接点。

> 注意：遍历过程当中，我们使用哈希表来访问新图节点

```C#
public class Solution {
    public Node CloneGraph(Node node) {
        if (node == null) return null;
        Dictionary<Node, Node> hash = new Dictionary<Node, Node>();
        Queue<Node> que = new Queue<Node>();
        que.Enqueue(node);
        hash.Add(node, new Node(node.val));
        while (que.Count != 0) {
            Node curNode = que.Dequeue();
            foreach (var neighbor in curNode.neighbors) {
                if (!hash.ContainsKey(neighbor)) {
                    hash.Add(neighbor, new Node(neighbor.val));
                    que.Enqueue(neighbor);
                }
                hash[curNode].neighbors.Add(hash[neighbor]);
            }
        }
        return hash[node];
    }
}
```

# 第2题-150. 逆波兰表达式求值

## 栈模拟

这是一道经典的栈模拟题。

由于逆波兰表达式的性质，一个符号的出现之前，必定有两个数出现。

所以，我们只需要在数字出现时，先将数压入栈当中。

遇到符号时，由于栈性质，先取出右操作数，再取出左操作数，计算结果，并且再将结果压入栈中。

如果表达式正确，最终的栈顶元素就是表达式的值。

```C#
public class Solution {
    public int EvalRPN(string[] tokens) {
        Stack<int> nums = new Stack<int>();
        Stack<char> symbols = new Stack<char>();
        for (int i = 0; i < tokens.Length; ++i) {
            if (tokens[i] == "+" || tokens[i] == "-" || tokens[i] == "*" || tokens[i] == "/") {
                int b = nums.Pop();
                int a = nums.Pop();
                int c = 0;
                if (tokens[i] == "+") c = a + b;
                if (tokens[i] == "-") c = a - b;
                if (tokens[i] == "*") c = a * b;
                if (tokens[i] == "/") c = a / b;
                nums.Push(c);
            }
            else {
                nums.Push(int.Parse(tokens[i]));
            }
        }
        return nums.Pop();
    }
}
```

# 第3题-207. 课程表

## Dfs+拓扑排序

首先，学一门课要先修另一门课，我们可以将其看作一张图，就是一个结点有从另一个结点的一条路径。

我们可以使用邻接表存储图中点的关系。

再看题目，根据题意，先修A，再修B；如果有先修A再修B && 先修B再修A，则这是不可能的。

如果整个课程表当中不存在第二种情况，返回true，否则返回false。

注意，这个先修链可能不只一级。

比如，有A->B，B->C，C->D，又有D->A，这也是不可能的。

所以，问题就变为了，给定图，让求得是否存在一个有向无环图。

我们可以使用拓扑排序解决这个问题。

Dfs+拓扑排序：

首先，确定邻接表，然后编程所有课程，如果没有被访问过，就Dfs。

我们设定，一个节点在Dfs途中有三种状态：

- 0，未搜索过
- 1，正在被其他节点搜索
- 2，搜索完毕

如果当前节点未搜索过，我们需要搜索它，遍历它的所有邻接节点。

如果当前节点正在被其他节点搜索，说明图中存在环，将答案设定为false，直接返回。

如果搜索完毕，没啥需要做的。

注意：一进入搜索，就置当前节点状态为正在被其他节点搜索

```C#
public class Solution {
    List<List<int>> edges = new List<List<int>>();
    List<int> visited = new List<int>();
    bool ret = true;

    void dfs(int u) {
        visited[u] = 1;
        foreach (var v in edges[u]) {
            if (visited[v] == 0) {
                dfs(v);
                if (!ret) {
                    return;
                }
            }
            else if (visited[v] == 1) {
                ret = false;
                return;
            }
        }
        visited[u] = 2;
    }

    public bool CanFinish(int numCourses, int[][] prerequisites) {
        for (int i = 0; i < numCourses; ++i) {
            edges.Add(new List<int>());
            visited.Add(0);
        }
        
        foreach (var item in prerequisites) {
            edges[item[1]].Add(item[0]);
        }
        
        for(int i = 0; i < numCourses && ret; ++i) {
            if (visited[i] == 0) {
                dfs(i);
            }
        }
        return ret;
        
    }
}
```

## Bfs + 拓扑排序

Dfs是在通过遍历当前节点的所有邻接节点，求得拓扑排序，并查看是否存在环。

我们也可以使用Bfs正向的构建拓扑排序。

拓扑排序就是将入度为0的节点添加到答案当中，并将该节点的所有邻接节点入度-1。

所以，我们先求得所有节点的入度，并将所有入度为0的节点添加到队列当中，然后使用广度优先搜索搜索这些节点。

搜索过程当中，我们需要将该节点的所有邻接节点的入度减一。

并且，将入度为0的节点添加到队列当中。

由于每一次出队操作，就是学完一门课；

那么如果执行出队操作的次数等于CourseNum，说明存在一个拓扑序列使得可以学完整个课程。

```C#
public class Solution {
    public List<List<int>> edges = new List<List<int>>();
    public List<int> indeg = new List<int>();

    public bool CanFinish(int numCourses, int[][] prerequisites) {
        for (int i = 0; i < numCourses; ++i) {
            edges.Add(new List<int>());
            indeg.Add(0);
        }

        for (int i = 0; i < prerequisites.Length; ++i) {
            edges[prerequisites[i][1]].Add(prerequisites[i][0]);
            indeg[prerequisites[i][0]]++;
        }

        Queue<int> que = new Queue<int>();
        for (int i = 0; i < numCourses; ++i) {
            if (indeg[i] == 0) {
                que.Enqueue(i);
            }
        }
        int visited = 0;
        while(que.Count != 0) {
            ++visited;
            int u = que.Dequeue();
            foreach (var v in edges[u]) {
                indeg[v]--;
                if (indeg[v] == 0) {
                    que.Enqueue(v);
                }
            }
        }
        return visited == numCourses;
    }
}
```

# 第4题-208. 实现 Trie (前缀树)

[208. 实现 Trie (前缀树) - 力扣（Leetcode）](https://leetcode.cn/problems/implement-trie-prefix-tree/description/)

## 数组实现

使用一个26长度的Trie数组，存储子节点，还需要使用一个isEnd标记，标记是否是一个单词的结尾。

插入：初始时当前节点为this

- 如果没有当前字符，新建一个节点，移动到新节点
- 如果有当前字符，移动到对应字符节点
- 遍历完字符串后，将当前节点的isEnd修改为true，因为这是一个单词

搜索单词：

- 如果没有当前字符，直接返回null
- 如果有当前字符，移动到对应字符节点
- 当遍历完字符，判断当前节点的isEnd是否为true，true返回true，false返回false

搜索前缀：

- 如果没有当前字符，直接返回null
- 如果有当前字符，移动到对应字符节点
- 当遍历完字符，返回true

我们发现，搜索单词和搜索前缀的前两步是一致的，所以，我们可以将其合并为一个函数，返回一个节点。

搜索单词时，调用此函数，判断返回的节点是否为空并且isEnd是否为true即可；

搜索前缀是，调用此函数，判断返回的节点是否为空即可。

```C#
public class Trie {
    List<Trie> children = new List<Trie>();
    bool isEnd = false;

    public Trie() {
        for(int i = 0; i < 26; ++i) {
            children.Add(null);
        }
    }
    
    public void Insert(string word) {
        Trie node = this;
        for (int i = 0; i < word.Length; ++i) {
            int index = word[i] - 'a';
            if (node.children[index] == null) {
                node.children[index] = new Trie();
            }
            node = node.children[index];
        }
        node.isEnd = true;
    }
    
    public bool Search(string word) {
        Trie node = SearchPrefix(word);
        return node != null && node.isEnd == true;
    }   

    public bool StartsWith(string prefix) {
        Trie node = SearchPrefix(prefix);
        return node != null; 
    }

    public Trie SearchPrefix(string word) {
        Trie node = this;
        for (int i = 0; i < word.Length; ++i) {
            int index = word[i] - 'a';
            if (node.children[index] == null) {
                return null;
            }
            node = node.children[index];
        }
        return node;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.Insert(word);
 * bool param_2 = obj.Search(word);
 * bool param_3 = obj.StartsWith(prefix);
 */
```

## 哈希表优化

显然，我们可以不使用数组实现子节点的对应关系。

我们可以直接使用字典（哈希表）实现

只需要在遍历字符时，判断是否拥有此字符对应的节点即可。

```C#
public class Trie {
    Dictionary<char, Trie> children = new Dictionary<char, Trie>();
    bool isEnd = false;

    public Trie() {
        
    }
    
    public void Insert(string word) {
        Trie node = this;
        for (int i = 0; i < word.Length; ++i) {
            if (!node.children.ContainsKey(word[i])) {
                node.children.Add(word[i], new Trie());
            }
            node = node.children[word[i]];
        }
        node.isEnd = true;
    }
    
    public bool Search(string word) {
        Trie node = SearchPrefix(word);
        return node != null && node.isEnd == true;
    }   

    public bool StartsWith(string prefix) {
        Trie node = SearchPrefix(prefix);
        return node != null; 
    }

    public Trie SearchPrefix(string word) {
        Trie node = this;
        for (int i = 0; i < word.Length; ++i) {
            if (!node.children.ContainsKey(word[i])) {
                return null;
            }
            node = node.children[word[i]];
        }
        return node;
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.Insert(word);
 * bool param_2 = obj.Search(word);
 * bool param_3 = obj.StartsWith(prefix);
 */
```

# 第5题-322. 零钱兑换

## 动态规划

每一个硬币是可以使用无数次的，所以可以看作是完全背包问题。

1. dp\[j\]：金额j最少需要多少枚硬币

2. 确定递推公式

   1. `dp[j]`表示金额 j 最少需要多少枚硬币，那么金额`j - coins[i]`最少需要`dp[j - coins[i]`，那么金额 j 需要`dp[j - coins[i] + 1`。

   2. 由于可能存在无法兑换的情况，比如`amount = 2`，`coins[0] = 3`判断`dp[j - coins[i]`其是否可以存储，然后，和当前`dp[j]`比较，选择最小的即可。

   3. ```C#
      dp[j] = min(dp[j - coins[i]] + 1, dp[j]);
      ```

3. dp数组如何初始化

   1. 0 金额一定只需要 0 个硬币。
   2. 其他金额需要计算，比较取较小的，所以初始化为一个`int.MaxValue`。

4. 确定遍历顺序

   1. 由于只是求硬币的最小数量，所以无需关心遍历顺序。
   2. 所以可以外层遍历硬币种类，内层遍历金额。
   3. 由于硬币可以无限使用，是完全背包，所以内层从当前最小值即`coins[i]`开始。

```C#
public class Solution {
    public int CoinChange(int[] coins, int amount) {
        int[] dp = new int[amount + 1];
        for (int i = 1; i <= amount; ++i) {
            dp[i] = int.MaxValue;
        }
        dp[0] = 0;
        for (int i = 0; i < coins.Length; ++i) {
            for (int j = coins[i]; j <= amount; ++j) {
                if (dp[j - coins[i]] != int.MaxValue) {
                    dp[j] = Math.Min(dp[j - coins[i]] + 1, dp[j]);
                }
            }
        }
        if (dp[amount] == int.MaxValue) {
            return -1;
        }
        return dp[amount];
    }
}

```

# 第6题-238. 除自身以外数组的乘积

## 哈希表

由于答案数组的每一个元素是由除`nums[i]`之外的所有数的乘积构成的。

那么，我们可以计算一个前缀乘积，并使用哈希表记录0的位置。

计算前缀乘积时，遇到0记录下来，不参与计算。

然后，再遍历一次计算答案。

- 如果只有一个0，那么只需要将那个位置的`ans[i] = prefix` 。
- 如果有多个0，那么全部都是0。
- 如果没有0，那么`ans[i] = prefix / nums[i]` 。

```C#
public class Solution {
    public int[] ProductExceptSelf(int[] nums) {
        int prefix = nums[0];
        int n = nums.Length;
        HashSet<int> hash = new HashSet<int>();
        if (prefix == 0) {
            hash.Add(0);
            prefix = 1;
        }
        for (int i = 1; i < n; ++i) {
            if (nums[i] == 0) {
                hash.Add(i);
            }
            else {
                prefix *= nums[i];
            }
        }
        int[] ans = new int[n];
        for (int i = 0; i < n; ++i) {
            if (hash.Contains(i) && hash.Count == 1) {
                ans[i] = prefix;
            }
            else if (hash.Count != 0) {
                ans[i] = 0;
            }
            else {
                ans[i] = prefix / nums[i];
            }
        }
        return ans;
    }
}
```

## 记录0的个数（O（1）的额外空间）

由于答案数组的每一个元素是由除`nums[i]`之外的所有数的乘积构成的。

那么：

- 如果只有一个0，只需要这个0的位置`ans[i] = prefix`
- 如果有多个0，那么所有`ans[i]`都是0
- 如果没有0，那么所有`ans[i] = prefix / nums[i]`

所以，我们只需要记录一次0的个数，不用将每一个0的位置都记录下来。

```C#
public class Solution {
    public int[] ProductExceptSelf(int[] nums) {
        int prefix = nums[0];
        int n = nums.Length;
        int zeroCount = 0;
        int zeroIndex = -1;
        if (prefix == 0) {
            ++zeroCount;
            zeroIndex = 0;
            prefix = 1;
        }
        for (int i = 1; i < n; ++i) {
            if (nums[i] == 0) {
                ++zeroCount;
                zeroIndex = i;
                if (zeroCount > 1) {
                    break;
                }
            }
            else {
                prefix *= nums[i];
            }
        }
        int[] ans = new int[n];
        if (zeroCount == 1) {
            for (int i = 0; i < n; ++i) {
                if (i != zeroIndex) {
                    ans[i] = 0;
                }
                else {
                    ans[i] = prefix;
                }
            }
        }
        else if (zeroCount > 1) {
            for (int i = 0; i < n; ++i) {
                ans[i] = 0;
            }
        }
        else {
            for (int i = 0; i < n; ++i) {
                ans[i] = prefix / nums[i];
            }
        }
        return ans;
    }
}
```

## 不使用除法

麻了，没看清楚题目，题目不允许使用除法！

不使用除法，那么就使用乘法。

我们构建一个不包括本身的前缀乘积数组和一个不包括本身的后缀乘积数组。

显然`prefix[0] = 1` ，`suffix[n - 1] = 1`。

因为0号元素的前面没有元素，n - 1号元素的后面没有元素。

对于其他元素：

`prefix[i] = prefix[i - 1] * nums[i - 1]`

`suffix[i] = suffix[i + 1] * nums[i + 1]`

那么，`ans[i] = prefix[i] * suffix[i]`。

```C#
public class Solution {
    public int[] ProductExceptSelf(int[] nums) {
        int n = nums.Length;
        int[] prefix = new int[n];
        int[] suffix = new int[n];
        int[] ans = new int[n];
        prefix[0] = 1;
        suffix[n - 1] = 1;
        for (int i = 1; i < n; ++i) {
            prefix[i] = prefix[i - 1] * nums[i - 1];
            suffix[n - i - 1] = suffix[n - i] * nums[n - i];
        }
        for (int i = 0; i < n; ++i) {
            ans[i] = prefix[i] * suffix[i];
        }
        return ans;
    }
}
```

# 第7题-155. 最小栈

## 两个栈，记录每一个元素的最小元素

使用两个栈，一个栈记录正常的推入元素，另一个栈记录“当前元素的最小元素”。

也就是说，minSta记录推入每一个元素的那个时刻，最小元素是谁。

由于推入第一个元素时就需要判断最小元素，所以，我们给minSta初始化一个int.MaxValue，用于第一个元素的判断。

```C#
public class MinStack {
    private int minNum = int.MaxValue;
    private Stack<int> sta = new Stack<int>();
    private Stack<int> minSta = new Stack<int>();

    public MinStack() {
        minSta.Push(int.MaxValue);
    }
    
    public void Push(int val) {
        sta.Push(val);
        if (minSta.Peek() > val) {
            minSta.Push(val);
        }
        else {
            minSta.Push(minSta.Peek());
        }
    }
    
    public void Pop() {
        sta.Pop();
        minSta.Pop();
    }
    
    public int Top() {
        return sta.Peek();
    }
    
    public int GetMin() {   
        return minSta.Peek();
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.Push(val);
 * obj.Pop();
 * int param_3 = obj.Top();
 * int param_4 = obj.GetMin();
 */
```

## 不使用辅助栈，记录差值

我们可以不使用辅助栈，用一个栈记录每一个元素和当前最小元素的差值。

- Push
  - 如果栈空，push一个0，minNum = val
  - 如果栈不空，计算val和minNum的差值
    - 如果差值 > 0，说明val > minNum，直接推入差值
    - 如果差值 <= 0，说明val <= minNum，更新minNum，推入差值
- Pop
  - 出栈并记录栈顶差值，更新最小元素
    - 如果栈顶差值 > 0，说明minNum仍然最小
    - 如果栈顶差值 <= 0，说明当前最小元素为`minNum - diff`
- Top
  - 如果栈顶差值 > 0，说明栈顶真正元素为`(int)(minNum + diff)`
  - 否则，说明栈顶元素就是`(int)(minNum)`

- GetMin
  - 直接返回`(int)minNum`


```C#
public class MinStack {
    private long minNum = 0;
    private Stack<long> sta = new Stack<long>();

    public MinStack() {
        
    }
    
    public void Push(int val) {
        if (sta.Count == 0) {
            minNum = val;
            sta.Push(0);
        }
        else {
            long diff = val - minNum;
            minNum = diff > 0 ? minNum : val;
            sta.Push(diff);
        }
    }
    
    public void Pop() {
        long diff = sta.Peek();
        sta.Pop();
        minNum = diff > 0 ? minNum : minNum - diff;
    }
    
    public int Top() {
        long diff = sta.Peek();
        if (diff > 0) {
            return (int)(minNum + diff);
        }
        else {
            return (int)minNum;
        }
    }
    
    public int GetMin() {   
        return (int)minNum;
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.Push(val);
 * obj.Pop();
 * int param_3 = obj.Top();
 * int param_4 = obj.GetMin();
 */
```

# 第8题-98. 验证二叉搜索树

## 中序遍历，存储遍历结果，然后比较、

由于二叉搜索树的性质，中序遍历的结果一定是有序的。所以，我们可以中序遍历二叉搜索树，然后保存遍历结果，然后再遍历一次，判断是否是升序的即可。

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    List<int> nums = new List<int>();

    void Dfs(TreeNode root) {
        if (root == null) {
            return;
        }
        Dfs(root.left);
        nums.Add(root.val);
        Dfs(root.right);
    }

    public bool IsValidBST(TreeNode root) {
        Dfs(root);
        for (int i = 0; i < nums.Count; ++i) {
            if (i > 0 && nums[i] <= nums[i - 1]) {
                return false;
            }
        }
        return true;
    }
}
```

## 迭代中序遍历，记录上一个值

我们也可以使用迭代中序遍历，记录上一个节点的值，与当前节点的值进行比较。

如果当前节点的值大于上一个节点的值，返回false。

注意：
pre（上一个节点的值）初始时需要初始化为`long.MinValue`
因为 `long.MinValue < int.MinValue`

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    public bool IsValidBST(TreeNode root) {
        Stack<TreeNode> sta = new Stack<TreeNode>();
        long pre = long.MinValue;
        while (sta.Count != 0 || root != null) {
            while (root != null) {
                sta.Push(root);
                root = root.left;
            }
            root = sta.Pop();
            if (root.val <= pre) {
                return false;
            }
            pre = root.val;
            root = root.right;
        }
        return true;
    }
}
```

## 利用二叉搜索树性质，递归

由于是二叉搜索树，当前元素，一定 > 左边的元素，一定 < 右边的元素。

也就是说，当前节点的元素，一定是在`(left, right)`。

所以，我们可以递归的判断当前元素是否符合。

递归时，`Dfs(root.left, left, root.val)` `Dfs(root.right, root.val, right)`

初始时，`left = long.MinValue`，`right = long.MaxValue`

注意：我们需要使用long，因为`long.MaxValue > int.MaxValue`

```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    bool Dfs(TreeNode root, long left, long right) {
        if (root == null) {
            return true;
        }
        if (root.val <= left || root.val >= right) {
            return false;
        }
        return Dfs(root.left, left, root.val) && Dfs(root.right, root.val, right);
    }

    public bool IsValidBST(TreeNode root) {
        return Dfs(root, long.MinValue, long.MaxValue);
    }
}
```

# 第9题-200. 岛屿数量

经典的搜索题，可以使用Bfs和Dfs解决

> [200. 岛屿数量 - 力扣（Leetcode）](https://leetcode.cn/problems/number-of-islands/)

## Bfs

遍历数组，每次遇到一个`1`，进行一次Bfs。

Bfs中，每次对于这个点，向上下左右四个方向扩展，发现是岛屿，修改为0，放入队列当中。

遍历过程中，每遇到一个`1`，即遇到一个岛屿，记录一次答案。

注意：Bfs过程当中，一遇到是`1`，就立马将当前格子变为`0`，不然可能重复加入，造成多余的遍历判断。

```C#
public class Solution {
    int[] dirx = new int[4] {0, 0, -1, 1};
    int[] diry = new int[4] {-1 , 1, 0, 0};
    int n = 0;
    int m = 0;

    void Bfs(char[][] grid, int row, int col) {
        Queue<int[]> que = new Queue<int[]>();
        char mark = grid[row][col];
        que.Enqueue(new int[]{row, col});
        grid[row][col] = '0';
        while (que.Count != 0) {
            int x = que.Peek()[0];
            int y = que.Peek()[1];
            que.Dequeue();
            
            for (int i = 0; i < 4; ++i) {
                int nx = x + dirx[i];
                int ny = y + diry[i];
                if (nx >= 0 && ny >= 0 && nx < n && ny < m) {
                    if (grid[nx][ny] == mark) {
                        grid[nx][ny] = '0';
                        que.Enqueue(new int[]{nx, ny});
                    }
                }
            }
        }
    }

    public int NumIslands(char[][] grid) {
        n = grid.Length;
        m = grid[0].Length;
        int ans = 0;
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                if (grid[i][j] == '1') {
                    ++ans;
                    Bfs(grid, i, j);
                }
            }
        }
        return ans;
    }
}
```



## Dfs

遍历数组，每次遇到一个`1`，我们就进行dfs。

dfs中，向上下左右四个方向进行dfs，将四个方向上的`1`变为0。

在遍历过程当中，没遇到一次1，就是遇到了一个岛屿，记录一次答案。

```C#
public class Solution {
    int[] dirx = new int[4] {0, 0, -1, 1};
    int[] diry = new int[4] {-1 , 1, 0, 0};
    int n = 0;
    int m = 0;

    void Dfs(char[][] grid, int x, int y) {
        if (x < 0 || y < 0 || x >= n || y >= m || grid[x][y] == '0') {
            return;
        }
        grid[x][y] = '0';
        Dfs(grid, x, y + 1);
        Dfs(grid, x, y - 1);
        Dfs(grid, x + 1, y);
        Dfs(grid, x - 1, y);
    }

    public int NumIslands(char[][] grid) {
        n = grid.Length;
        m = grid[0].Length;
        int ans = 0;
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                if (grid[i][j] == '1') {
                    ++ans;
                    Dfs(grid, i, j);
                }
            }
        }
        return ans;
    }
}
```



# ---------------------------------------

# 第6周

# 第1题-994. 腐烂的橘子

## Bfs

根据题意，需要统计橘子需要多少时间感染为坏橘子。

那么，我们先将所有坏橘子入队，然后使用Bfs，每次将每一个烂橘子的周围的好橘子变为坏橘子，并加入队列当中。

每进行一次感染后，如果队列不为空，说明进行了感染，我们加一次答案。

Bfs后，我们还需要进行一次遍历，判断是否有单独的橘子出现，如果有返回-1，没有返回ans。

```C#
public class Solution {
    public int OrangesRotting(int[][] grid) {
        int n = grid.Length;
        int m = grid[0].Length;
        Queue<int[]> que = new Queue<int[]>();
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                if (grid[i][j] == 2) {
                    que.Enqueue(new int[] { i, j});
                }
            }
        }
        int[] dirx = new int[4] {0, 0, -1, 1};
        int[] diry = new int[4] {-1, 1, 0, 0};
        int ans = 0;
        while (que.Count != 0) {
            int size = que.Count;
            for (int l = 0; l < size; ++l) {
                int x = que.Peek()[0];
                int y = que.Peek()[1];
                que.Dequeue();
                for (int k = 0; k < 4; ++k) {
                    int nx = x + dirx[k];
                    int ny = y + diry[k];
                    if (nx >= 0 && ny >= 0 && nx < n && ny < m) {
                        if (grid[nx][ny] == 1) {
                            que.Enqueue(new int[2]{ nx, ny});
                            grid[nx][ny] = 2;
                        }
                    }
                }
            }
            if (que.Count != 0) {
                ++ans;
            }
        }
        foreach(var ary in grid) {
            foreach(var item in ary) {
                if(item == 1) {
                    return -1;
                }
            }
        } 
        return ans;
    }
}
```

## Bfs小优化

在记录烂橘子的时候，我们可以同时记录好橘子的数量。

每一次感染到好橘子，就将好橘子的数量-1，如果途中好橘子数量为0，直接返回答案，否则返回-1。

注意：

- 由于可能刚开始就没有好橘子，所以，我们在记录完好橘子的数量之后，判断一次好橘子数量是否为0，为0直接返回0。
- 在一次Bfs结束后，需要在判断完队列长度后再判断好橘子数量，不然可能少算一次感染。

```C#
public class Solution {
    public int OrangesRotting(int[][] grid) {
        int n = grid.Length;
        int m = grid[0].Length;
        int orange = 0;
        Queue<int[]> que = new Queue<int[]>();
        for (int i = 0; i < n; ++i) {
            for (int j = 0; j < m; ++j) {
                if (grid[i][j] == 2) {
                    que.Enqueue(new int[] { i, j});
                }
                if (grid[i][j] == 1) {
                    ++orange;
                }
            }
        }
        //特判
        if (orange == 0) {
            return 0;
        }
        int[] dirx = new int[4] {0, 0, -1, 1};
        int[] diry = new int[4] {-1, 1, 0, 0};
        int ans = 0;
        while (que.Count != 0) {
            int size = que.Count;
            for (int l = 0; l < size; ++l) {
                int x = que.Peek()[0];
                int y = que.Peek()[1];
                que.Dequeue();
                for (int k = 0; k < 4; ++k) {
                    int nx = x + dirx[k];
                    int ny = y + diry[k];
                    if (nx >= 0 && ny >= 0 && nx < n && ny < m) {
                        if (grid[nx][ny] == 1) {
                            que.Enqueue(new int[2]{ nx, ny});
                            grid[nx][ny] = 2;
                            --orange;
                        }
                    }
                }
            }
            if (que.Count != 0) {
                ++ans;
            }
            //注意！必须判断队列数量之后才返回，不然会少算一次感染
            if (orange == 0) {
                return ans;
            }
        }
        return -1;
    }
}
```

# 第2题-33. 搜索旋转排序数组

> 题目要求：必须设计一个时间复杂度为 `O(log n)` 的算法解决此问题

## 二分查找

我们知道，只有对于有序的区间，才能进行二分查找。

但是题目给定的数组是经过旋转的，也就是说，是局部有序的。

那么，我们可以在二分查找过程当中寻找有序区间。

- 如果 `[left, mid)`有序，并且target在此区间内，那么，我们在这个区间内查找。否则到无序区查找。
  - 此时无序区是 `[mid + 1, right]`
- 如果 `(mid, right]`有序，并且target在此区间内，那么，我们在这个区间内查找。否则到无序区查找。
  - 此时无序区是 `[left, mid - 1]`

具体到代码上，就是

```C#
if (nums[left] <= nums[mid]) {
    //如果 `[left, mid)`有序，并且target在此区间内，
    //那么，我们在这个区间内查找。否则到无序区查找。
    if (nums[left] <= target && target < nums[mid]) {
        right = mid - 1;
    }
    else {
        //到无序区查找
        left = mid + 1;
    }
}
else {
    //如果 `(mid, right]`有序，并且target在此区间内，
    //那么，我们在这个区间内查找。否则到无序区查找。
    if (nums[mid] < target && target <= nums[right]) {
        left = mid + 1;
    }
    else {
        //到无序区查找
        right = mid - 1;
    }
}
```

全部代码

```Cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size() - 1;
        while(left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) return mid;
            if (nums[left] <= nums[mid]) {
                if (nums[left] <= target && target < nums[mid]) {
                    right = mid - 1;
                }
                else {
                    left = mid + 1;
                }
            }
            else {
                if (nums[mid] < target && target <= nums[right]) {
                    left = mid + 1;
                }
                else {
                    right = mid - 1;
                }
            }
        }
        return -1;
    }
};
```

