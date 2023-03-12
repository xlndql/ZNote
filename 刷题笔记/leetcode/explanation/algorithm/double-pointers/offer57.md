# 剑指 Offer 57. 和为s的两个数字

[剑指 Offer 57. 和为s的两个数字 - 力扣（Leetcode）](https://leetcode.cn/problems/he-wei-sde-liang-ge-shu-zi-lcof/description/)

## 功能

返回升序数组 nums 中和为 target 的两个数字，不用管顺序。

## 具体分析

通过双指针分别指向数组的头和尾，每次判断两个指针指向数字的和是否等于 target，等于则返回两个指针指向的值，小于 target 则将左指针向右移动一位，大于 target 则将右指针向左移动一位。

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.02.01 21:42
 */
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0, j = nums.length - 1; i < j; ) {
            if (nums[i] + nums[j] < target) i++;
            else if (nums[i] + nums[j] > target) j--;
            else return new int[]{nums[i], nums[j]};
        }
        return new int[]{-1, -1};
    }
}
```
