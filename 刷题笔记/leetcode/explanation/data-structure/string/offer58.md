# 剑指 Offer 58 - II. 左旋转字符串

[剑指 Offer 58 - II. 左旋转字符串 - 力扣（Leetcode）](https://leetcode.cn/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/description/)

## 功能

获取一个字符串 s 和 int 类型变量 n，将字符串 s 的前 n 个字符移动到字符串 s 的末尾并返回。

## 具体分析

通过 Java 特有的 subString() 方法来完成。

## Java 代码实现

```java
/**
 * @Description Solution
 * @Author ZFiend
 * @Create 2023.01.19 21:54
 */
public class Solution {
    public String reverseLeftWords(String s, int n) {
        return s.substring(n) + s.substring(0, n);
    }
}
```
