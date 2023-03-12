# 剑指 Offer 32 - I. 从上到下打印二叉树

[剑指 Offer 32 - I. 从上到下打印二叉树 - 力扣（Leetcode）](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/description/)

## 功能

将二叉树每一层的值按从左到右的顺序存储到一个数组中并返回。

结点：

```java
public class TreeNode {
    public int val;
    public TreeNode left;
    public TreeNode right;

    TreeNode(int x) {
        val = x;
    }
}
```

## 具体分析

通过层序遍历的方式，通过一个队列数据结构 Queue 将根结点 root 存入队列中，每次取出队列中的 root，获取对应的值 val 存入结果数组中，再将该结点的左子节点和右子节点按顺序存入队列中，直到队列中不存在结点为止。

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
 * @Create 2023.01.24 16:59
 */
public class Solution {
    public int[] levelOrder(TreeNode root) {
        if (root == null) return new int[0];
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        ArrayList<Integer> vals = new ArrayList<>();
        while (!queue.isEmpty()) {
            TreeNode node = queue.poll();
            vals.add(node.val);
            if (node.left != null) queue.add(node.left);
            if (node.right != null) queue.add(node.right);
        }
        int[] res = new int[vals.size()];
        for (int i = 0; i < res.length; i++) {
            res[i] = vals.get(i);
        }
        return res;
    }
}
```
