# 剑指 Offer 35. 复杂链表的复制

[剑指 Offer 35. 复杂链表的复制 - 力扣（Leetcode）](https://leetcode.cn/problems/fu-za-lian-biao-de-fu-zhi-lcof/description/)

## 功能

复制链表的所有结构并返回头节点。

**Node：**

```java
public class Node {
    public int val;
    public Node next;
    public Node random;

    public Node(int val) {
        this.val = val;
        this.next = null;
        this.random = null;
    }
}
```

## 具体分析

通过一个哈希表来第一次遍历原链表并创建新的链表节点，使每个原链表节点和每个新链表节点的映射关系存入哈希表。

通过第二次遍历原链表来将 next 和 random 属性复制。

## 数据结构

通过一个 HashMap 来存储映射关系。

通过一个 Node 对象来作为每次遍历的指针。

```java
HashMap<Node, Node> map = new HashMap<>();
Node temp = head;
```

## Java 代码实现

```java
/**
 * @Description Solution
 * @Author ZFiend
 * @Create 2023.01.18 22:44
 */
public class Solution {
    public Node copyRandomList(Node head) {
        HashMap<Node, Node> map = new HashMap<>();
        Node temp = head;
        while (temp != null) {
            map.put(temp, new Node(temp.val));
            temp = temp.next;
        }
        temp = head;
        while (temp != null) {
            map.get(temp).next = map.get(temp.next);
            map.get(temp).random = map.get(temp.random);
            temp = temp.next;
        }
        return map.get(head);
    }
}
```
