# 剑指 Offer 30. 包含 min 函数的栈

[剑指 Offer 30. 包含min函数的栈 - 力扣（Leetcode）](https://leetcode.cn/problems/bao-han-minhan-shu-de-zhan-lcof/description/)

## 功能

push(int x)

将数据存入 MinStack 栈中

pop()

将 MinStack 栈中的顶部数据弹出

top()

返回栈中的顶部数据

min()

返回目前栈中所有元素的最小元素

## 1. 压栈的方式

### 具体分析

通过维护两个栈结构 all 和 min 来将 min() 操作的时间复杂度降到 O(1) 。

每次存入 min 时判断是否比当前 min 的顶部元素小或等于，如果是则存入，不是则不存。

pop() 操作移除元素时每次判断 all 移除的顶部元素是否与 min 顶部的一致，一致则同时都移除，不一致则只移除 all 的顶部，确保 min 的顶部永远是当前 all 中所有元素的最小值。

### 数据结构

通过一个栈 all 来存储所有 push(int x) 进来的元素。

```java
LinkedList<Integer> all = new LinkedList<>();
```

通过一个栈 min 来存储每次比 min 顶部元素小的元素。

```java
LinkedList<Integer> min = new LinkedList<>();
```

**注：因为性能的原因，这里的栈通过 LinkedList 来模拟，而不直接使用 Stack。**

### 伪代码

push(int x)

1. min 为空：

   * x 存入 min 中
2. min 不为空：

   1. x 小于等于 min 的顶部元素
      * x 存入 min 中
   2. x 大于 min 的顶部元素
      * x 不存入 min 中

* x 存入 all 中

pop()

1. min 的顶部元素等于 all 的顶部元素
   * min 抛出顶部元素
2. min 的顶部元素不等于 all 的顶部元素
   * min 不抛出顶部元素

* all 抛出顶部元素

top()

* all 返回顶部元素

min()

* min 返回顶部元素

### Java代码实现

```java
/**
 * @Description MinStack
 * @Author ZFiend
 * @Create 2023.01.16 22:20
 */
class MinStack {
    LinkedList<Integer> min;
    LinkedList<Integer> all;

    /**
     * initialize your data structure here.
     */
    public MinStack() {
        min = new LinkedList<>();
        all = new LinkedList<>();
    }

    public void push(int x) {
        if (!min.isEmpty() && x <= min.peek()) {
            min.push(x);
        }
        if (min.isEmpty()) min.push(x);
        all.push(x);
    }

    public void pop() {
        if (Objects.equals(min.peek(), all.poll())) {
            min.poll();
        }
    }

    public int top() {
        return all.peek();
    }

    public int min() {
        return min.peek();
    }
}
```

## 2.自定义链表结点方式

### 具体分析

通过自定义链表结点的方式模拟栈，将每一个结点 Node 都存有以这个结点为头往下所有结点的最小值 minVal 和自己的值 val，以及下一个结点指针 next。

使用一个 Node 对象 head 来指向链表的头位置来模拟出入栈和查询。

### 数据结构

通过一个自定义的 Node 结构来模拟这题的栈结构。

通过一个 Node 对象 head 来记录栈的头位置。

```java
class Node {
    int val;
    int minVal;
    Node next;

    public Node(int val, int minVal) {
        this.val = val;
        this.minVal = minVal;
    }
}
Node head;
```

### 伪代码

MinStack()

* 初始化 head ，将 head 的 minVal 设置为 int 类型的最大值

push(int x)

* 创建 Node 对象 node
* 将 x 存入 node 的 val 值
* 将 head 的 minVal 值和 x 进行比较，取较小值存入 node 的 minVal 值
* 令 node.next = head，将 head 接到 node 的尾部
* 令 head = node，更新 head 为 node

pop()

* 令 head = head.next ，模拟删除栈顶元素

top()

* 返回 head 的 val 值

min()

* 返回 head 的 minVal 值

### Java代码实现

```java
/**
 * @Description MinStack
 * @Author ZFiend
 * @Create 2023.01.16 22:36
 */
public class MinStack {
    class Node {
        int val;
        int minVal;
        Node next;

        public Node(int val, int minVal) {
            this.val = val;
            this.minVal = minVal;
        }
    }

    Node head;

    /**
     * initialize your data structure here.
     */
    public MinStack() {
        head = new Node(-1, Integer.MAX_VALUE);
    }

    public void push(int x) {
        Node node = new Node(x, Math.min(x, head.minVal));
        node.next = head;
        head = node;
    }

    public void pop() {
        head = head.next;
    }

    public int top() {
        return head.val;
    }

    public int min() {
        return head.minVal;
    }
}
```
