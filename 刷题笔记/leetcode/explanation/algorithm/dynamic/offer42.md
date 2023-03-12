# 剑指 Offer 42. 连续子数组的最大和

[剑指 Offer 42. 连续子数组的最大和 - 力扣（Leetcode）](https://leetcode.cn/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/description/)

# 功能

将一个数组中的最大连续子数组的值返回。

# 具体分析

通过动态规划的方式，数组中从 0 到第 i 个数组元素的连续子数组最大值为 dp[i] = max(dp[i - 1] + num[i], num[i])，dp[i - 1] 为 0 到 i - 1 个数组元素的连续子数组最大值。其中若 dp[i - 1] < 0 则 dp[i - 1] + num[i] < num[i]，此时 dp[i] = num[i]。

# Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.29 19:16
 */
public class Solution {
    public int maxSubArray(int[] nums) {
        int res = nums[0];
        for (int i = 1; i < nums.length; i++) {
            if (nums[i - 1] > 0) nums[i] += nums[i - 1];
            res = res > nums[i] ? res : nums[i];
        }
        return res;
    }
}
```
