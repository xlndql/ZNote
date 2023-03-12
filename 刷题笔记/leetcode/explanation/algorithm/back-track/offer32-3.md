# **剑指 Offer 32 - III.** **从上到下打印二叉树 III**

[剑指 Offer 32 - III. 从上到下打印二叉树 III - 力扣（Leetcode）](https://leetcode.cn/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/description/)

## 功能

将二叉树的奇数层的值按从左到右的顺序，偶数层按从右到左的顺序存储到一个二维数组中，每一层存入数组的一行中。

## 具体分析

同第二题，只需要在每次存入结果数组前判断是否为偶数层，再逆序数组即可。

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
            if (res.size() % 2 == 1) {
                for (int i = 0, j = vals.size() - 1; i < j; i++, j--) {
                    int tmp = vals.get(i);
                    vals.set(i, vals.get(j));
                    vals.set(j, tmp);
                }
            }
            res.add(vals);
        }
        return res;
    }
}
```
