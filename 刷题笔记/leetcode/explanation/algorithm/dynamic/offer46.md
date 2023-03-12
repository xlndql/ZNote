# 剑指 Offer 46. 把数字翻译成字符串

[剑指 Offer 46. 把数字翻译成字符串 - 力扣（Leetcode）](https://leetcode.cn/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/description/)

## 功能

给定一个数字，将这个数字能翻译成的字符串个数返回。

## 具体分析

通过动态规划可得，当第 i 个数字和第 i - 1 个数字组成的二位数不在 [0, 25] 范围内时，第 i 个数能翻译成的字符串个数为 dp[i] = dp[i - 1]；当第 i 个数字和第 i - 1 个数字组成的二位数在 [0, 25] 范围内时，第 i 个数能翻译成的字符串个数为dp[i] = dp[i - 1] + dp[i - 2]，则可解答此题。

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.30 22:18
 */
public class Solution {
    public int translateNum(int num) {
        if (num == 0) return 1;
        int f0 = 1, f1 = 1, f2, num1, num2 = num % 10;
        num /= 10;
        while (num > 0) {
            num1 = num2;
            num2 = num % 10;
            num /= 10;
            if ((num2 * 10 + num1 < 26) && num2 != 0) f2 = f0 + f1;
            else f2 = f1;
            f0 = f1;
            f1 = f2;
        }
        return f1;
    }
}
```
