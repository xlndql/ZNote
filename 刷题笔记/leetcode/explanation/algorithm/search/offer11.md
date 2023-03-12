# 剑指 Offer 11. 旋转数组的最小数字

[剑指 Offer 11. 旋转数组的最小数字 - 力扣（Leetcode）](https://leetcode.cn/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/description/)

## 功能

一个递增的有序数组经过多次的区间旋转。

## 具体分析

通过一次遍历出结果，如果第 i 个元素比第 i - 1 个元素小，则将第 i 个元素与目前的最小值比较，计算新的最小值，最后返回最小值。

## 数据结构

无额外数据结构。

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.23 16:16
 */
public class Solution {
    public int minArray(int[] numbers) {
        int min = numbers[0];
        for (int i = 1; i < numbers.length; i++) {
            if (numbers[i] < numbers[i - 1]) {
                min = min < numbers[i] ? min : numbers[i];
            }
        }
        return min;
    }
}
```
