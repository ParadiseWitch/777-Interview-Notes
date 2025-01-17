# LCOF 67. 把字符串转换成整数

## 1. [问题](https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/)

写一个函数 StrToInt，实现把字符串转换成整数这个功能。不能使用 atoi 或者其他类似的库函数。

首先，该函数会根据需要丢弃无用的开头空格字符，直到寻找到第一个非空格的字符为止。

当我们寻找到的第一个非空字符为正或者负号时，则将该符号与之后面尽可能多的连续数字组合起来，作为该整数的正负号；假如第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成整数。

该字符串除了有效的整数部分之后也可能会存在多余的字符，这些字符可以被忽略，它们对于函数不应该造成影响。

注意：假如该字符串中的第一个非空格字符不是一个有效整数字符、字符串为空或字符串仅包含空白字符时，则你的函数不需要进行转换。

在任何情况下，若函数不能进行有效的转换时，请返回 0。

**说明：**

假设我们的环境只能存储 32 位大小的有符号整数，那么其数值范围为 \[−231, 231 − 1]。如果数值超过这个范围，请返回 INT_MAX (231 − 1) 或 INT_MIN (−231) 。

**示例 1:**

```
输入: "42"
输出: 42
```

**示例 2:**

```
输入: "   -42"
输出: -42
解释: 第一个非空白字符为 '-', 它是一个负号。
     我们尽可能将负号与后面所有连续出现的数字组合起来，最后得到 -42 。
```

**示例 3:**

```
输入: "4193 with words"
输出: 4193
解释: 转换截止于数字 '3' ，因为它的下一个字符不为数字。
```

**示例 4:**

```
输入: "words and 987"
输出: 0
解释: 第一个非空字符是 'w', 但它不是数字或正、负号。
     因此无法执行有效的转换。
```

**示例 5:**

```
输入: "-91283472332"
输出: -2147483648
解释: 数字 "-91283472332" 超过 32 位有符号整数范围。 
     因此返回 INT_MIN (−231) 。
```

## 2. 标签

* 数学
* 字符串

## 3. 解法

### 3.1 Java

```java
class Solution {
    public int strToInt(String str) {
        // 先将字符串转换为字符数组，删除首尾空格
        char[] c = str.trim().toCharArray();

        // 判空
        if (c.length == 0)
            return 0;

        // 最终结果
        int ans = 0;
        // 边界
        int boundary = Integer.MAX_VALUE / 10;

        // 字符开始的位置
        int i = 1;
        // 符号位
        int sign = 1;
        // 判断符号
        if(c[0] == '-') 
            sign = -1;
        else if(c[0] != '+') 
            i = 0; // 如果第一位不是正负号，那么数字开始的位置就是 0

        // 从第一个字符开始遍历到最后一个字符
        for(int j = i; j < c.length; j++) {
            // 如果发现不是数字就直接跳过
            if(c[j] < '0' || c[j] > '9') 
                break;
            // 如果此时的结果已经超过边界值，直接根据符号返回整数的最大值 or 最小值
            if(ans > boundary || ans == boundary && c[j] > '7') 
                return sign == 1 ? Integer.MAX_VALUE : Integer.MIN_VALUE;
            // 结果没有越界，继续累加数字
            ans = ans * 10 + (c[j] - '0');
        }
        // 返回带符号的结果
        return sign * ans;

    }
}
```

### 3.2 Kotlin

```kotlin
class Solution {
    fun strToInt(str: String): Int {
        // 先将字符串转换为字符数组，删除首尾空格
        val c = str.trim { it <= ' ' }.toCharArray()

        // 判空
        if (c.size == 0)
            return 0

        // 最终结果
        var ans = 0
        // 边界
        val boundary = Integer.MAX_VALUE / 10

        // 字符开始的位置
        var i = 1
        // 符号位
        var sign = 1
        // 判断符号
        if (c[0] == '-')
            sign = -1
        else if (c[0] != '+')
            i = 0 // 如果第一位不是正负号，那么数字开始的位置就是 0

        // 从第一个字符开始遍历到最后一个字符
        for (j in i until c.size) {
            // 如果发现不是数字就直接跳过
            if (c[j] < '0' || c[j] > '9')
                break
            // 如果此时的结果已经超过边界值，直接根据符号返回整数的最大值 or 最小值
            if (ans > boundary || ans == boundary && c[j] > '7')
                return if (sign == 1) Integer.MAX_VALUE else Integer.MIN_VALUE
            // 结果没有越界，继续累加数字
            ans = ans * 10 + (c[j] - '0')
        }
        // 返回带符号的结果
        return sign * ans

    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：其中 N 为字符串的长度，该题只需要线性遍历字符串。
* 空间复杂度 `O(N)` ：删除首尾空格后需建立新字符串，最差情况下占用 `O(N)` 额外空间。

> 不使用 `trim()` ，直接从头开始遍历字符串，可以将空间复杂度降低至 `O(1)`。

## 4. 参考

* [https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/](https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/)
* [https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/solution/mian-shi-ti-67-ba-zi-fu-chuan-zhuan-huan-cheng-z-4/](https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/solution/mian-shi-ti-67-ba-zi-fu-chuan-zhuan-huan-cheng-z-4/)
