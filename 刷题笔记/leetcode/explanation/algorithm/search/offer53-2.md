# 剑指 Offer 53 - II. 0～n-1中缺失的数字

[剑指 Offer 53 - II. 0～n-1中缺失的数字 - 力扣（Leetcode）](https://leetcode.cn/problems/que-shi-de-shu-zi-lcof/description/)

## 功能

找出在长度为 n - 1元素唯一且元素的范围为[0, n - 1]的递增数组中缺少的那个数。

## 具体分析

直接通过遍历的方式，当数组下标 i 不等于当前下标对应的值时就是缺少的那个数。

## 数据结构

无额外数据结构

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.21 0:28
 */
public class Solution {
    public int missingNumber(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != i) return i;
        }
        return nums.length;
    }
}
```
