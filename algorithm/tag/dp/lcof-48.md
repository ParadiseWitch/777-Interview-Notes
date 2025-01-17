# LCOF 48. 最长不含重复字符的子字符串

## 1. [问题](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)

请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

**示例 1:**

```
输入: "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**

```
输入: "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

**示例 3:**

```
输入: "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

提示：

* `s.length <= 40000`

## 2. 标签

* 哈希表
* 动态规划
* 双指针
* 滑动窗口

## 3. 解法 - 动态规划 哈希表

### 3.1 Java

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        // 判空
        if (s.length() == 0)
            return 0;

        // 状态转移方程
        // dp[i] 表示以字符 s[i] 结尾的「最长不重复子字符串」的长度
        int[] dp = new int[s.length()];

        // 使用哈希表统计「每个字符最后一次出现的位置」
        Map<Character, Integer> hashmap = new HashMap<>();

        // 最长不含重复字符的子字符串的长度
        int ans = 0;

        // i 为左边界，j 为右边界
        for (int j = 0; j < s.length(); j++) {
            // 从哈希表中获取到当前字符 s[j] 左边距离最近的相同字符 s[i]
            // 左边不存在相同的字符就给 i 赋值 -1
            int i = hashmap.getOrDefault(s.charAt(j), -1);

            // 遍历字符串的同时使用哈希表统计「每个字符最后一次出现的位置」
            hashmap.put(s.charAt(j), j);

            // 状态转移方程
            if (j!=0)
                dp[j] = dp[j - 1] < j - i ? dp[j - 1] + 1 : j - i;
            else
                dp[j] = 1;

            // 更新结果
            ans = Math.max(ans, dp[j]);

        }
        return ans;
    }
}

```

### 3.2 Kotlin

```kotlin
class Solution {
    fun lengthOfLongestSubstring(s: String): Int {
        // 判空
        if (s.length == 0)
            return 0

        // 状态转移方程
        // dp[i] 表示以字符 s[i] 结尾的「最长不重复子字符串」的长度
        val dp = IntArray(s.length)

        // 使用哈希表统计「每个字符最后一次出现的位置」
        val hashmap = mutableMapOf<Char, Int>()

        // 最长不含重复字符的子字符串的长度
        var ans = 0

        // i 为左边界，j 为右边界
        for (j in 0 until s.length) {
            // 从哈希表中获取到当前字符 s[j] 左边距离最近的相同字符 s[i]
            // 左边不存在相同的字符就给 i 赋值 -1
            val i = hashmap.getOrDefault(s[j], -1)

            // 遍历字符串的同时使用哈希表统计「每个字符最后一次出现的位置」
            hashmap[s[j]] = j

            // 状态转移方程
            if (j != 0)
                dp[j] = if (dp[j - 1] < j - i) dp[j - 1] + 1 else j - i
            else
                dp[j] = 1

            // 更新结果
            ans = Math.max(ans, dp[j])

        }
        return ans
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：其中 N 是字符串的长度，动态规划需要遍历字符串来计算 dp 数组。
* 空间复杂度 `O(1)` ：字符的 ASCII 码范围为 \[0, 127]，所以哈希表最多使用 `O(128) = O(1)` 大小的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)
* [https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/solution/mian-shi-ti-48-zui-chang-bu-han-zhong-fu-zi-fu-d-9/](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/solution/mian-shi-ti-48-zui-chang-bu-han-zhong-fu-zi-fu-d-9/)
