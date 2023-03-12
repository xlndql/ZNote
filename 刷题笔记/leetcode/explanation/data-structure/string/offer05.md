# 剑指 Offer 05. 替换空格

[剑指 Offer 05. 替换空格 - 力扣（Leetcode）](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/description/)

## 功能

将字符串中的空格替换成 "%20"。

## 具体分析

通过 Java 特有的 StringBuilder 类来操作字符串，提高效率。

## 数据结构

通过一个 StringBuilder 类来保存字符串的每一个字符，将所有空格替换成 "%20"。

```java
StringBuilder sb = new StringBuilder();
```

## Java 代码实现

```java
/**
 * @Description Solution
 * @Author ZFiend
 * @Create 2023.01.19 21:46
 */
public class Solution {
    public String replaceSpace(String s) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == ' ') {
                sb.append("%20");
            } else {
                sb.append(s.charAt(i));
            }
        }
        return sb.toString();
    }
}
```
