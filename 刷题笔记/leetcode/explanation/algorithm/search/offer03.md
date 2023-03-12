# 剑指 Offer 03. 数组中重复的数字

[剑指 Offer 03. 数组中重复的数字 - 力扣（Leetcode）](https://leetcode.cn/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/description/)

## 功能

找出数组中一个重复的元素并返回。

## 1.利用辅助 Set

### 详细分析

通过辅助 set 来记录数组中每一个值，若有重复则立即返回

### 数据结构

一个辅助 Set 对象来存数组元素。

```java
Set<Integer> set = new HashSet<>();
```

### Java 代码实现

这里使用数组更加快速高效。

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.20 22:41
 */
public class Solution {
    public int findRepeatNumber(int[] nums) {
        int[] map = new int[100000];
        for (int num : nums) {
            if (map[num] > 0) return num;
            map[num]++;
        }
        return -1;
    }
}
```

## 2.原地交换

### 详细分析

因为本题的特殊性，数组元素大小为[0, n - 1]，数组大小为 n，则可以通过在原数组中使用将下标与值一一对应的方式来判断是否有多余的数，有则直接返回该数。

### 数据结构

本地修改，无多余数据结构。

### Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.20 23:51
 */
public class Solution {
    public int findRepeatNumber(int[] nums) {
        int i = 0;
        while (i < nums.length) {
	// 若当前 i 与 nums[i] 相同，则移动到下一位
            if (nums[i] == i) {
                i++;
                continue;
            }
	// 若当前 i 与 nums[i] 不相同，则意味着需要将 nums[i] 移动到对应的nums[nums[i]]的位置
	// 若对应位置以及存在相同的数，则直接返回
            if (nums[i] == nums[nums[i]]) return nums[i];
	// 否则将nums[i]的值与nums[nums[i]]处的值互换，继续判断nums[i]的值是否等于 i
            int tmp = nums[i];
            nums[i] = nums[nums[i]];
            nums[tmp] = tmp;
        }
        return -1;
    }
}
```

最终要保证所有的 i = nums[i] 如果有冲突的则直接返回。
