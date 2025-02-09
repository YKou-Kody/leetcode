# [1031. Maximum Sum of Two Non-Overlapping Subarrays](https://leetcode.com/problems/maximum-sum-of-two-non-overlapping-subarrays)

[中文文档](/solution/1000-1099/1031.Maximum%20Sum%20of%20Two%20Non-Overlapping%20Subarrays/README.md)

## Description

<p>Given an array <code>A</code> of non-negative integers, return the maximum sum of elements in two non-overlapping (contiguous) subarrays, which have lengths&nbsp;<code>L</code> and <code>M</code>.&nbsp; (For clarification, the <code>L</code>-length subarray could occur before or after the <code>M</code>-length subarray.)</p>

<p>Formally,&nbsp;return the largest <code>V</code> for which&nbsp;<code>V = (A[i] + A[i+1] + ... + A[i+L-1]) + (A[j] + A[j+1] + ... + A[j+M-1])</code> and either:</p>

<ul>
	<li><code>0 &lt;= i &lt; i + L - 1 &lt; j &lt; j + M - 1 &lt; A.length</code>, <strong>or</strong></li>
	<li><code>0 &lt;= j &lt; j + M - 1 &lt; i &lt; i + L - 1 &lt; A.length</code>.</li>
</ul>

<p>&nbsp;</p>

<ol>

</ol>

<div>

<p><strong>Example 1:</strong></p>

<pre>

<strong>Input: </strong>A = <span id="example-input-1-1">[0,6,5,2,2,5,1,9,4]</span>, L = <span id="example-input-1-2">1</span>, M = <span id="example-input-1-3">2</span>

<strong>Output: </strong><span id="example-output-1">20

<strong>Explanation:</strong> One choice of subarrays is [9] with length 1, and [6,5] with length 2.</span>

</pre>

<div>

<p><strong>Example 2:</strong></p>

<pre>

<strong>Input: </strong>A = <span id="example-input-2-1">[3,8,1,3,2,1,8,9,0]</span>, L = <span id="example-input-2-2">3</span>, M = <span id="example-input-2-3">2</span>

<strong>Output: </strong><span id="example-output-2">29

</span><span id="example-output-1"><strong>Explanation:</strong> One choice of subarrays is</span><span> [3,8,1] with length 3, and [8,9] with length 2.</span>

</pre>

<div>

<p><strong>Example 3:</strong></p>

<pre>

<strong>Input: </strong>A = <span id="example-input-3-1">[2,1,5,6,0,9,5,0,3,8]</span>, L = <span id="example-input-3-2">4</span>, M = <span id="example-input-3-3">3</span>

<strong>Output: </strong><span id="example-output-3">31

</span><span id="example-output-1"><strong>Explanation:</strong> One choice of subarrays is</span><span> [5,6,0,9] with length 4, and [3,8] with length 3.</span>

</pre>

<p>&nbsp;</p>

<p><strong>Note:</strong></p>

<ol>
	<li><code>L &gt;= 1</code></li>
	<li><code>M &gt;= 1</code></li>
	<li><code>L + M &lt;= A.length &lt;= 1000</code></li>
	<li><code>0 &lt;= A[i] &lt;= 1000</code></li>
</ol>

</div>

</div>

</div>

## Solutions

<!-- tabs:start -->

### **Python3**

```python
class Solution:
    def maxSumTwoNoOverlap(self, nums: List[int], firstLen: int, secondLen: int) -> int:
        n = len(nums)
        s = [0] * (n + 1)
        for i in range(1, n + 1):
            s[i] = s[i - 1] + nums[i - 1]
        ans1, ans2, fm, sm = 0, 0, 0, 0
        for i in range(n - firstLen - secondLen + 1):
            fm = max(fm, s[i + firstLen] - s[i])
            ans1 = max(fm + s[i + firstLen + secondLen] - s[i + firstLen], ans1)
        for i in range(n - firstLen - secondLen + 1):
            sm = max(sm, s[i + secondLen] - s[i])
            ans2 = max(sm + s[i + firstLen + secondLen] - s[i + secondLen], ans2)
        return max(ans1, ans2)
```

### **Java**

```java
class Solution {
    public int maxSumTwoNoOverlap(int[] nums, int firstLen, int secondLen) {
        int n = nums.length;
        int[] s = new int[n + 1];
        for (int i = 1; i <= n; i++) {
            s[i] = s[i - 1] + nums[i - 1];
        }
        int ans1 = 0, ans2 = 0, fm = 0, sm = 0;
        for (int i = 0; i < n - firstLen - secondLen + 1; i++) {
            fm = Math.max(s[i + firstLen] - s[i], fm);
            ans1 = Math.max(fm + s[i + firstLen + secondLen] - s[i + firstLen], ans1);
        }
        for (int i = 0; i < n - firstLen - secondLen + 1; i++) {
            sm = Math.max(s[i + secondLen] - s[i], sm);
            ans2 = Math.max(sm + s[i + firstLen + secondLen] - s[i + secondLen], ans2);
        }
        return Math.max(ans1, ans2);
    }
}
```

### **...**

```

```

<!-- tabs:end -->
