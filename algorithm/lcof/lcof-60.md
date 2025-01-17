# \*60. n个骰子的点数【DP】

## 1. [问题](https://leetcode-cn.com/problems/nge-tou-zi-de-dian-shu-lcof/)

把 n 个骰子扔在地上，所有骰子朝上一面的点数之和为 s。输入 n，打印出 s 的所有可能的值出现的概率。

你需要用一个浮点数数组返回答案，其中第 i 个元素代表这 n 个骰子所能掷出的点数集合中第 i 小的那个的概率。

**示例 1:**

```
输入: 1
输出: [0.16667,0.16667,0.16667,0.16667,0.16667,0.16667]
```

**示例 2:**

```
输入: 2
输出: [0.02778,0.05556,0.08333,0.11111,0.13889,0.16667,0.13889,0.11111,0.08333,0.05556,0.02778]
```

**限制：**

* `1 <= n <= 11`

## 2. 标签

* 动态规划

## 3. 解法 - 动态规划

> 不太想得到啊OTZ

### 3.1 Java

```java
// ref: https://leetcode-cn.com/problems/nge-tou-zi-de-dian-shu-lcof/solution/nge-tou-zi-de-dian-shu-dong-tai-gui-hua-ji-qi-yo-3/
class Solution {
    public double[] dicesProbability(int n) {
        /**
         * 如果使用递归来搜索解空间的话，会导致超时
         * 因为在递归过程中存在大量的重复子结构
         * 这会导致大量的重复计算
         * 
         * 故选用动态规划来解决问题
         */

         // 状态转移方程
         // dp[i][j] 表示投掷完 i 枚骰子后，点数之和 j 的出现次数
         int[][] dp = new int[n + 1][6 * n + 1];

         // 边界处理
         for (int i=1;i<=6;i++) {
             // 投掷完 1 枚骰子后，可能的点数之和 i 为 1,2,3,4,5,6
             // 每个点数之和可能出现的次数都为 1
             dp[1][i] = 1; 
         }

         // 统计点数之和中，所有可能的值出现的次数
         // 
         for (int i=2;i<=n;i++) {
             for (int j=i;j<=6*i;j++) {
                 for (int k=1;k<=6 && k<=j;k++) {
                     /**
                      * 投掷完 i 枚骰子后，点数之和 j 可能出现的次数
                      * 可以由投掷完 n - 1 枚骰子后，对应的点数之和：
                      * j-1,j-2,j-3,...,j-6 可能出现的次数之和
                      * 转化而来
                      *
                      * 这里用 k 来表示第 i 枚骰子会出现的六个点数
                      */
                     dp[i][j] += dp[i-1][j-k];
                 }
             }
         }

         // 点数之和中，所有可能的值出现的概率
         double[] ans = new double[6 * n - n + 1];

         // 计算概率 
         for (int i=n;i<=6*n;i++) {
             ans[i-n] = (double) dp[n][i] / Math.pow(6, n);
         }

         return ans;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun dicesProbability(n: Int): DoubleArray {
        /**
         * 如果使用递归来搜索解空间的话，会导致超时
         * 因为在递归过程中存在大量的重复子结构
         * 这会导致大量的重复计算
         *
         * 故选用动态规划来解决问题
         */

        // 状态转移方程
        // dp[i][j] 表示投掷完 i 枚骰子后，点数之和 j 的出现次数
        val dp = Array(n + 1) { IntArray(6 * n + 1) }

        // 边界处理
        for (i in 1..6) {
            // 投掷完 1 枚骰子后，可能的点数之和 i 为 1,2,3,4,5,6
            // 每个点数之和可能出现的次数都为 1
            dp[1][i] = 1
        }

        // 统计点数之和中，所有可能的值出现的次数
        //
        for (i in 2..n) {
            for (j in i..6 * i) {
                var k = 1
                while (k <= 6 && k <= j) {
                    /**
                     * 投掷完 i 枚骰子后，点数之和 j 可能出现的次数
                     * 可以由投掷完 n - 1 枚骰子后，对应的点数之和：
                     * j-1,j-2,j-3,...,j-6 可能出现的次数之和
                     * 转化而来
                     *
                     * 这里用 k 来表示第 i 枚骰子会出现的六个点数
                     */
                    dp[i][j] += dp[i - 1][j - k]
                    k++
                }
            }
        }

        // 点数之和中，所有可能的值出现的概率
        val ans = DoubleArray(6 * n - n + 1)

        // 计算概率
        for (i in n..6 * n) {
            ans[i - n] = dp[n][i].toDouble() / Math.pow(6.0, n.toDouble())
        }

        return ans
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N^3)` ：三重循环。
* 空间复杂度 `O(N)` ：dp 数组占用了 `O(N)` 的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/nge-tou-zi-de-dian-shu-lcof/](https://leetcode-cn.com/problems/nge-tou-zi-de-dian-shu-lcof/)
* [https://leetcode-cn.com/problems/nge-tou-zi-de-dian-shu-lcof/solution/nge-tou-zi-de-dian-shu-dong-tai-gui-hua-ji-qi-yo-3/](https://leetcode-cn.com/problems/nge-tou-zi-de-dian-shu-lcof/solution/nge-tou-zi-de-dian-shu-dong-tai-gui-hua-ji-qi-yo-3/)
