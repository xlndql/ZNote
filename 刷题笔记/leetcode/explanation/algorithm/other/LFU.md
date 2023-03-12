# 460. LFU 缓存

[460. LFU 缓存 - 力扣（Leetcode）](https://leetcode.cn/problems/lfu-cache/)

LFU：最不经常使用（最少次）淘汰算法（Least Frequently Used）。淘汰一段时间使用次数最少的页面。

## 功能

容量 capacity：用于记录当前缓存的容量。

get(int key)：用于获取缓存中的某个数据。

* key存在，返回val
* key不存在，返回-1

put(int key, int value)：用于将某个数据写入缓存。

* key存在，修改对应的val
* key不存在，写入缓存，若写入前缓存已经达到容量上限，则应该淘汰使用次数最少的缓存
* 若使用次数最少的缓存不止一个，则应该淘汰最久未使用的缓存

## 具体分析

每次调用 get 和 put 方法时将每个元素对应的调用次数 + 1，每次删除调用次数最少的元素列表中的尾部元素。

## 数据结构

使用HashMap存储key到val的映射，快速计算get(key)

```java
HashMap<Integer, Integer> keyToVal;
```

使用HashMap存储key到freq的映射，快速获取当前key对应的使用频率

```java
HashMap<Integer, Integer> keyToFreq;
```

使用HashMap存储freq到keys的映射，快速获取当前freq下的所有key

```java
HashMap<Integer, LinkedHashSet<Integer>> freqToKeys;
```

使用Integer存储capacity（缓存容量）

```java
int capacity;
```

使用Integer存储minFreq（最少使用次数），快速获取当前使用最少的次数

```java
int minFreq;
```

## 伪代码

get(int val)

1. key存在
   * 在 keyToFreq 中获取当前key对应的调用次数 freq
   * 在 freqToKeys 里 freq 对应的keys中将key删除
   * 如果当前 freq 对应的keys的数量为0，则删除 freqToKeys里 freq 对应的映射关系（防止查找时找到空数据）
   * 在 freqToKeys 里查找 freq + 1 对应的keys，将 key 插入keys的头位置，若不存在 keys 则创建一个新的keys将key存入，最后存入 freqToKeys 的 freq + 1 位置
   * 更新 minFreq 的值
   * 更新 keyToFreq 中 key 对应的 freq（+1）
2. key不存在
   * 返回 -1

put(int key, int val)

1. key存在
   * 参考 get(int val) 中 key 存在的情况
   * 将 keyToVal 中 key 对应的 val 更新成对应的新 val
2. key不存在
   * 如果当前缓存容量已经到达上限
     * 在 freqToKeys 中获取 minFreq 对应的 keys
     * 将其中的第一个 key 获取，作为将要删除的 key
     * 将 keyToVal 中 key 对应的映射关系删除
     * 将 keyToFreq 中 key 对应的映射关系删除
     * 将 freqToKeys 中 对应的 keys 中的 key 删除
     * 若此时的 keys 为空，则将 keys 从 freqToKeys 中删除
   * 如果当前容量没有达到上限
     * 在 keyToVal 中新增 key 和 val 的映射关系
     * 在 ketToFreq 中新增 key 和 freq（1） 的映射关系
     * 在 freqToKeys 中 freq = 1 的头部添加 key
     * 将 minFreq 的值设置为 1

## Java代码实现

在 freqToKeys 中需要每一个 freq 对应的 keys 都保证插入顺序，则可以利用 LinkedHashSet 来储存 keys

```java
public class LFUCache {
    HashMap<Integer, Integer> keyToVal;
    HashMap<Integer, Integer> keyToFreq;
    HashMap<Integer, LinkedHashSet<Integer>> freqToKeys;
    int capacity;
    int minFreq;
  
    public LFUCache(int capacity) {
        keyToVal = new HashMap<>();
        keyToFreq = new HashMap<>();
        freqToKeys = new HashMap<>();
        this.capacity = capacity;
        minFreq = 0;
    }

    public int get(int key) {
        if (keyToVal.containsKey(key)) {    //  如果存在key则将key对应的映射关系更新
            increaseFreq(key);
            return keyToVal.get(key);
        }
        return -1;
    }

    public void put(int key, int val) {
        if (capacity <= 0) return;  //  如果容量本身小于0，则直接返回
        if (keyToVal.containsKey(key)) {  //  如果存在这个key，则直接更新freq
            increaseFreq(key);
        } else {
            if (keyToFreq.size() == capacity) { //  如果此时容量达到上限，则先将使用次数最少的key去除
                removeMinFreqKey();
            }
            keyToFreq.put(key, 1);  //  将新的key添加到freq = 1 中
            freqToKeys.putIfAbsent(1, new LinkedHashSet<>());   // 若freq=1的keys为空，则添加新的map
            freqToKeys.get(1).add(key);    //  将新key添加到set集合中
            this.minFreq = 1;   //  插入新的节点最小的freq一定为1
        }
        keyToVal.put(key, val); //  将key存入keyToVal
    }

    public void increaseFreq(int key) {
        Integer freq = keyToFreq.get(key);//  获取key对应的调用次数
        keyToFreq.put(key, freq + 1);     //  更新key的调用次数
        freqToKeys.get(freq).remove(key);   //  移除旧调用次数的set集合中的val
        if (freqToKeys.get(freq).isEmpty()) { //  如果旧调用次数的set集合为空，则去掉旧调用集合
            freqToKeys.remove(freq);
            if (freq == minFreq) minFreq++; //  如果这个freq正好是minFreq，则更新minFreq
        }
        freqToKeys.putIfAbsent(freq + 1, new LinkedHashSet<>());
        freqToKeys.get(freq + 1).add(key);  //  将key存入新调用集合
    }

    public void removeMinFreqKey() {
        LinkedHashSet<Integer> minFreqKeysSet = freqToKeys.get(minFreq);    //  获取目前最小freq对应的set集合
        Integer removeKey = minFreqKeysSet.iterator().next();   //  获取需要移除的 key
        keyToVal.remove(removeKey);   //  将key对应的val移除
        keyToFreq.remove(removeKey);    //  将key对应的freq移除
        minFreqKeysSet.remove(removeKey);   //  将set集合中对应的key移除
        if (minFreqKeysSet.isEmpty()) {   //  如果此时set集合大小为0，则移除
            freqToKeys.remove(minFreq);
        }
    }
}
```

PS：特别注意，在 removeMinFreqKey() 方法中最后一行去除 freqToKeys 中的 minFreq 后不需要更新 minFreq 的值，因为该方法只在 put() 中使用过，而使用之后就更新了 minFreq 的值，所有不需要在方法最后重复更新了。

> <p align="right">2023.1.9</p>
