# [798. Smallest Rotation with Highest Score](https://leetcode.com/problems/smallest-rotation-with-highest-score)

[中文文档](/solution/0700-0799/0798.Smallest%20Rotation%20with%20Highest%20Score/README.md)

## Description

<p>&nbsp;Given an array <code>A</code>, we may rotate it by a non-negative integer <code>K</code> so that the array becomes <code>A[K], A[K+1], A{K+2], ... A[A.length - 1], A[0], A[1], ..., A[K-1]</code>.&nbsp; Afterward, any entries that are less than or equal to their index are worth 1 point.&nbsp;</p>

<p>For example, if we have <code>[2, 4, 1, 3, 0]</code>, and we rotate by <code>K = 2</code>, it becomes <code>[1, 3, 0, 2, 4]</code>.&nbsp; This is worth 3 points because 1 &gt; 0 [no points], 3 &gt; 1 [no points], 0 &lt;= 2 [one point], 2 &lt;= 3 [one point], 4 &lt;= 4 [one point].</p>

<p>Over all possible rotations, return the rotation index K that corresponds to the highest score we could receive.&nbsp; If there are multiple answers, return the smallest such index K.</p>

<pre>

<strong>Example 1:</strong>

<strong>Input:</strong> [2, 3, 1, 4, 0]

<strong>Output:</strong> 3

<strong>Explanation: </strong> 

Scores for each K are listed below: 

K = 0,  A = [2,3,1,4,0],    score 2

K = 1,  A = [3,1,4,0,2],    score 3

K = 2,  A = [1,4,0,2,3],    score 3

K = 3,  A = [4,0,2,3,1],    score 4

K = 4,  A = [0,2,3,1,4],    score 3

</pre>

<p>So we should choose K = 3, which has the highest score.</p>

<p>&nbsp;</p>

<pre>

<strong>Example 2:</strong>

<strong>Input:</strong> [1, 3, 0, 2, 4]

<strong>Output:</strong> 0

<strong>Explanation: </strong> A will always have 3 points no matter how it shifts.

So we will choose the smallest K, which is 0.

</pre>

<p><strong>Note:</strong></p>

<ul>
	<li><code>A</code>&nbsp;will have&nbsp;length at most <code>20000</code>.</li>
	<li><code>A[i]</code> will be in the range <code>[0, A.length]</code>.</li>
</ul>

## Solutions

<!-- tabs:start -->

### **Python3**

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
