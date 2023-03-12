# 剑指 Offer 63. 股票的最大利润

[剑指 Offer 63. 股票的最大利润 - 力扣（Leetcode）](https://leetcode.cn/problems/gu-piao-de-zui-da-li-run-lcof/description/)

## 功能

将股票的价格按照时间顺序存在数组中，计算只买卖一次可获得的最大利润。

## 具体分析

通过动态规划可得，令第 n 天可获得的最大利润为 dp(n)，则 dp(n) = max(dp(n - 1), price[n] - min(price[0 : n]))。意思是第 n 天的最大利润为第 n - 1 天的最大利润和第 n 天的价格减去前 n - 1 天中最低价格求得的利润比较，返回较大者，即为第 n 天的最大利润。

则可以得到 dp(0) = 0，dp(1) = max(dp(0), price[1] - min(price[0:1]))，则可以解答问题。

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.26 22:05
 */
public class Solution {
    public int maxProfit(int[] prices) {
        int profit = 0, minPrice = Integer.MAX_VALUE;
        for (int price : prices) {
            minPrice = Math.min(price, minPrice);
            profit = Math.max(profit, price - minPrice);
        }
        return profit;
    }
}
```
