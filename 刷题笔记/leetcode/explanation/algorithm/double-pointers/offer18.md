# 剑指 Offer 18. 删除链表的节点

[剑指 Offer 18. 删除链表的节点 - 力扣（Leetcode）](https://leetcode.cn/problems/shan-chu-lian-biao-de-jie-dian-lcof/description/)

## 功能

给定链表某结点的值，删除该结点。

## 具体分析

通过两个指针 p1 p2 同时记录前后两个链表结点，当前一个结点获取到待删除的结点时将后一个结点的 next 设为前一个结点的 next，将待删除结点隔开。

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.31 21:01
 */
public class Solution {
    public ListNode deleteNode(ListNode head, int val) {
        if (head.val == val) return head.next;
        ListNode p1 = head, p2 = head;
        while (p1 != null) {
            p1 = p1.next;
            if (p1.val == val) {
                p2.next = p1.next;
                break;
            }
            p2 = p2.next;
        }
        return head;
    }
}
```
