# 剑指 Offer 25. 合并两个排序的链表

[剑指 Offer 25. 合并两个排序的链表 - 力扣（Leetcode）](https://leetcode.cn/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/solutions/)

## 功能

合并两个有序的链表。

## 具体分析

通过两个指针分别指向两个链表，每次获取当前两个指针指向的值的较小者存入新链表，再将较小者的指针向前走一步，直到其中一个指针走到链表结尾，再将另一个指针指向的剩余链表全部存入新链表结尾处。

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.31 21:08
 */
public class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode res = new ListNode(-1);
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                res.next = new ListNode(l1.val);
                l1 = l1.next;
            } else {
                res.next = new ListNode(l2.val);
                l2 = l2.next;
            }
        }
        if (l1 != null) {
            res.next = l1;
        }
        if (l2 != null) {
            res.next = l2;
        }
        return res;
    }
}
```
