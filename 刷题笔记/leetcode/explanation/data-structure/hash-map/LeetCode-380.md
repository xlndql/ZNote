# 在 o(1) 时间内完成数组元素插入删除和随机获取

例题来自 [380. O(1) 时间插入、删除和获取随机元素 - 力扣（Leetcode）](https://leetcode.cn/problems/insert-delete-getrandom-o1/description/) 。

## 功能

在 o(1) 的时间内完成对一个 RandomizedSet 集合的插入、删除和随机取值。

## 具体分析

通过一个可变数组和一个 val => key 的哈希表来保证数据的插入和查找在 O(1) 时间内完成，删除功能首先通过在哈希表中获取 val 对应的 key 的值后，将数组中的 key 与最后一个元素互换位置后删除最后一个元素来完成删除操作，这样可以最大限度的保证数组中每个元素还保持原先的位置，就不用对哈希表中的数据进行大的改动。

## 数据结构

通过一个 ArrayList 来保存整个集合中的数据。

通过一个 HashMap 来保存 ArrayList 中 val 到 index 的映射。

## 伪代码

insert(int val)

1. *key 存在*
   * 返回 false
2. key不存在
   * list 中插入 val
   * map 中新增 val 到 list 中 val 对应的 index 的映射（val => index）
   * 返回 true

remove(int val)

1. key 存在
   * 从 map 中获取到 val 对应的 index
   * 获取 list 中最后一个位置的值 lastVal
   * 将 list 中最后一个位置的值 lastVal 和 index 处的数据 val 交换位置（做到最少的移动元素位置来删除元素）
   * 将 map 中 lastVal 对应的位置修改成 index，和 list 同步
   * 移除 list 最后一位
   * 移除 map 中 val 对应的映射关系
2. key 不存在
   * 返回 false

getRandom()

* 获取 list.size() 范围内的随机正整数 num
* 返回 list 中对应 num 位置的值

## Java代码实现

```java
public class RandomizedSet {
    ArrayList<Integer> list;
    HashMap<Integer, Integer> map;

    public RandomizedSet() {
        list = new ArrayList<>();
        map = new HashMap<>();
    }

    public boolean insert(int val) {
        if (map.containsKey(val)) {
            return false;
        }
        map.put(val, list.size());
        list.add(val);
        return true;
    }

    public boolean remove(int val) {
        if (!map.containsKey(val)) {
            return false;
        }
        Integer i = map.get(val);
        swap(i, list.size() - 1);	// 通过将要删除的元素和list中最后一个元素交换位置后删除，可以只修改一个元素的位置就做到在数组中删除元素。
        list.remove(list.size() - 1);
        map.remove(val);
        return true;
    }

    private void swap(int i1, int i2) {
        map.put(list.get(i2), i1);
        Integer temp = list.get(i1);
        list.set(i1, list.get(i2));
        list.set(i2, temp);
    }

    public int getRandom() {
        int num = new Random().nextInt(list.size());
        return list.get(num);
    }
}
```

> <div align="right">2023.1.10</div>
