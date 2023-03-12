# 剑指 Offer 10- I. 斐波那契数列

[剑指 Offer 10- I. 斐波那契数列 - 力扣（Leetcode）](https://leetcode.cn/problems/fei-bo-na-qi-shu-lie-lcof/description/)

## 功能

返回第 n 个斐波那契数列数并对（1e9 + 7）取余。

## 具体分析

通过动态规划的方式，第 n 个斐波那契数列数定为 dp[n]，则 dp[n] = dp[n - 1] + dp[n - 2]，则可得 dp[2] = dp[1] + dp[0]，因为 dp[0] = 0，dp[1] = 1，所以可以通过动态规划实现。

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.26 21:21
 */
public class Solution {
    public int fib(int n) {
        int f0 = 0, f1 = 1, f2;
        while (--n > 0) {
            f2 = (f0 + f1) % 1000000007;
            f0 = f1;
            f1 = f2;
        }
        return f0;
    }
}
```
