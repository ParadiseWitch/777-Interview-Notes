# 43. 1～n 整数中 1 出现的次数【找规律】

## 1. [问题](https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/)

输入一个整数 n ，求1～n这n个整数的十进制表示中1出现的次数。

例如，输入12，1～12这些整数中包含1 的数字有1、10、11和12，1一共出现了5次。

**示例 1：**

```
输入：n = 12
输出：5
```

**示例 2：**

```
输入：n = 13
输出：6
```

**限制：**

* `1 <= n < 2^31`

## 2. 标签

* 数学
* 找规律

## 3. 解法 - 找规律

> 好的，找规律题我放弃，本猪脑子想多久都是想不出的 🤯

### 3.1 Java

```java
class Solution {
    public int countDigitOne(int n) {
        // digit 是「位因子」
        int digit = 1;
        int ans = 0;

        // 当前位
        int cur = n % 10;
        // cur之前的所有高位
        int high = n / 10;
        // cur之后会的所有低位
        int low = 0;

        // 从最低位一直循环遍历到最高位
        while (high != 0 || cur != 0) {
            // cur为0时，结果只由高位决定，为什么呢，看k佬，找规律太难了我不会555
            if (cur == 0)
                ans += high * digit;
            // cur为1时，结果由高低位一起决定
            else if (cur == 1)
                ans += high * digit + low + 1;
            // cur为其他数字时，结果只由高位决定
            else 
                ans += (high + 1) * digit;

            // 更新cur hight low
            low += cur * digit;
            cur = high % 10;
            high /= 10;
            digit *= 10;
        }
        return ans;
    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun countDigitOne(n: Int): Int {
        // digit 是「位因子」
        var digit = 1
        var ans = 0

        // 当前位
        var cur = n % 10
        // cur之前的所有高位
        var high = n / 10
        // cur之后会的所有低位
        var low = 0

        // 从最低位一直循环遍历到最高位
        while (high != 0 || cur != 0) {
            // cur为0时，结果只由高位决定，为什么呢，看k佬，找规律太难了我不会555
            if (cur == 0)
                ans += high * digit
            else if (cur == 1)
                ans += high * digit + low + 1
            else
                ans += (high + 1) * digit// cur为其他数字时，结果只由高位决定
            // cur为1时，结果由高低位一起决定

            // 更新cur hight low
            low += cur * digit
            cur = high % 10
            high /= 10
            digit *= 10
        }
        return ans
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(logn)` ：循环内的计算操作使用 `O(1)` 时间，总共循环了$$O(log_{10}n)$$次 ，因此循环总共使用了 `O(logn)` 的时间。
* 空间复杂度 `O(1)` ：变量只使用了常数大小的额外存储空间。

## 4. 参考

* [https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/](https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/)
* [https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/solution/mian-shi-ti-43-1n-zheng-shu-zhong-1-chu-xian-de-2/](https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/solution/mian-shi-ti-43-1n-zheng-shu-zhong-1-chu-xian-de-2/)
