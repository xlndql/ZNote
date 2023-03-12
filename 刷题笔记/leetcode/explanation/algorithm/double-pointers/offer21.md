# 剑指 Offer 21. 调整数组顺序使奇数位于偶数前面

[剑指 Offer 21. 调整数组顺序使奇数位于偶数前面 - 力扣（Leetcode）](https://leetcode.cn/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/description/)

## 功能

将数组 nums 中所有的奇数都移动到偶数前面。

## 具体分析

通过两个指针，分别从数组的头和尾开始遍历，左指针找偶数，右指针找奇数，两个指针都找到时互换两个指针对应的值，当左指针越过右指针时结束查找。

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.02.01 21:25
 */
public class Solution {
    public int[] exchange(int[] nums) {
        int p1 = 0, p2 = nums.length - 1;
        while (p1 < p2) {
            while (nums[p1] % 2 != 0 && p1 < nums.length) p1++;
            while (nums[p2] % 2 == 0 && p2 >= 0) p2--;
            if (p1 >= p2) break;
            int tmp = nums[p1];
            nums[p1] = nums[p2];
            nums[p2] = tmp;
        }
        return nums;
    }
}
```
