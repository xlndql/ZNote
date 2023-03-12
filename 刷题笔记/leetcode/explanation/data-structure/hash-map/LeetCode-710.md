# 黑名单映射

例题来自 [710. 黑名单中的随机数 - 力扣（Leetcode）](https://leetcode.cn/problems/random-pick-with-blacklist/description/)

## 功能

在给定的一个整数范围和一个不重复的黑名单列表，随机获取给定整数范围内的数且不在黑名单列表中。

## 具体分析

若整数范围为 m，黑名单个数为 n，则将随机数获取的范围定为 [0, m - n)，就可以保证不会获取到 [m - n, m)，范围内的黑名单数据，若在 [0, m - n)，获取到黑名单数据，则通过哈希表映射到 [m - n, m)，中的非黑名单元素。

## 数据结构

通过一个哈希表保存 [0, m - n) 范围内的黑名单元素到 [m - n, m) 范围内非黑名单元素的映射关系。

## 伪代码

Solution(int n, int[] blackList)

* 将 blackList 中大于等于 n - blackList.length 的元素提出
* 将 blackList 中小于 n - blackList.length 的元素找出记为 key，并获取大于 n - blackList.length 小于 n 范围内非黑名单元素记为 val，将其存入 map（key => val）

pick()

* 随机产生 [0, n - blackList.length) 范围内的随机数
* 返回 map 中对应随机数的 val，如果没有则返回随机数本身

## Java代码实现

```java
public class Solution {
    Map<Integer, Integer> map;
    Random random;
    int len;

    public Solution(int n, int[] blacklist) {
        map = new HashMap<>();
        random = new Random();
        len = n - blacklist.length;
        Set<Integer> blackBeyondLen = new HashSet<>();
        for (int black : blacklist) {
            if (black >= len) blackBeyondLen.add(black);
        }
        int index = len;
        for (int black : blacklist) {
            if (black < len) {
                while (blackBeyondLen.contains(index)) {
                    index++;
                }
                map.put(black, index++);
            }
        }
    }

    public int pick() {
        int index = random.nextInt(len);
        return map.getOrDefault(index, index);
    }
}
```

> <div align="right">2023.1.12</div>
