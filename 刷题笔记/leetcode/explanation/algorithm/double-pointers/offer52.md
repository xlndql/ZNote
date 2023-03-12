# 剑指 Offer 52. 两个链表的第一个公共节点

[剑指 Offer 52. 两个链表的第一个公共节点 - 力扣（Leetcode）](https://leetcode.cn/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/description/)

## 功能

给定两个链表，这两个链表有一部分可能是公用的，返回它们的第一个公共结点。

## 具体分析

通过两个指针指向两个链表的头位置，分别遍历完本链表再遍历另一个链表，当它们相同时则是第一个公共结点。

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.31 21:16
 */
public class Solution {
    ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode p1 = headA, p2 = headB;
        while (p1 != p2) {
            p1 = p1 != null ? p1.next : headB;
            p2 = p2 != null ? p2.next : headA;
        }
        return p1;
    }
}
```
