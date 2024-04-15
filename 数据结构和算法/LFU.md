# LFU
请你为 最不经常使用（LFU）缓存算法设计并实现数据结构。

实现 LFUCache 类：

LFUCache(int capacity) - 用数据结构的容量 capacity 初始化对象
int get(int key) - 如果键存在于缓存中，则获取键的值，否则返回 -1。
void put(int key, int value) - 如果键已存在，则变更其值；如果键不存在，请插入键值对。当缓存达到其容量时，则应该在插入新项之前，使最不经常使用的项无效。在此问题中，当存在平局（即两个或更多个键具有相同使用频率）时，应该去除 最近最久未使用 的键。
注意「项的使用次数」就是自插入该项以来对其调用 get 和 put 函数的次数之和。使用次数会在对应项被移除后置为 0 。

为了确定最不常使用的键，可以为缓存中的每个键维护一个 使用计数器 。使用计数最小的键是最久未使用的键。

当一个键首次插入到缓存中时，它的使用计数器被设置为 1 (由于 put 操作)。对缓存中的键执行 get 或 put 操作，使用计数器的值将会递增。

## 方法一：哈希表 + 平衡二叉树
```java
class LFUCache {
    // 缓存容量，时间戳
    int capacity, time;
    Map<Integer, Node> key_table;
    TreeSet<Node> S;

    public LFUCache(int capacity) {
        this.capacity = capacity;
        this.time = 0;
        key_table = new HashMap<Integer, Node>();
        S = new TreeSet<Node>();
    }
    
    public int get(int key) {
        if (capacity == 0) {
            return -1;
        }
        // 如果哈希表中没有键 key，返回 -1
        if (!key_table.containsKey(key)) {
            return -1;
        }
        // 从哈希表中得到旧的缓存
        Node cache = key_table.get(key);
        // 从平衡二叉树中删除旧的缓存
        S.remove(cache);
        // 将旧缓存更新
        cache.cnt += 1;
        cache.time = ++time;
        // 将新缓存重新放入哈希表和平衡二叉树中
        S.add(cache);
        key_table.put(key, cache);
        return cache.value;
    }
    
    public void put(int key, int value) {
        if (capacity == 0) {
            return;
        }
        if (!key_table.containsKey(key)) {
            // 如果到达缓存容量上限
            if (key_table.size() == capacity) {
                // 从哈希表和平衡二叉树中删除最近最少使用的缓存
                key_table.remove(S.first().key);
                S.remove(S.first());
            }
            // 创建新的缓存
            Node cache = new Node(1, ++time, key, value);
            // 将新缓存放入哈希表和平衡二叉树中
            key_table.put(key, cache);
            S.add(cache);
        } else {
            // 这里和 get() 函数类似
            Node cache = key_table.get(key);
            S.remove(cache);
            cache.cnt += 1;
            cache.time = ++time;
            cache.value = value;
            S.add(cache);
            key_table.put(key, cache);
        }
    }
}

class Node implements Comparable<Node> {
    int cnt, time, key, value;

    Node(int cnt, int time, int key, int value) {
        this.cnt = cnt;
        this.time = time;
        this.key = key;
        this.value = value;
    }

    public boolean equals(Object anObject) {
        if (this == anObject) {
            return true;
        }
        if (anObject instanceof Node) {
            Node rhs = (Node) anObject;
            return this.cnt == rhs.cnt && this.time == rhs.time;
        }
        return false;
    }

    public int compareTo(Node rhs) {
        return cnt == rhs.cnt ? time - rhs.time : cnt - rhs.cnt;
    }

    public int hashCode() {
        return cnt * 1000000007 + time;
    }
}
```
## 方法二：双哈希表
```java
class LFUCache {
    int minfreq, capacity;
    Map<Integer, Node> key_table;
    Map<Integer, LinkedList<Node>> freq_table;

    public LFUCache(int capacity) {
        this.minfreq = 0;
        this.capacity = capacity;
        key_table = new HashMap<Integer, Node>();;
        freq_table = new HashMap<Integer, LinkedList<Node>>();
    }
    
    public int get(int key) {
        if (capacity == 0) {
            return -1;
        }
        if (!key_table.containsKey(key)) {
            return -1;
        }
        Node node = key_table.get(key);
        int val = node.val, freq = node.freq;
        freq_table.get(freq).remove(node);
        // 如果当前链表为空，我们需要在哈希表中删除，且更新minFreq
        if (freq_table.get(freq).size() == 0) {
            freq_table.remove(freq);
            if (minfreq == freq) {
                minfreq += 1;
            }
        }
        // 插入到 freq + 1 中
        LinkedList<Node> list = freq_table.getOrDefault(freq + 1, new LinkedList<Node>());
        list.offerFirst(new Node(key, val, freq + 1));
        freq_table.put(freq + 1, list);
        key_table.put(key, freq_table.get(freq + 1).peekFirst());
        return val;
    }
    
    public void put(int key, int value) {
        if (capacity == 0) {
            return;
        }
        if (!key_table.containsKey(key)) {
            // 缓存已满，需要进行删除操作
            if (key_table.size() == capacity) {
                // 通过 minFreq 拿到 freq_table[minFreq] 链表的末尾节点
                Node node = freq_table.get(minfreq).peekLast();
                key_table.remove(node.key);
                freq_table.get(minfreq).pollLast();
                if (freq_table.get(minfreq).size() == 0) {
                    freq_table.remove(minfreq);
                }
            }
            LinkedList<Node> list = freq_table.getOrDefault(1, new LinkedList<Node>());
            list.offerFirst(new Node(key, value, 1));
            freq_table.put(1, list);
            key_table.put(key, freq_table.get(1).peekFirst());
            minfreq = 1;
        } else {
            // 与 get 操作基本一致，除了需要更新缓存的值
            Node node = key_table.get(key);
            int freq = node.freq;
            freq_table.get(freq).remove(node);
            if (freq_table.get(freq).size() == 0) {
                freq_table.remove(freq);
                if (minfreq == freq) {
                    minfreq += 1;
                }
            }
            LinkedList<Node> list = freq_table.getOrDefault(freq + 1, new LinkedList<Node>());
            list.offerFirst(new Node(key, value, freq + 1));
            freq_table.put(freq + 1, list);
            key_table.put(key, freq_table.get(freq + 1).peekFirst());
        }
    }
}

class Node {
    int key, val, freq;

    Node(int key, int val, int freq) {
        this.key = key;
        this.val = val;
        this.freq = freq;
    }
}
```

# 文章参考
- https://leetcode-cn.com/problems/lfu-cache/solution/lfuhuan-cun-by-leetcode-solution/