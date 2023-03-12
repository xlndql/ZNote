# 数据流的中位数

例题来自 [295. 数据流的中位数 - 力扣（Leetcode）](https://leetcode.cn/problems/find-median-from-data-stream/description/)

## 功能

在给定的动态数据流中可以满足随时插入数据和获取目前所有元素的中位数。

## 具体分析

通过使用两个优先队列，一个大顶堆一个小顶堆，让每次插入的数据均匀分布在两个队列中，则获取中位数时只要通过当前的数据总数和两个队列的堆顶就可以判断。

## 数据结构

通过使用两个 PriorityQueue 来将获取的数据按顺序均匀分布在两个队列中。

## 伪代码

addNum(int num)

1. smallQueue 的大小 大于等于 largeQueue 的大小
   * 将 num 存入 smallQueue
   * 将 smallQueue 的堆顶移除并存入 largeQueue 中
2. smallQueue 的大小 小于 largeQueue 的大小
   * 将 num 存入 largeQueue
   * 将 largeQueue 的堆顶移除并存入 smallQueue 中

findMedian()

1. smallQueue 的大小 大于 largeQueue 的大小
   * 返回 smallQueue 的堆顶
2. smallQueue 的大小 小于 largeQueue 的大小
   * 返回 largeQueue 的堆顶
3. smallQueue 的大小 等于 largeQueue 的大小
   * 返回 smallQueue 和 largeQueue 的两个堆顶的平均值

## Java代码实现

```java
public class MedianFinder {
    PriorityQueue<Integer> smallQueue;
    PriorityQueue<Integer> largeQueue;

    public MedianFinder() {
        smallQueue = new PriorityQueue<>();
        largeQueue = new PriorityQueue<>((a, b) -> b - a);	// 定义大顶堆的优先队列
    }

    public void addNum(int num) {
        if (smallQueue.size() >= largeQueue.size()) {
            smallQueue.offer(num);	// 数据存入小顶堆队列
            largeQueue.offer(smallQueue.poll());	// 将堆顶的值存入大顶堆队列
        } else {
            largeQueue.offer(num);	// 数据存入大顶堆队列
            smallQueue.offer(largeQueue.poll());	// 将堆顶的值存入小顶堆队列
        }
    }

    public double findMedian() {
        if (smallQueue.size() > largeQueue.size()) {
            return smallQueue.peek();
        } else if (smallQueue.size() < largeQueue.size()) {
            return largeQueue.peek();
        }
        return (smallQueue.peek() + largeQueue.peek()) / 2.0;
    }
}
```
