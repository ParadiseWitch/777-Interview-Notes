# LCOF 49. 丑数

## 1. [问题](https://leetcode-cn.com/problems/chou-shu-lcof/)

我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。

**示例:**

```
输入: n = 10
输出: 12
解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。
```

**说明: ** 

1. `1` 是丑数。
2. `n` **不超过**1690。

## 2. 标签

* 数学
* 动态规划

## 3. 解法

### 3.1 Java

```java
class Solution {
    public int nthUglyNumber(int n) {
        // 丑数可以递推：丑数 = 某较小丑数 * 某因子（ 2, 3 ,5 三个其中之一）
        int index2 = 0;
        int index3 = 0;
        int index5 = 0;

        // 状态转移方程
        // dp[i] 代表第 i + 1 个丑数
        int[] dp = new int[n];

        // 边界值
        // 第一个丑数是 1
        dp[0] = 1;

        // 状态转移方程
        for (int i = 1; i < n; i++) {
            int factor2 = dp[index2] * 2;
            int factor3 = dp[index3] * 3;
            int factor5 = dp[index5] * 5;

            // 当前第 i + 1 个丑数就取由之前的丑数递推出来的丑数的最小值
            dp[i] = Math.min(Math.min(factor2, factor3), factor5);

            // 取了哪个因子递推出来的丑数，就将哪个因子的索引自增
            if (dp[i] == factor2)
                index2++;
            if (dp[i] == factor3)
                index3++;
            if (dp[i] == factor5)
                index5++;
        }
        // 返回第 n 个丑数
        return dp[n - 1];
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun nthUglyNumber(n: Int): Int {
        // 丑数可以递推：丑数 = 某较小丑数 * 某因子（ 2, 3 ,5 三个其中之一）
        var index2 = 0
        var index3 = 0
        var index5 = 0

        // 状态转移方程
        // dp[i] 代表第 i + 1 个丑数
        val dp = IntArray(n)

        // 边界值
        // 第一个丑数是 1
        dp[0] = 1

        // 状态转移方程
        for (i in 1 until n) {
            val factor2 = dp[index2] * 2
            val factor3 = dp[index3] * 3
            val factor5 = dp[index5] * 5

            // 当前第 i + 1 个丑数就取由之前的丑数递推出来的丑数的最小值
            dp[i] = Math.min(Math.min(factor2, factor3), factor5)

            // 取了哪个因子递推出来的丑数，就将哪个因子的索引自增
            if (dp[i] == factor2)
                index2++
            if (dp[i] == factor3)
                index3++
            if (dp[i] == factor5)
                index5++
        }
        // 返回第 n 个丑数
        return dp[n - 1]
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(n)` ：动态规划需要遍历计算 dp 数组。
* 空间复杂度 `O(n)` ：dp 数组占用 `O(n)` 大小的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/chou-shu-lcof/](https://leetcode-cn.com/problems/chou-shu-lcof/)
* [https://leetcode-cn.com/problems/chou-shu-lcof/solution/mian-shi-ti-49-chou-shu-dong-tai-gui-hua-qing-xi-t/](https://leetcode-cn.com/problems/chou-shu-lcof/solution/mian-shi-ti-49-chou-shu-dong-tai-gui-hua-qing-xi-t/)
