# 剑指 Offer 32 - II. 从上到下打印二叉树 II

[剑指 Offer 32 - II. 从上到下打印二叉树 II - 力扣（Leetcode）](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/description/)

## 功能

将二叉树每一层的值按从左到右的顺序存储到一个二维数组中，每一层存入数组的一行中。

## 具体分析

通过层序遍历的方式，通过一个队列数据结构 Queue 将根结点 root 存入队列中，每次取出队列中的 root，获取对应的值 val 存入结果数组中，再将该结点的左子节点和右子节点按顺序存入队列中，每次存入新结点前记录当前队列的大小作为这一层结点的数目，再将该数目的结点从队列中弹出记录对应的 val 存入新数组中，直到队列中不存在结点为止。

## 数据结构

通过一个队列数据结构按顺序存储所有结点。

```java
Queue<TreeNode> queue = new LinkedList<>();
```

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.24 18:37
 */
public class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        Queue<TreeNode> queue = new LinkedList<>();
        if (root != null) queue.add(root);
        List<List<Integer>> res = new ArrayList<>();
        while (!queue.isEmpty()) {
            List<Integer> vals = new ArrayList<>();
            int len = queue.size();
            while (len-- > 0) {
                TreeNode node = queue.poll();
                vals.add(node.val);
                if (node.left != null) queue.add(node.left);
                if (node.right != null) queue.add(node.right);
            }
            res.add(vals);
        }
        return res;
    }
}
```
