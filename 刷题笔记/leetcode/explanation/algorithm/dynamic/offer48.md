# 剑指 Offer 48. 最长不含重复字符的子字符串

[剑指 Offer 48. 最长不含重复字符的子字符串 - 力扣（Leetcode）](https://leetcode.cn/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/description/)

## 功能

给定一个字符串，返回该字符串中最长不含重复字符的子字符串。

## 具体分析

通过动态规划可得，从 0 到第 i 个字符中最长不含重复字符的字符串为：

* 当第 i 个字符和前面无重复时：dp[i] = dp[i - 1] + 1
* 当第 i 个字符和前面有重复时：
  * 当第 i 个字符重复的位置在 dp[i - 1] 之外，则不影响结果：dp[i] = dp[i - 1] + 1
  * 当第 i 个字符重复的位置在 dp[i - 1] 之内，则结果：dp[i] = i - i 重复位置下标

最后返回最大的 dp[i] 可解此题。

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.30 22:54
 */
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int[] ton = new int[256]; // 用于保存每个字符的下标
        int maxLen = 0, len = 0; // 用于临时保存 dp[i] 和 dp[i] 的最大值
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
	    // 若当前位置 i 到字符 c 重复位置的长度大于此时的 dp[i - 1]，则重复位置在范围外，不影响，所以dp[i] = dp[i - 1] + 1；反之，则 dp[i] 被更新为当前位置 i 到字符 c 重复位置的长度
            len = len < i - (ton[c] - 1) ? len + 1 : i - (ton[c] - 1); 
            maxLen = maxLen > len ? maxLen : len; // 每次循环都记录最大的子字符串的长度
            ton[c] = i + 1; // 每次循环都将该字符的下标存入数组（下标 + 1 是为了区分已存入的下标（大于0）和未存入的下标（等于0））
        }
        return maxLen;
    }
}
```
