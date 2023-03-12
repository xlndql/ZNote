# **剑指 Offer 27.** **二叉树的镜像**

[剑指 Offer 27. 二叉树的镜像 - 力扣（Leetcode）](https://leetcode.cn/problems/er-cha-shu-de-jing-xiang-lcof/description/)

## 功能

输入一个二叉树，返回该二叉树横向翻转后的结果。

## 具体分析

通过递归的方式将该二叉树的左右结点互换。

## 数据结构

无额外数据结构。

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.25 15:12
 */
public class Solution {
    public TreeNode mirrorTree(TreeNode root) {
        if (root == null) return null;
        TreeNode tmp = root.left;
        root.left = mirrorTree(root.right);
        root.right = mirrorTree(tmp);
        return root;
    }
}
```
