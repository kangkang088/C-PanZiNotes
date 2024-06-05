# 个人在各种网站做过的算法题整理

开始于2022年8月

# 一、排序
## 简单中等
## 1.【力扣148】排序链表（归并排序）

[148. 排序链表](https://leetcode.cn/problems/sort-list/)

#### **为什么fast需要初始化为head->next->next或者head->next而不能初始化为head?**

> 当链表节点只有两个时，由于每次mergeSort中slow都只进了一步，每次right都为nullptr，每次都将执行一次mergeSort(head)，此时会无限循环

## 2.【力扣56】合并区间（排序后应用）

[56. 合并区间](https://leetcode.cn/problems/merge-intervals/)

## 3.【力扣179】最大数（特殊排序规则）
[179. 最大数](https://leetcode.cn/problems/largest-number/)

## 4.【力扣87】颜色排序（三数排序）
[75. 颜色分类](https://leetcode.cn/problems/sort-colors/)
## 5.【力扣215】数组中的第K个最大元素（快速选择，堆排序）

[215. 数组中的第K个最大元素](https://leetcode.cn/problems/kth-largest-element-in-an-array/)

## 6.【力扣1636. 按照频率将数组升序排序】计算数据然后排序

[1636. 按照频率将数组升序排序](https://leetcode.cn/problems/sort-array-by-increasing-frequency/)

## 7.【力扣791. 自定义字符串排序】按照下标排序

[791. 自定义字符串排序 - 力扣（Leetcode）](https://leetcode.cn/problems/custom-sort-string/description/)

# 二、数组

## 简单中等
## 1.【力扣704. 二分查找】

[704. 二分查找](https://leetcode.cn/problems/binary-search/)

## 3.【力扣209. 长度最小的字数组】滑动窗口

[209. 长度最小的子数组 - 力扣（LeetCode）](https://leetcode.cn/problems/minimum-size-subarray-sum/)

## 4.【力扣1413. 逐步求和得到正数的最小值】求前缀和最小值

[1413. 逐步求和得到正数的最小值](https://leetcode.cn/problems/minimum-value-to-get-positive-step-by-step-sum/)

## 5.【力扣1450. 在既定时间做作业的学生人数】差分数组，二分查找

[1450. 在既定时间做作业的学生人数](https://leetcode.cn/problems/number-of-students-doing-homework-at-a-given-time/)
## 6.【力扣1460. 通过翻转子数组使两个数组相等】排序、哈希表

[1460. 通过翻转子数组使两个数组相等](https://leetcode.cn/problems/make-two-arrays-equal-by-reversing-sub-arrays/)
## 7.【力扣658. 找到 K 个最接近的元素】

[658. 找到 K 个最接近的元素](https://leetcode.cn/problems/find-k-closest-elements/)
## 8.【力扣1464. 数组中两元素的最大乘积】 

[1464. 数组中两元素的最大乘积](https://leetcode.cn/problems/maximum-product-of-two-elements-in-an-array/)

## 9.【力扣6160. 和有限的最长子序列】 

[6160. 和有限的最长子序列](https://leetcode.cn/problems/longest-subsequence-with-limited-sum/)

## 10.【力扣1470. 重新排列数组】 

[1470. 重新排列数组 - 力扣（Leetcode）](https://leetcode.cn/problems/shuffle-the-array/description/)
## 11.【力扣15. 三数之和】 双指针

[15. 三数之和 - 力扣（Leetcode）](https://leetcode.cn/problems/3sum/description/)
## 12.【力扣18. 四数之和】双指针去重

[18. 四数之和](https://leetcode.cn/problems/4sum/)

## 13.【力扣1475. 商品折扣后的最终价格】

[1475. 商品折扣后的最终价格](https://leetcode.cn/problems/final-prices-with-a-special-discount-in-a-shop/)

## 14.【力扣646. 最长数对链】贪心

[646. 最长数对链](https://leetcode.cn/problems/maximum-length-of-pair-chain/)

## 15.【力扣1582. 二进制矩阵中的特殊位置】 计数查找

[1582. 二进制矩阵中的特殊位置](https://leetcode.cn/problems/special-positions-in-a-binary-matrix/)

## 16.【力扣27. 移除元素】 双指针

[27. 移除元素](https://leetcode.cn/problems/remove-element/)

## 17.【力扣667. 优美的排列 II】找规律

[667. 优美的排列 II](https://leetcode.cn/problems/beautiful-arrangement-ii/)

## 18.【力扣1608. 特殊数组的特征值】 

[1608. 特殊数组的特征值](https://leetcode.cn/problems/special-array-with-x-elements-greater-than-or-equal-x/)

## 19.【力扣670. 最大交换】

[670. 最大交换](https://leetcode.cn/problems/maximum-swap/)

## 20.【力扣1619. 删除某些元素后的数组均值】 

[1619. 删除某些元素后的数组均值](https://leetcode.cn/problems/mean-of-array-after-removing-some-elements/)

## 21.【力扣1652. 拆炸弹】分情况模拟

[1652. 拆炸弹](https://leetcode.cn/problems/defuse-the-bomb/)

## 22.【力扣1800. 最大升序子数组和】

[1800. 最大升序子数组和](https://leetcode.cn/problems/maximum-ascending-subarray-sum/)

## 23.【力扣870. 优势洗牌】排序下标，田忌赛马

[870. 优势洗牌](https://leetcode.cn/problems/advantage-shuffle/)

## 24.【力扣769. 最多能完成排序的块】贪心

[769. 最多能完成排序的块 - 力扣（Leetcode）](https://leetcode.cn/problems/max-chunks-to-make-sorted/description/)

> 元素范围在0~n-1，则如果能排序的块，下标和一定等于元素和
>
> 分别记录下标和与元素和，判断是否相等，相等则这个块可排序，++ret

## 25.【力扣169. 多数元素】找出现n/2次的数

[169. 多数元素 - 力扣（Leetcode）](https://leetcode.cn/problems/majority-element/description/)

> 方法一：使用哈希表
>
> 方法二：直接排序，返回中位数

## 26.【力扣904. 水果成篮】滑动窗口

[904. 水果成篮 - 力扣（Leetcode）](https://leetcode.cn/problems/fruit-into-baskets/description/)

## 27.【力扣1732. 找到最高海拔】

[1732. 找到最高海拔 - 力扣（Leetcode）](https://leetcode.cn/problems/find-the-highest-altitude/description/)

## 28.【力扣795. 区间子数组个数】双指针记录位置

[795. 区间子数组个数 - 力扣（Leetcode）](https://leetcode.cn/problems/number-of-subarrays-with-bounded-maximum/description/)

## 困难

## 1.【力扣927. 三等分】

[927. 三等分](https://leetcode.cn/problems/three-equal-parts/)

> 记录每一等分0的位置
>
> if (first + len <= second && second + len <= third)是因为third - len 的位置是无法改变的

# 三、模拟

## 简单中等

## 1.【力扣640】求解方程（模拟只有加减的解方程）

[640. 求解方程](https://leetcode.cn/problems/solve-the-equation/)


## 2.【力扣1417】重新格式化字符串

[1417. 重新格式化字符串](https://leetcode.cn/problems/reformat-the-string/)


## 3.【力扣54】螺旋矩阵（按层模拟）

[54. 螺旋矩阵](https://leetcode.cn/problems/spiral-matrix/)

## 4.【力扣59】螺旋矩阵 II（按层模拟）

[59. 螺旋矩阵 II](https://leetcode.cn/problems/spiral-matrix-ii/)

## 5.【力扣1620. 网络信号最好的坐标】（暴力）

[1620. 网络信号最好的坐标 - 力扣（Leetcode）](https://leetcode.cn/problems/coordinate-with-maximum-network-quality/)

## 14.【力扣1138. 字母板上的路径】根据下标模拟

[1138. 字母板上的路径 - 力扣（Leetcode）](https://leetcode.cn/problems/alphabet-board-path/)

# 四、链表

## 简单中等

## 1.【力扣203】删除链表元素

[203. 移除链表元素](https://leetcode.cn/problems/remove-linked-list-elements/)

## 2.【力扣206】反转链表

[206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)

## 3.【力扣876】链表的中间节点

[876. 链表的中间结点](https://leetcode.cn/problems/middle-of-the-linked-list/)

## 4.【力扣141】环形链表

[141. 环形链表](https://leetcode.cn/problems/linked-list-cycle/)


## 5.【力扣92】 反转链表 II

[92. 反转链表 II](https://leetcode.cn/problems/reverse-linked-list-ii/)


## 6.【力扣328】奇偶链表（双指针）

[328. 奇偶链表](https://leetcode.cn/problems/odd-even-linked-list/)

## 7.【力扣24】两两交换链表中的节点（双指针）

[24. 两两交换链表中的节点](https://leetcode.cn/problems/swap-nodes-in-pairs/)

## 8.【力扣19】删除链表的倒数第 N 个结点（快慢指针）

[19. 删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)


## 9.【力扣面试题 02.07】链表相交(双指针)

[面试题 02.07. 链表相交](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/)

lenA + lenB = lenB + lenA


## 10.【力扣142】环形链表 II（快慢指针求链表相交入口）

[142. 环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/)

## 11.【力扣21. 合并两个有序链表】归并的一次操作

[21. 合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/)

## 12.【力扣2. 两数相加】模拟

[2. 两数相加 - 力扣（Leetcode）](https://leetcode.cn/problems/add-two-numbers/description/)

# 五、哈希表

## 简单中等

## 1.【力扣1282】用户分组

[1282. 用户分组](https://leetcode.cn/problems/group-the-people-given-the-group-size-they-belong-to/)

## 2.【力扣242】有效的字母异位词

[242. 有效的字母异位词](https://leetcode.cn/problems/valid-anagram/)

## 3.【力扣349】两个数组的交集

[349. 两个数组的交集](https://leetcode.cn/problems/intersection-of-two-arrays/)

## 4.【力扣202】快乐数

[202. 快乐数](https://leetcode.cn/problems/happy-number/)


## 5.【力扣1】两数之和

[1. 两数之和](https://leetcode.cn/problems/two-sum/)

## 6.【力扣383】 赎金信

[383. 赎金信 - 力扣（Leetcode）](https://leetcode.cn/problems/ransom-note/description/)

## 7.【力扣1624. 两个相同字符之间的最长子字符串】

[1624. 两个相同字符之间的最长子字符串](https://leetcode.cn/problems/largest-substring-between-two-equal-characters/)

## 8.【力扣1640. 能否连接形成数组】

[1640. 能否连接形成数组](https://leetcode.cn/problems/check-array-formation-through-concatenation/)

## 9.【力扣817. 链表组件】

[817. 链表组件 - 力扣（Leetcode）](https://leetcode.cn/problems/linked-list-components/description/)

## 10.【力扣1684. 统计一致字符串的数目】

[1684. 统计一致字符串的数目 - 力扣（Leetcode）](https://leetcode.cn/problems/count-the-number-of-consistent-strings/description/)

## 11.【力扣1704. 判断字符串的两半是否相似】

[1704. 判断字符串的两半是否相似 - 力扣（Leetcode）](https://leetcode.cn/problems/determine-if-string-halves-are-alike/description/)

## 12.【力扣1742. 盒子中小球的最大数量】

[1742. 盒子中小球的最大数量 - 力扣（Leetcode）](https://leetcode.cn/problems/maximum-number-of-balls-in-a-box/)

## 13.【力扣1604. 警告一小时内使用相同员工卡大于等于三次的人】

[1604. 警告一小时内使用相同员工卡大于等于三次的人 - 力扣（Leetcode）](https://leetcode.cn/problems/alert-using-same-key-card-three-or-more-times-in-a-one-hour-period/description/)

## 14.【力扣1138. 字母板上的路径】根据下标模拟

[1138. 字母板上的路径 - 力扣（Leetcode）](https://leetcode.cn/problems/alphabet-board-path/)

## 困难

## 1.【力扣1224】最大相等频率

[1224. 最大相等频率](https://leetcode.cn/problems/maximum-equal-frequency/)

## 2.*【力扣726. 原子的数量】栈+哈希表

[726. 原子的数量 - 力扣（Leetcode）](https://leetcode.cn/problems/number-of-atoms/solutions/)

# 六、字符串

## 简单中等

## 1.【力扣1422】分割字符串的最大得分（字符计数）

[1422. 分割字符串的最大得分](https://leetcode.cn/problems/maximum-score-after-splitting-a-string/)

**注意如何处理不同分割情况**


## 2.【力扣1455】检查单词是否为句中其他单词的前缀（双指针）

[1455. 检查单词是否为句中其他单词的前缀](https://leetcode.cn/problems/check-if-a-word-occurs-as-a-prefix-of-any-word-in-a-sentence/)

## 3.【力扣6161】 从字符串中移除星号（双指针）

[6161. 从字符串中移除星号 - 力扣（Leetcode）](https://leetcode.cn/problems/removing-stars-from-a-string/description/)


## 4.【力扣344】反转字符串（双指针）

[344. 反转字符串](https://leetcode.cn/problems/reverse-string/)

## 5.【力扣541】反转字符串 II

[541. 反转字符串 II](https://leetcode.cn/problems/reverse-string-ii/)

## 6.【力扣剑指 Offer 05】替换空格

[剑指 Offer 05. 替换空格](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)

## 7.【力扣151】反转字符串中的单词

[151. 反转字符串中的单词](https://leetcode.cn/problems/reverse-words-in-a-string/)

## 8.【力扣剑指 Offer 58 - II】左旋转字符串

[剑指 Offer 58 - II. 左旋转字符串](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

## 9.【力扣28】实现 strStr() （KMP）

[28. 实现 strStr()](https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string/)

## 10.【力扣828】 统计子串中的唯一字符（哈希表+动态规划）

[828. 统计子串中的唯一字符](https://leetcode.cn/problems/count-unique-characters-of-all-substrings-of-a-given-string/)

## 11.【力扣1592】重新排列单词间的空格

[1592. 重新排列单词间的空格](https://leetcode.cn/problems/rearrange-spaces-between-words/)

## 12.【力扣1694. 重新格式化电话号码】字符串处理模拟

[1694. 重新格式化电话号码](https://leetcode.cn/problems/reformat-phone-number/)

## 13.【力扣777. 在LR字符串中交换相邻字符】双指针

[777. 在LR字符串中交换相邻字符](https://leetcode.cn/problems/swap-adjacent-in-lr-string/)

> 判断L和R的位置
>
> 由于L只能向左移动，i的位置一定比j大
>
> 由于R只能向右移动，i的位置一定比j小

## 14.【力扣1784. 检查二进制字符串字段】记录1的数量

[1784. 检查二进制字符串字段](https://leetcode.cn/problems/check-if-binary-string-has-at-most-one-segment-of-ones/)

## 15.【力扣811. 子域名访问计数】模拟

[811. 子域名访问计数](https://leetcode.cn/problems/subdomain-visit-count/)

## 16.【力扣1790. 仅执行一次字符串交换能否使两个字符串相等】

[1790. 仅执行一次字符串交换能否使两个字符串相等](https://leetcode.cn/problems/check-if-one-string-swap-can-make-strings-equal/)

## 17.【力扣125. 验证回文串】使用api

[125. 验证回文串 - 力扣（Leetcode）](https://leetcode.cn/problems/valid-palindrome/description/)

## 18.【力扣1768. 交替合并字符串】模拟

[1768. 交替合并字符串 - 力扣（Leetcode）](https://leetcode.cn/problems/merge-strings-alternately/description/)

## 19.【力扣1662. 检查两个字符串数组是否相等】构造、双指针

[1662. 检查两个字符串数组是否相等 - 力扣（Leetcode）](https://leetcode.cn/problems/check-if-two-string-arrays-are-equivalent/)

## 20.【力扣1668. 最大重复子字符串】KMP\暴力

[1668. 最大重复子字符串 - 力扣（Leetcode）](https://leetcode.cn/problems/maximum-repeating-substring/)

## 21.【力扣1678. 设计 Goal 解析器】模拟构造

[1678. 设计 Goal 解析器 - 力扣（Leetcode）](https://leetcode.cn/problems/goal-parser-interpretation/description/)

## 22.【力扣816. 模糊坐标】枚举

[816. 模糊坐标 - 力扣（Leetcode）](https://leetcode.cn/problems/ambiguous-coordinates/description/)

## 23.【力扣434. 字符串中的单词数】

[434. 字符串中的单词数 - 力扣（Leetcode）](https://leetcode.cn/problems/number-of-segments-in-a-string/description/)

## 24.【力扣792. 匹配子序列的单词数】哈希表+二分查找

[792. 匹配子序列的单词数 - 力扣（Leetcode）](https://leetcode.cn/problems/number-of-matching-subsequences/description/)

# 七、贪心

## 简单中等

## 1.【力扣1710. 卡车上的最大单元数】

[1710. 卡车上的最大单元数 - 力扣（Leetcode）](https://leetcode.cn/problems/maximum-units-on-a-truck/description/)

## 困难

# 八、栈

## 简单中等

## 1.【力扣636函数的独占时间】栈模拟

[636. 函数的独占时间](https://leetcode.cn/problems/exclusive-time-of-functions/)

## 2.【力扣946验证栈序列】栈模拟

[946. 验证栈序列](https://leetcode.cn/problems/validate-stack-sequences/)

## 3.【力扣1598文件夹操作日志搜集器】栈模拟

[1598. 文件夹操作日志搜集器](https://leetcode.cn/problems/crawler-log-folder/)

## 4.【力扣20有效的括号】 栈模拟

[20. 有效的括号](https://leetcode.cn/problems/valid-parentheses/)

## 5.【力扣1047删除字符串中的所有相邻重复项】 

[1047. 删除字符串中的所有相邻重复项](https://leetcode.cn/problems/remove-all-adjacent-duplicates-in-string/)

## 6.【力扣150逆波兰表达式求值】 栈模拟

[150. 逆波兰表达式求值](https://leetcode.cn/problems/evaluate-reverse-polish-notation/)

## 7.【力扣921. 使括号有效的最少添加】栈模拟

[921. 使括号有效的最少添加](https://leetcode.cn/problems/minimum-add-to-make-parentheses-valid/)

## 8.【力扣20. 有效的括号】栈模拟

[20. 有效的括号](https://leetcode.cn/problems/valid-parentheses/)

> 可以直接使用string作为一个栈

## 9.【力扣856. 括号的分数】栈模拟，计算括号深度

[856. 括号的分数](https://leetcode.cn/problems/score-of-parentheses/)

## 10.【力扣1441. 用栈操作构建数组】栈模拟

[1441. 用栈操作构建数组 - 力扣（Leetcode）](https://leetcode.cn/problems/build-an-array-with-stack-operations/description/)

## 11.【901. 股票价格跨度】单调栈模拟

[901. 股票价格跨度 - 力扣（Leetcode）](https://leetcode.cn/problems/online-stock-span/description/)

## 困难

## 1.【力扣768最多能完成排序的块 II】单调栈

[768. 最多能完成排序的块 II](https://leetcode.cn/problems/max-chunks-to-make-sorted-ii/)

## 2.【力扣1106. 解析布尔表达式】栈模拟

[1106. 解析布尔表达式 - 力扣（Leetcode）](https://leetcode.cn/problems/parsing-a-boolean-expression/description/)

## 3.*【力扣726. 原子的数量】栈+哈希表

[726. 原子的数量 - 力扣（Leetcode）](https://leetcode.cn/problems/number-of-atoms/solutions/)

# 九、队列

## 简单中等

## 1.【力扣346数据流中的移动平均值】队列模拟

[346. 数据流中的移动平均值_Finish_Hou的博客-CSDN博客](https://blog.csdn.net/qq_37548441/article/details/119305958)

## 2.【力扣347前 K 个高频元素】 优先队列

[347. 前 K 个高频元素](https://leetcode.cn/problems/top-k-frequent-elements/)

## 3.【力扣1700. 无法吃午餐的学生数量】队列模拟

[1700. 无法吃午餐的学生数量 - 力扣（Leetcode）](https://leetcode.cn/problems/number-of-students-unable-to-eat-lunch/description/)

## 困难

## 1.【力扣239 滑动窗口最大值】单调队列/优先队列

[239. 滑动窗口最大值](https://leetcode.cn/problems/sliding-window-maximum/)

# 十、设计

## 简单中等

## 1.【力扣1656】设计有序流

[1656. 设计有序流](https://leetcode.cn/problems/design-an-ordered-stream/)

## 2.【力扣641】 设计循环双端队列

[641. 设计循环双端队列](https://leetcode.cn/problems/design-circular-deque/)

## 3.【力扣225】用队列实现栈

[225. 用队列实现栈](https://leetcode.cn/problems/implement-stack-using-queues/)

## 4.【力扣707】设计链表

[707. 设计链表](https://leetcode.cn/problems/design-linked-list/)


## 5.【力扣155】最小栈

[155. 最小栈](https://leetcode.cn/problems/min-stack/)

## 6.【力扣232】用栈实现队列

[232. 用栈实现队列](https://leetcode.cn/problems/implement-queue-using-stacks/)

# 十一、树

## 简单中等

## 1.【力扣1302】层次最深叶子节点的和（层次遍历）

[1302. 层数最深叶子节点的和](https://leetcode.cn/problems/deepest-leaves-sum/)

## 2.【力扣654】最大二叉树（根据要求构建指定二叉树）

[654. 最大二叉树](https://leetcode.cn/problems/maximum-binary-tree/)

## 3.【力扣655】输出二叉树（DFS）

[655. 输出二叉树](https://leetcode.cn/problems/print-binary-tree/)

## 4.【力扣662】二叉树最大宽度

[662. 二叉树最大宽度](https://leetcode.cn/problems/maximum-width-of-binary-tree/)


## 5.【力扣998】 最大二叉树 II（最大二叉树插入值）

[998. 最大二叉树 II](https://leetcode.cn/problems/maximum-binary-tree-ii/)

## 6.【力扣687】最长同值路径（深度优先搜索）

[687. 最长同值路径](https://leetcode.cn/problems/longest-univalue-path/)

## 7.【力扣652】寻找重复的子树（序列化二叉树+哈希表）

[652. 寻找重复的子树](https://leetcode.cn/problems/find-duplicate-subtrees/)

## 8.【力扣669】 修剪二叉搜索树

[669. 修剪二叉搜索树](https://leetcode.cn/problems/trim-a-binary-search-tree/)

## 9.【力扣144】 二叉树的前序遍历

[144. 二叉树的前序遍历](https://leetcode.cn/problems/binary-tree-preorder-traversal/)

## 10.【力扣145】二叉树的后序遍历

[145. 二叉树的后序遍历](https://leetcode.cn/problems/binary-tree-postorder-traversal/)

## 11.【94】 二叉树的中序遍历

[94. 二叉树的中序遍历](https://leetcode.cn/problems/binary-tree-inorder-traversal/)

## 12.【力扣102】 二叉树的层序遍历

[102. 二叉树的层序遍历](https://leetcode.cn/problems/binary-tree-level-order-traversal/)

## 13.【力扣199】 二叉树的右视图

[199. 二叉树的右视图](https://leetcode.cn/problems/binary-tree-right-side-view/)

## 14.【力扣637】二叉树的层平均值

[637. 二叉树的层平均值](https://leetcode.cn/problems/average-of-levels-in-binary-tree/)

## 15.【力扣429】N 叉树的层序遍历

[429. N 叉树的层序遍历](https://leetcode.cn/problems/n-ary-tree-level-order-traversal/)

## 16.【力扣515】 在每个树行中找最大值

[515. 在每个树行中找最大值](https://leetcode.cn/problems/find-largest-value-in-each-tree-row/)

## 17.【力扣116】填充每个节点的下一个右侧节点指针（可以不使用层次遍历）

[116. 填充每个节点的下一个右侧节点指针](https://leetcode.cn/problems/populating-next-right-pointers-in-each-node/)

## 18.【力扣117】 填充每个节点的下一个右侧节点指针 II（可以不使用层次遍历）

[117. 填充每个节点的下一个右侧节点指针 II](https://leetcode.cn/problems/populating-next-right-pointers-in-each-node-ii/)

## 19.【力扣104 二叉树的最大深度】

[104. 二叉树的最大深度](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)

## 20.【力扣111二叉树的最小深度】

[111. 二叉树的最小深度](https://leetcode.cn/problems/minimum-depth-of-binary-tree/)

## 21.【力扣226. 翻转二叉树】

[226. 翻转二叉树](https://leetcode.cn/problems/invert-binary-tree/)

## 22.【力扣101. 对称二叉树】

[101. 对称二叉树](https://leetcode.cn/problems/symmetric-tree/)

## 23.【力扣589. N 叉树的前序遍历】

[589. N 叉树的前序遍历](https://leetcode.cn/problems/n-ary-tree-preorder-traversal/)

## 24.【力扣590. N 叉树的后序遍历】

[590. N 叉树的后序遍历](https://leetcode.cn/problems/n-ary-tree-postorder-traversal/)

## 25.【力扣101. 对称二叉树】

[101. 对称二叉树](https://leetcode.cn/problems/symmetric-tree/)

## 26.【力扣2331. 计算布尔二叉树的值】

[2331. 计算布尔二叉树的值 - 力扣（Leetcode）](https://leetcode.cn/problems/evaluate-boolean-binary-tree/description/)

## 27.【力扣208. 实现 Trie (前缀树)】

[208. 实现 Trie (前缀树) - 力扣（Leetcode）](https://leetcode.cn/problems/implement-trie-prefix-tree/description/)

# 十二、搜索

## 简单中等

## 1.【力扣797. 所有可能的路径】深度优先搜索

[797. 所有可能的路径](https://leetcode.cn/problems/all-paths-from-source-to-target/)

## 2.【力扣733. 图像渲染】dfs/bfs

[733. 图像渲染 - 力扣（Leetcode）](https://leetcode.cn/problems/flood-fill/description/)

## 困难

## 1.【827. 最大人工岛】深度优先搜索+标记

[827. 最大人工岛](https://leetcode.cn/problems/making-a-large-island/)

## 2【力扣854. 相似度为 K 的字符串】BFS+剪枝

[854. 相似度为 K 的字符串](https://leetcode.cn/problems/k-similar-strings/)

## 3.【力扣864. 获取所有钥匙的最短路径】BFS+状态压缩

[864. 获取所有钥匙的最短路径 - 力扣（Leetcode）](https://leetcode.cn/problems/shortest-path-to-get-all-keys/description/)

# 十三、回溯

## 简单中等

## 1.【698. 划分为k个相等的子集】桶记录回溯+约束条件

[698. 划分为k个相等的子集](https://leetcode.cn/problems/partition-to-k-equal-sum-subsets/)

## 困难

# 十四、动态规划

## 简单中等

## 1.【力扣790. 多米诺和托米诺平铺】

[790. 多米诺和托米诺平铺 - 力扣（Leetcode）](https://leetcode.cn/problems/domino-and-tromino-tiling/description/)

## 2.【力扣799. 香槟塔】

[799. 香槟塔 - 力扣（Leetcode）](https://leetcode.cn/problems/champagne-tower/description/)

## 困难

## 1.【力扣801. 使序列递增的最小交换次数】

[801. 使序列递增的最小交换次数](https://leetcode.cn/problems/minimum-swaps-to-make-sequences-increasing/)

## 2【力扣1235. 规划兼职工作】

[1235. 规划兼职工作 - 力扣（Leetcode）](https://leetcode.cn/problems/maximum-profit-in-job-scheduling/description/)

## 3.【力扣764. 最大加号标志】预处理4个方向上连续的1

[764. 最大加号标志 - 力扣（Leetcode）](https://leetcode.cn/problems/largest-plus-sign/)

> 考虑进一步优化，压缩在两个for内预处理

# 十五、数学

## 简单中等

## 1【力扣319. 灯泡开关】

[319. 灯泡开关](https://leetcode.cn/problems/bulb-switcher/)

## 2.【力扣672. 灯泡开关 Ⅱ】

[672. 灯泡开关 Ⅱ](https://leetcode.cn/problems/bulb-switcher-ii/)[672. 灯泡开关 Ⅱ](https://leetcode.cn/problems/bulb-switcher-ii/)

## 3.【力扣779. 第K个语法符号】有关树的位运算

[779. 第K个语法符号 - 力扣（Leetcode）](https://leetcode.cn/problems/k-th-symbol-in-grammar/description/)

## 4.【力扣754. 到达终点数字】推算公式

[754. 到达终点数字 - 力扣（Leetcode）](https://leetcode.cn/problems/reach-a-number/description/)

## 5.【力扣1017. 负二进制转换】除基取余

## 困难

## 1.【力扣793】 阶乘函数后 K 个零

[793. 阶乘函数后 K 个零 - 力扣（Leetcode）](https://leetcode.cn/problems/preimage-size-of-factorial-zeroes-function/)

# 十六、图

## 1.【力扣207. 课程表】拓扑排序（BFS+DFS）

[207. 课程表 - 力扣（Leetcode）](https://leetcode.cn/problems/course-schedule/)

## 2.【力扣210. 课程表 II】拓扑排序（BFS+DFS）

[210. 课程表 II - 力扣（Leetcode）](https://leetcode.cn/problems/course-schedule-ii/)

# 十七、其他算法

## 简单中等

## 1.【AtCoder】Disjoint Set Union（并查集模板题）

[A - Disjoint Set Union (atcoder.jp)](https://atcoder.jp/contests/practice2/tasks/practice2_a)

```Cpp
#include <stdio.h>
#include <stdlib.h>
#include <iostream>
#include <iomanip>
#include <vector>
#include <algorithm>
#include <unordered_map>
using namespace std;

int n = 0, q = 0;
vector<int> fa;
void init(int n) {
	fa = vector<int>(n);
	for (int i = 0; i < n; ++i) {
		fa[i] = i;
	}
}

int find(int i) {
	if (fa[i] == i) {
		return i;
	}
	else {
		fa[i] = find(fa[i]);
	}
	return fa[i];
}

void merge(int i, int j) {
	int fa_i = find(i);
	int fa_j = find(j);
	fa[fa_i] = fa_j;
}


void Solution() {
	int t, u, v;
	cin >> t >> u >> v;
	if (t == 0) {
		merge(u, v);
	}
	else {
		if (find(u) == find(v)) {
			cout << 1 << endl;
		}
		else {
			cout << 0 << endl;
		}
	}
}

int main()
{
	cin >> n >> q;
	init(n);
	while (q--) {
		Solution();
	}
	return 0;
}
```

