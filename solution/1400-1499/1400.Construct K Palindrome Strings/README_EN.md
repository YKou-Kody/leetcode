# [1400. Construct K Palindrome Strings](https://leetcode.com/problems/construct-k-palindrome-strings)

[中文文档](/solution/1400-1499/1400.Construct%20K%20Palindrome%20Strings/README.md)

## Description

<p>Given a string <code>s</code> and an integer <code>k</code>. You should construct <code>k</code> non-empty <strong>palindrome</strong> strings using <strong>all the characters</strong> in <code>s</code>.</p>

<p>Return <em><strong>True</strong></em> if you can use all the characters in <code>s</code> to construct <code>k</code> palindrome strings or <em><strong>False</strong></em> otherwise.</p>

<p>&nbsp;</p>

<p><strong>Example 1:</strong></p>

<pre>

<strong>Input:</strong> s = &quot;annabelle&quot;, k = 2

<strong>Output:</strong> true

<strong>Explanation:</strong> You can construct two palindromes using all characters in s.

Some possible constructions &quot;anna&quot; + &quot;elble&quot;, &quot;anbna&quot; + &quot;elle&quot;, &quot;anellena&quot; + &quot;b&quot;

</pre>

<p><strong>Example 2:</strong></p>

<pre>

<strong>Input:</strong> s = &quot;leetcode&quot;, k = 3

<strong>Output:</strong> false

<strong>Explanation:</strong> It is impossible to construct 3 palindromes using all the characters of s.

</pre>

<p><strong>Example 3:</strong></p>

<pre>

<strong>Input:</strong> s = &quot;true&quot;, k = 4

<strong>Output:</strong> true

<strong>Explanation:</strong> The only possible solution is to put each character in a separate string.

</pre>

<p><strong>Example 4:</strong></p>

<pre>

<strong>Input:</strong> s = &quot;yzyzyzyzyzyzyzy&quot;, k = 2

<strong>Output:</strong> true

<strong>Explanation:</strong> Simply you can put all z&#39;s in one string and all y&#39;s in the other string. Both strings will be palindrome.

</pre>

<p><strong>Example 5:</strong></p>

<pre>

<strong>Input:</strong> s = &quot;cr&quot;, k = 7

<strong>Output:</strong> false

<strong>Explanation:</strong> We don&#39;t have enough characters in s to construct 7 palindromes.

</pre>

<p>&nbsp;</p>

<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10^5</code></li>
	<li>All characters in <code>s</code> are lower-case English letters.</li>
	<li><code>1 &lt;= k &lt;= 10^5</code></li>
</ul>

## Solutions

<!-- tabs:start -->

### **Python3**

```python
class Solution:
    def canConstruct(self, s: str, k: int) -> bool:
        if len(s) < k:
            return False
        counter = Counter(s)
        cnt = sum(1 for n in counter.values() if n % 2 == 1)
        return cnt <= k
```

### **Java**

```java
class Solution {
    public boolean canConstruct(String s, int k) {
        if (s.length() < k) {
            return false;
        }
        int[] counter = new int[26];
        for (char c : s.toCharArray()) {
            ++counter[c - 'a'];
        }
        int cnt = 0;
        for (int v : counter) {
            if (v % 2 == 1) {
                ++cnt;
            }
        }
        return cnt <= k;
    }
}
```

### **C++**

```cpp
class Solution {
public:
    bool canConstruct(string s, int k) {
        if (s.size() < k) return 0;
        vector<int> counter(26);
        for (char c : s) ++counter[c - 'a'];
        int cnt = 0;
        for (int v : counter)
            if (v % 2)
                ++cnt;
        return cnt <= k;
    }
};
```

### **Go**

```go
func canConstruct(s string, k int) bool {
	if len(s) < k {
		return false
	}
	counter := make([]int, 26)
	for _, c := range s {
		counter[c-'a']++
	}
	cnt := 0
	for _, v := range counter {
		if v%2 == 1 {
			cnt++
		}
	}
	return cnt <= k
}
```

### **...**

```

```

<!-- tabs:end -->
