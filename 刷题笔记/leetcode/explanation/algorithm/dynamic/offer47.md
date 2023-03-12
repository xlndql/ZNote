# 剑指 Offer 47. 礼物的最大价值

[剑指 Offer 47. 礼物的最大价值 - 力扣（Leetcode）](https://leetcode.cn/problems/li-wu-de-zui-da-jie-zhi-lcof/description/)

# 功能

在一个 m * n 的棋盘中计算从左上到右下每次向右或向下走一格，最多可以得到多大价值的分。

# 具体分析

通过一遍遍历计算每一格能获得的最大值，一直到最后一格。

利用动态规划的方式，一共有四种情况（i 为行，j 为列）：

* i = 0 && j = 0 时，dp[i][j] = num[i][j]
* i = 0 && j != 0 时，dp[i][j] = dp[i][j - 1] + num[i][j]
* i != 0 && j = 0 时，dp[i][j] = dp[i - 1][j] + num[i][j]
* i != 0 && j != 0 时，dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]) + num[i][j]

# Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.29 19:49
 */
public class Solution {
    public int maxValue(int[][] grid) {
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (i == 0 && j == 0) continue;
                else if (i == 0) grid[i][j] += grid[i][j - 1];
                else if (j == 0) grid[i][j] += grid[i - 1][j];
                else grid[i][j] += Math.max(grid[i][j - 1], grid[i - 1][j]);
            }
        }
        return grid[grid.length - 1][grid[0].length - 1];
    }
}
```
