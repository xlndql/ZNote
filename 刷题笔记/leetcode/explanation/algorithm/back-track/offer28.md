# 剑指 Offer 28. 对称的二叉树

[剑指 Offer 28. 对称的二叉树 - 力扣（Leetcode）](https://leetcode.cn/problems/dui-cheng-de-er-cha-shu-lcof/description/)

## 功能

判断一个二叉树是不是对称的。

## 具体分析

通过将根结点的左右子结点分开进行判断。

## 数据结构

无额外数据结构。

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.25 15:59
 */
public class Solution {
    public boolean isSymmetric(TreeNode root) {
        return root == null || recur(root.left, root.right);
    }

    private boolean recur(TreeNode l, TreeNode r) {
        if (l == null && r == null) return true;
        if (l == null || r == null || l.val != r.val) return false;
        return recur(l.left, r.right) && recur(l.right, r.left);
    }
}
```
