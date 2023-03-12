# 剑指 Offer 53 - I. 在排序数组中查找数字 I

[剑指 Offer 53 - I. 在排序数组中查找数字 I - 力扣（Leetcode）](https://leetcode.cn/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/description/)

## 功能

统计 targe 在数组 nums 中出现的次数。

## 具体分析

通过二分查找的方式找出 target 在数组 nums 中的左右边界 left 和 right，则 target 出现的次数为 right - left + 1。

## 数据结构

无额外数据结构。

## Java 代码实现

```
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.21 0:08
 */
public class Solution {
    public int search(int[] nums, int target) {
        int l = 0, r = nums.length - 1;
        while (l <= r) {
            int m = l + (r - l) / 2;
            if (nums[m] <= target) l = m + 1;
            else r = m - 1;
        }
        if (r >= 0 && nums[r] != target) return 0;
        int right = r;
        l = 0;
        r = nums.length - 1;
        while (l <= r) {
            int m = l + (r - l) / 2;
            if (nums[m] < target) l = m + 1;
            else r = m - 1;
        }
        int left = l;
        return right - left + 1;
    }
}
```
