# **剑指 Offer 26.** **树的子结构**

[剑指 Offer 26. 树的子结构 - 力扣（Leetcode）](https://leetcode.cn/problems/shu-de-zi-jie-gou-lcof/description/)

## 功能

给定两棵二叉树 A 和 B，判断 B 是否是 A 的子结构。

## 具体分析

遍历 A 中的每一个结点，判断以该结点为根结点的情况下是否包含子结构 B。

通过回溯的方式判断 A 和 B 中的每一个结点的值是否相同。

## 数据结构

无额外数据结构。

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.25 14:31
 */
public class Solution {
    public boolean isSubStructure(TreeNode A, TreeNode B) {
        return (A != null && B != null) && (isSubStructure(A.left, B) || isSubStructure(A.right, B) || recur(A, B));
    }

    private boolean recur(TreeNode A, TreeNode B) {
        if (B == null) return true;
        if (A == null || A.val != B.val) return false;
        return recur(A.left, B.left) && recur(A.right, B.right);
    }
}
```
