# 55 - II. 平衡二叉树【DFS】

## 1. [问题](https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/)

输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

**示例 1：**

给定二叉树 `[3,9,20,null,null,15,7]`

```
    3
   / \
  9  20
    /  \
   15   7
```

返回 `true` 。

**示例 2：**

给定二叉树 `[1,2,2,3,3,null,null,4,4]`

```
       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
```

返回 `false` 。

**限制：**

* `1 <= 树的结点个数 <= 10000`

## 2. 标签

* 树
* DFS

## 3. 解法 - DFS

> 该解法为自顶向下，还有一种解法是自底向上剪枝，之后可以看一下。#TODO

### 3.1 Java

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public boolean isBalanced(TreeNode root) {
        int height = tree_height(root);
        // 若返回值为 -1 说明不是平衡树，若不为 -1 说明是平衡树。
        return height != -1;
    }

    // 判断 root 是否为平衡树，若返回值为 -1 说明不是平衡树，若不为 -1 说明是平衡树。
    public int tree_height(TreeNode root) {
        // 递归出口，根为空返回 0
        if (root == null)
            return 0;
        // 求左子树是否为平衡二叉树
        int left_height = tree_height(root.left);
        // 求右子树是否为平衡二叉树
        int right_height = tree_height(root.right);
        /**
         * 只要以下三个条件成立一个就说明当前树不是平衡二叉树
         *  1. 左子树不是平衡二叉树
         *  2. 右子树不是平衡二叉树
         *  3. 左右子树的高度差大于 1
         */
        if (left_height == -1 || right_height == -1 || Math.abs(left_height - right_height) > 1)
            return -1;
        // 如果当前树是平衡二叉树，那么就直接返回它的高度：左右子树高度的较大值 + 1 （别忘记加上 1 ）
        return Math.max(left_height, right_height) + 1;
    }
}
```

### 3.2 Kotlin

```kotlin
/**
 * Example:
 * var ti = TreeNode(5)
 * var v = ti.`val`
 * Definition for a binary tree node.
 * class TreeNode(var `val`: Int) {
 *     var left: TreeNode? = null
 *     var right: TreeNode? = null
 * }
 */
class Solution {
    fun isBalanced(root: TreeNode?): Boolean {
        val height = tree_height(root)
        // 若返回值为 -1 说明不是平衡树，若不为 -1 说明是平衡树。
        return height != -1
    }

    // 判断 root 是否为平衡树，若返回值为 -1 说明不是平衡树，若不为 -1 说明是平衡树。
    fun tree_height(root: TreeNode?): Int {
        // 递归出口，根为空返回 0
        if (root == null)
            return 0
        // 求左子树是否为平衡二叉树
        val left_height = tree_height(root.left)
        // 求右子树是否为平衡二叉树
        val right_height = tree_height(root.right)
        /**
         * 只要以下三个条件成立一个就说明当前树不是平衡二叉树
         *  1. 左子树不是平衡二叉树
         *  2. 右子树不是平衡二叉树
         *  3. 左右子树的高度差大于 1
         * 如果当前树是平衡二叉树，那么就直接返回它的高度：左右子树高度的较大值 + 1 （别忘记加上 1 ）
         */
        return if (left_height == -1 || right_height == -1 || Math.abs(left_height - right_height) > 1) -1 else Math.max(
            left_height,
            right_height
        ) + 1
        // 
    }
}
```

### 3.3 复杂度分析

* 时间复杂度 `O(N)` ：N 是树的结点数量，最差情况下，当树退化为链表时，需要递归遍历树的所有结点。
* 空间复杂度 `O(N)` ：最差情况下，当树退化为链表时，系统递归时需要占用 `O(N)` 的栈空间。

## 4. 参考

* [https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/](https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/)
* [https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/solution/mian-shi-ti-55-ii-ping-heng-er-cha-shu-cong-di-zhi/](https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/solution/mian-shi-ti-55-ii-ping-heng-er-cha-shu-cong-di-zhi/)

