# 剑指 Offer 06. 从尾到头打印链表

[剑指 Offer 06. 从尾到头打印链表 - 力扣（Leetcode）](https://leetcode.cn/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/description/)

## 功能

如题。

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

## 1.递归方式

### 具体分析

通过递归的方式从链表的最后一位开始存入数组。

### 数据结构

通过一个可变数组 ArrayList 存倒叙的链表值

通过一个数组将 ArrayList 的数据存储并返回

### Java代码实现

```java
/**
 * @Description Solution
 * @Author ZFiend
 * @Create 2023.01.18 21:34
 */
public class Solution {
    ArrayList<Integer> tmp = new ArrayList<>();

    public int[] reversePrint(ListNode head) {
        recursion(head);
        int[] res = new int[tmp.size()];
        for (int i = 0; i < tmp.size(); i++) {
            res[i] = tmp.get(i);
        }
        return res;
    }

    private void recursion(ListNode head) {
        if (head == null) return;
        recursion(head.next);
        tmp.add(head.val);
    }
}
```


## 2.辅助栈方式

### 具体分析

通过一个辅助的栈结构来存储链表数据，再从栈中弹出所有元素存入数组返回。

### 数据结构

通过一个栈结构临时存储链表数据。

```java
Stack<Integer> stack = new Stack<>();
```

通过一个数组存储栈弹出的元素并返回。

```java
int[] res = new int[stack.size()];
```

### Java代码实现

```java
/**
 * @Description Solution
 * @Author ZFiend
 * @Create 2023.01.18 21:15
 */
public class Solution {
    public int[] reversePrint(ListNode head) {
        LinkedList<Integer> stack = new LinkedList<>();
        while (head != null) {
            stack.push(head.val);
            head = head.next;
        }
        int[] res = new int[stack.size()];
        for (int i = 0; i < res.length; i++) {
            res[i] = stack.poll();
        }
        return res;
    }
}
```


## 3.辅助链表元素 node 方式

### 具体分析

通过一个链表元素遍历完链表记录链表的长度 len，然后创建一个长度为 len 的数组，逆序存储链表中的所有数据然后返回数组。

### 数据结构

通过一个链表元素 node 来遍历链表。

```java
ListNode node = new ListNode();
```

通过 一个 int 类型的数据来记录链表长度。

```java
int len = 0;
```

### Java代码实现

```java
/**
 * @Description Solution
 * @Author ZFiend
 * @Create 2023.01.18 21:21
 */
public class Solution {
    public int[] reversePrint(ListNode head) {
        ListNode node = head;
        int len = 0;
        while (node != null) {
            len++;
            node = node.next;
        }
        int[] res = new int[len];
        for (int i = len - 1; i >= 0; i--) {
            res[i] = head.val;
            head = head.next;
        }
        return res;
    }
}
```
