# 42. 连续子数组的最大和【DP】

## 1. [问题](https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

**示例1:**

```
输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。
```

**提示：**

* `1 <= arr.length <= 10^5`
* `-100 <= arr[i] <= 100`

## 2. 标签

* 分治
* 动态规划

## 3. 解法 - 动态规划

### 3.1 Java

```java
class Solution {
    public int maxSubArray(int[] nums) {
        // 状态数组
        // dp[i] 表示以元素 nums[i] 结尾的连续子数组的最大和
        int[] dp = new int[nums.length];

        // 边界值
        dp[0] = nums[0];

        // 最大和
        int max = dp[0];

        // 状态转移
        for (int i = 1; i < nums.length; i++) {
            if (dp[i - 1] <= 0) {
                // 此时说明 dp[i-1] 产生负贡献，还没有 nums[i]大，给 dp[i] 赋值为 nums[i] 即可
                dp[i] = nums[i];
            } else {
                // 此时说明 dp[i-1] 产生正贡献，累加上 nums[i] 后赋值给 dp[i] 即可
                dp[i] = dp[i - 1] + nums[i];
            }
            // 若 dp[i] 大于 max，更新最大值即可
            if (dp[i] > max)
                max = dp[i];
        }
        // 返回最大值
        return max;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun maxSubArray(nums: IntArray): Int {
        // 状态数组
        // dp[i] 表示以元素 nums[i] 结尾的连续子数组的最大和
        val dp = IntArray(nums.size)

        // 边界值
        dp[0] = nums[0]

        // 最大和
        var max = dp[0]

        // 状态转移
        for (i in 1 until nums.size) {
            if (dp[i - 1] <= 0) {
                // 此时说明 dp[i-1] 产生负贡献，还没有 nums[i]大，给 dp[i] 赋值为 nums[i] 即可
                dp[i] = nums[i]
            } else {
                // 此时说明 dp[i-1] 产生正贡献，累加上 nums[i] 后赋值给 dp[i] 即可
                dp[i] = dp[i - 1] + nums[i]
            }
            // 若 dp[i] 大于 max，更新最大值即可
            if (dp[i] > max)
                max = dp[i]
        }
        // 返回最大值
        return max
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：线性遍历数组需要 `O(N)` 时间。
* 空间复杂度 `O(N)` ：状态数组 dp 占用了 `O(N)` 空间。

### 3.4 优化

由于 `dp[i]` 只和 `dp[i-1]` 以及 `nums[i]` 有关，所以可以直接把 `nums` 数组当作状态数组，即在 `nums` 上直接修改即可，这样可以使得空间复杂度从 `O(N)` 降到 `O(1)` 。

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int maxValue = nums[0];
        for (int i = 1; i < nums.length; i++) {
            // 注意这里是 += 不是 =
            nums[i] += Math.max(nums[i - 1], 0);
            maxValue = Math.max(nums[i], maxValue);
        }
        return maxValue;
    }
}
```

## 4. 参考

* [https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/](https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)
* [https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/solution/mian-shi-ti-42-lian-xu-zi-shu-zu-de-zui-da-he-do-2/](https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/solution/mian-shi-ti-42-lian-xu-zi-shu-zu-de-zui-da-he-do-2/)
