# [798. 得分最高的最小轮调](https://leetcode-cn.com/problems/smallest-rotation-with-highest-score)

[English Version](/solution/0700-0799/0798.Smallest%20Rotation%20with%20Highest%20Score/README_EN.md)

## 题目描述

<!-- 这里写题目描述 -->

<p>给定一个数组&nbsp;<code>A</code>，我们可以将它按一个非负整数 <code>K</code>&nbsp;进行轮调，这样可以使数组变为&nbsp;<code>A[K], A[K+1], A{K+2], ... A[A.length - 1], A[0], A[1], ..., A[K-1]</code>&nbsp;的形式。此后，任何值小于或等于其索引的项都可以记作一分。</p>

<p>例如，如果数组为&nbsp;<code>[2, 4, 1, 3, 0]</code>，我们按&nbsp;<code>K = 2</code>&nbsp;进行轮调后，它将变成&nbsp;<code>[1, 3, 0, 2, 4]</code>。这将记作 3 分，因为 1 &gt; 0 [no points], 3 &gt; 1 [no points], 0 &lt;= 2 [one point], 2 &lt;= 3 [one point], 4 &lt;= 4 [one point]。</p>

<p>在所有可能的轮调中，返回我们所能得到的最高分数对应的轮调索引 K。如果有多个答案，返回满足条件的最小的索引 K。</p>

<p>&nbsp;</p>

<p><strong>示例 1：</strong></p>

<pre><strong>输入：</strong>[2, 3, 1, 4, 0]
<strong>输出：</strong>3
<strong>解释：</strong>
下面列出了每个 K 的得分：
K = 0,  A = [2,3,1,4,0],    score 2
K = 1,  A = [3,1,4,0,2],    score 3
K = 2,  A = [1,4,0,2,3],    score 3
K = 3,  A = [4,0,2,3,1],    score 4
K = 4,  A = [0,2,3,1,4],    score 3
所以我们应当选择&nbsp;K = 3，得分最高。</pre>

<p><strong>示例 2：</strong></p>

<pre><strong>输入：</strong>[1, 3, 0, 2, 4]
<strong>输出：</strong>0
<strong>解释：</strong>
A 无论怎么变化总是有 3 分。
所以我们将选择最小的 K，即 0。
</pre>

<p>&nbsp;</p>

<p><strong>提示：</strong></p>

<ul>
	<li><code>A</code>&nbsp;的长度最大为&nbsp;<code>20000</code>。</li>
	<li><code>A[i]</code> 的取值范围是&nbsp;<code>[0, A.length]</code>。</li>
</ul>

## 解法

<!-- 这里可写通用的实现逻辑 -->

差分数组。

对于每个数，都有一个固定的 k 生效区间。我们先利用差分，预处理每个数的 k 生效区间。有最多个数能覆盖到的 k 即是答案。

<!-- tabs:start -->

### **Python3**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```python
class Solution:
    def bestRotation(self, nums: List[int]) -> int:
        n = len(nums)
        mx, ans = -1, n
        d = [0] * n
        for i, v in enumerate(nums):
            l, r = (i + 1) % n, (n + i + 1 - v) % n
            d[l] += 1
            d[r] -= 1
        s = 0
        for k, t in enumerate(d):
            s += t
            if s > mx:
                mx = s
                ans = k
        return ans
```

### **Java**

<!-- 这里可写当前语言的特殊实现逻辑 -->

```java
class Solution {
    public int bestRotation(int[] nums) {
        int n = nums.length;
        int[] d = new int[n];
        for (int i = 0; i < n; ++i) {
            int l = (i + 1) % n;
            int r = (n + i + 1 - nums[i]) % n;
            ++d[l];
            --d[r];
        }
        int mx = -1;
        int s = 0;
        int ans = n;
        for (int k = 0; k < n; ++k) {
            s += d[k];
            if (s > mx) {
                mx = s;
                ans = k;
            }
        }
        return ans;
    }
}
```

### **C++**

```cpp
class Solution {
public:
    int bestRotation(vector<int>& nums) {
        int n = nums.size();
        int mx = -1, ans = n;
        vector<int> d(n);
        for (int i = 0; i < n; ++i)
        {
            int l = (i + 1) % n;
            int r = (n + i + 1 - nums[i]) % n;
            ++d[l];
            --d[r];
        }
        int s = 0;
        for (int k = 0; k < n; ++k)
        {
            s += d[k];
            if (s > mx)
            {
                mx = s;
                ans = k;
            }
        }
        return ans;
    }
};
```

### **Go**

```go
func bestRotation(nums []int) int {
	n := len(nums)
	d := make([]int, n)
	for i, v := range nums {
		l, r := (i+1)%n, (n+i+1-v)%n
		d[l]++
		d[r]--
	}
	mx, ans, s := -1, n, 0
	for k, t := range d {
		s += t
		if s > mx {
			mx = s
			ans = k
		}
	}
	return ans
}
```

### **...**

```

```

<!-- tabs:end -->
