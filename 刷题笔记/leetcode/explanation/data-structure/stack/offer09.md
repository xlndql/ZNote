# 剑指 Offer 09. 用两个栈实现队列

[剑指 Offer 09. 用两个栈实现队列 - 力扣（Leetcode）](https://leetcode.cn/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/description/)

## 功能

通过两个栈结构模拟队列的功能，具体有在尾部添加元素和删除头部元素。

## 具体分析

通过两个栈 in 和 out 来模拟栈，in 负责接收存入的数据，out 负责弹出数据，out 若为空则会首先从 in 中以逆序获取到所有的元素，让 in 的栈底成为 out 的栈顶，这样就可以模拟队列的先进先出。

## 数据结构

两个栈 in 和 out。

```java
private LinkedList<Integer> in = new LinkedList<>();
private LinkedList<Integer> out = new LinkedList<>();
```

## 伪代码

appendTail(int value)

* 将 value 存入 in

deleteHead()

1. out 不为空
   * 返回并删除 out 的顶部元素
2. out 为空
   1. in 不为空
      * 从 in 中获取并删除顶部元素
      * 将获取到的 in 的顶部元素存入 out
      * 循环执行以上两步直到 in 为空
   2. in 为空
      * 返回 -1

## Java代码实现

```java
/**
 * @Description Solution
 * @Author ZFiend
 * @Create 2023.01.16 21:26
 */
public class CQueue {
    LinkedList<Integer> stack1;
    LinkedList<Integer> stack2;

    public CQueue() {
        stack1 = new LinkedList<>();
        stack2 = new LinkedList<>();
    }

    public void appendTail(int value) {
        stack1.add(value);
    }

    public int deleteHead() {
        if (!stack2.isEmpty()) {
            return stack2.poll();
        }
        while (!stack1.isEmpty()) {
            stack2.add(stack1.poll());
        }
        return stack2.isEmpty() ? -1 : stack2.poll();
    }
}
```
