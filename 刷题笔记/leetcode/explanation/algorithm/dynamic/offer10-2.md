# 剑指 Offer 10- II. 青蛙跳台阶问题

[剑指 Offer 10- II. 青蛙跳台阶问题 - 力扣（Leetcode）](https://leetcode.cn/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/description/)

## 功能

一只青蛙一次可以跳一个台阶也可以跳两个台阶，求出青蛙跳到第 n 个台阶的时候有几种跳法。

## 具体分析

通过动态规划可知，青蛙跳最后一步时有两种情况，一种是跳一个台阶，记为 dp(n - 1)；一种是跳两个台阶，记为 dp(n - 2)。则 dp(n) 即是以上两种情况的和，即 dp(n) = dp(n - 1) + dp(n - 2)，就等同于斐波那契数列，不同的点在于起始数字不同：dp(0) = 1，dp(1) = 1。

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.26 21:55
 */
public class Solution {
    public int numWays(int n) {
        int f0 = 1, f1 = 1, f2;
        while (n-- > 0) {
            f2 = (f0 + f1) % 1000000007;
            f0 = f1;
            f1 = f2;
        }
        return f0;
    }
}
```
