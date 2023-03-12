# 剑指 Offer 22. 链表中倒数第k个节点

[剑指 Offer 22. 链表中倒数第k个节点 - 力扣（Leetcode）](https://leetcode.cn/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/description/)

## 功能

给定一个链表和一个数 k，返回链表中倒数第 k 个结点。

## 具体分析

通过两个指向链表头的指针 p1 和 p2，p1 先向前走 k 步，再让 p1 和 p2 同时向前走，当 p1 走到链表尾部时 p2 位于链表倒数第 k 个结点，返回即可。

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.31 21:06
 */
public class Solution {
    public ListNode getKthFromEnd(ListNode head, int k) {
        ListNode p1 = head, p2 = head;
        while (k-- > 0) {
            p2 = p2.next;
        }
        while (p2 != null) {
            p1 = p1.next;
            p2 = p2.next;
        }
        return p1;
    }
}
```
