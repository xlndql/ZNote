# 剑指 Offer 50. 第一个只出现一次的字符

[剑指 Offer 50. 第一个只出现一次的字符 - 力扣（Leetcode）](https://leetcode.cn/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/description/)

## 功能

找出字符串中第一个只出现一次的字符。

## 具体分析

通过一个 LinkedHashMap 来保存字符对是否只出现一次的映射，遍历后返回第一个只出现一次的字符。

## 数据结构

一个 map 来保存所有字符对是否只出现一次的映射。

```java
Map<Character, Boolean> map = new LinkedHashMap<>();
```

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.01.23 16:29
 */
public class Solution {
    public char firstUniqChar(String s) {
        Map<Character, Boolean> map = new LinkedHashMap<>();
        char[] chars = s.toCharArray();
        for (char c : chars) {
            map.put(c, !map.containsKey(c));
        }
        for (Character key : map.keySet()) {
            if (map.get(key)) return key;
        }
        return ' ';
    }
}
```
