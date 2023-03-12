# 146. LRU 缓存

[146. LRU 缓存 - 力扣（Leetcode）](https://leetcode.cn/problems/lru-cache/)

LRU：是最近最少使用（最长时间）淘汰算法（Least Recently Used）。淘汰最长时间没有被使用的页面。

## 功能

容量 capacity：用于记录当前缓存的容量。

get(int key)：用于获取缓存中的某个数据。

* key存在，返回val
* key不存在，返回-1

put(int key, int value)：用于将某个数据写入缓存。

* key已存在，修改对应的val
* key不存在，写入缓存，写入前缓存已经达到容量上限，则删除最末尾的缓存数据

## 具体分析

每次 put 或者 get 操作时将元素从有序的哈希表中删除再重新添加到头部，每次删除时删除有序哈希表的尾部元素。

## 数据结构

使用**双向链表**维护缓存的顺序结构，保证调用的时间顺序。

```java
/**
 * 节点
 **/
class Node {
    public int key, val;
    public Node next, prev;
    public Node(int k, int v) {
        this.key = k;
        this.val = v;
    }
}
```

使用**哈希表**保证在O(1)的时间复杂度内获取到缓存数据的位置。

```java
/**
 * 哈希表
 */
Map<Integer, Node> hashMap = new HashMap<>();
```

## 伪代码

get(int key)

1. key存在：
   * 根据哈希表查出key对应的value（node节点）在双向链表中删除该节点，重新插入到链表头部。
   * 返回该节点对应的value
2. key不存在：
   * 返回-1

put(int key, int value)

1. 容量达到了上限
   * 删除双向链表的尾节点，并获取删除的节点的key
   * 删除哈希表中key对应的映射关系
   * 根据输入参数构造新的节点
   * 将新的节点插入链表头部
   * 将新的key和节点的映射关系存入哈希表
2. 容量没有达到上限
   * 根据输入参数构造新的节点
   * 将新的节点插入链表头部
   * 将新的key和节点的映射关系存入哈希表

## Java代码实现

java中的 LinkedHashMap 集合容器拥有双向链表和哈希表的特性，可以直接用来实现LRU算法，具体如下：

```java
public class LRUCache {
    LinkedHashMap<Integer, Integer> cache;
    int capacity;
  
    public LRUCache(int capacity) {
        cache = new LinkedHashMap<>();
        this.capacity = capacity;  
    }

    public int get(int key) {
        if (cache.containsKey(key)) {	// 如果key存在，则将key放到容器头部并返回val
            Integer val = cache.get(key);
            cache.remove(key);
            cache.put(key, val);
            return val;
        }
        return -1;	// 如果key不存在，则返回-1
    }

    public void put(int key, int val) {
        get(key);	// 先调用get()方法将put的key调用一次，若存在则会被放到容器头部
        cache.put(key, val);	// 将容器中key对应的val更新
        if (cache.size() > capacity) {	// 如果容器的大小大于capacity，则将尾部节点删除
            Integer removeKey = cache.keySet().iterator().next();
            cache.remove(removeKey);
        }
    }
}
```

> <p align="right">2023.1.9</p>
