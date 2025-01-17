# LCOF 56 - I. 数组中数字出现的次数

## 1. [问题](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/)

一个整型数组 `nums` 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。

**示例 1：**

```
输入：nums = [4,1,4,6]
输出：[1,6] 或 [6,1]
```

**示例 2：**

```
输入：nums = [1,2,10,4,1,4,3,3]
输出：[2,10] 或 [10,2]
```

**限制：**

* `2 <= nums.length <= 10000`

## 2. 标签

* 位运算

## 3. 解法 - 位运算

### 3.1 Java

```java
class Solution {
    public int[] singleNumbers(int[] nums) {
        // ^ 异或
        // A ^ A = 0
        // 0 ^ B = B

        // 先对所有数字进行一次异或
        // 可以得到两个只出现一次的数字的异或值
        // 假设两个数字为 resA 和 resB，那么 allXOR = resA ^ resB
        int allXOR = 0;
        for (int num : nums)
            allXOR ^= num;

        // 在 allXOR 中随便找出一个二进制中值为 1 的位
        // 该位为 1 说明 resA 和 resB 在这一位上对应的值不同
        // 该位为 0 说明 resA 和 resB 在这一位上对应的值相同
        // 而我们想找的就是不同的，所以找值为 1 的位
        int div = 1;
        while ((div & allXOR) == 0)
            div <<= 1; // 左移一位

        // 两个只出现一次的数字
        int resA = 0;
        int resB = 0;
        // 根据找到的 div 对所有数字进行分组
        // 在每个组内进行异或操作，分别可以得到只出现一次的数字：resA resB
        for (int num : nums)
            if ((div & num) == 0)
                resA ^= num;
            else
                resB ^= num;
        // 返回两个数字即可
        return new int[] { resA, resB };
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun singleNumbers(nums: IntArray): IntArray {
        // ^ 异或
        // A ^ A = 0
        // 0 ^ B = B

        // 先对所有数字进行一次异或
        // 可以得到两个只出现一次的数字的异或值
        // 假设两个数字为 resA 和 resB，那么 allXOR = resA ^ resB
        var allXOR = 0
        for (num in nums)
            allXOR = allXOR xor num

        // 在 allXOR 中随便找出一个二进制中值为 1 的位
        // 该位为 1 说明 resA 和 resB 在这一位上对应的值不同
        // 该位为 0 说明 resA 和 resB 在这一位上对应的值相同
        // 而我们想找的就是不同的，所以找值为 1 的位
        var div = 1
        while (div and allXOR == 0)
            div = div shl 1 // 左移一位

        // 两个只出现一次的数字
        var resA = 0
        var resB = 0
        // 根据找到的 div 对所有数字进行分组
        // 在每个组内进行异或操作，分别可以得到只出现一次的数字：resA resB
        for (num in nums)
            if (div and num == 0)
                resA = resA xor num
            else
                resB = resB xor num
        // 返回两个数字即可
        return intArrayOf(resA, resB)
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(n)` ：总共只遍历了两次数组。
* 空间复杂度 `O(1)` ：变量只占用了常数大小的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/)
* [https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/solution/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-by-leetcode/](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/solution/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-by-leetcode/)
