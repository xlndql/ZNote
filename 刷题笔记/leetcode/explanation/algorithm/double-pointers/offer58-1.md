# 剑指 Offer 58 - I. 翻转单词顺序

[剑指 Offer 58 - I. 翻转单词顺序 - 力扣（Leetcode）](https://leetcode.cn/problems/fan-zhuan-dan-ci-shun-xu-lcof/description/)

## 功能

将字符串中的所有单词逆序生成一个新字符串并返回。

## 具体分析

先利用 java 中字符串的一个方法 trim() 来去除字符串收尾的多余空格，再通过双指针从字符串最后一位每次读取一个单词存入一个新的 StringBuilder 对象，最后返回 StringBuilder 对象生成的字符串。

## Java 代码实现

```java
/**
 * @Description TODO Solution
 * @Author ZFiend
 * @Create 2023.02.01 21:45
 */
public class Solution {
    public String reverseWords(String s) {
        s = s.trim();
        StringBuilder res = new StringBuilder();
        int p1 = s.length() - 1, p2 = p1;
        while (p1 >= 0) {
            while (p1 >= 0 && s.charAt(p1) != ' ') p1--;
            res.append(s.substring(p1 + 1, p2 + 1)).append(" ");
            while (p1 >= 0 && s.charAt(p1) == ' ') p1--;
            p2 = p1;
        }
        return res.toString().trim();
    }
}
```
