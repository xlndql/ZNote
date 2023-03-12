# 剑指 Offer 24. 反转链表

[剑指 Offer 24. 反转链表 - 力扣（Leetcode）](https://leetcode.cn/problems/fan-zhuan-lian-biao-lcof/description/)

## 功能

翻转链表元素并返回。

**ListNode：**

```java
public class ListNode {
    public int val;
    public ListNode next;

    ListNode(int x) {
        val = x;
    }
}
```

## 具体分析

通过双指针的方式，将每一个节点的 next 和 prev 交换。

## 数据结构

通过两个链表元素 Node 作为两个指针来交换链表元素的 next 和 prev。

```java
ListNode prev = null;
ListNode temp = head;
```

## 伪代码

1. 当 temp 不为 null 时
   * 在每次循环开始使 head 等于 temp，确保返回结果时 head 不为 null
   * 使 temp 等于 head.next，让 temp 记录初始 head 的 next 值，往前移动一位
   * 使 head.next 等于 prev，让 head 的 next 重新赋值为 prev
   * 使 prev 等于 head，让 prev 成为 head，向前移动一位

## Java 代码实现

```java
/**
 * @Description Solution
 * @Author ZFiend
 * @Create 2023.01.18 22:08
 */
public class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null, temp = head;
        while (temp != null) {
            head = temp;
            temp = head.next;
            head.next = prev;
            prev = head;
        }
        return head;
    }
}
```
