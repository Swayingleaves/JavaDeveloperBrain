# 常考的算法题

## 206. 反转链表
https://leetcode.cn/problems/reverse-linked-list/description/

给你单链表的头节点 head ，请你反转链表，并返回反转后的链表。
 

示例 1：


输入：head = [1,2,3,4,5]

输出：[5,4,3,2,1]

示例 2：


输入：head = [1,2]

输出：[2,1]

示例 3：

输入：head = []

输出：[]
 

提示：

- 链表中节点的数目范围是 [0, 5000]
- -5000 <= Node.val <= 5000

迭代法
```java
public ListNode reverseList(ListNode head) {
    ListNode prev = null; // 前一个节点
    ListNode curr = head; // 当前节点
    while (curr != null) { // 当当前节点不为空时继续遍历
        ListNode nextTemp = curr.next; // 暂存当前节点的下一个节点
        curr.next = prev; // 当前节点指向前一个节点，实现反转
        prev = curr; // 将当前节点变成前一个节点，为下一轮循环做准备
        curr = nextTemp; // 移动到下一个节点
    }
    return prev; // 返回反转后的头节点
}
```

递归法
```java
public ListNode reverseList(ListNode head) {
    if (head == null || head.next == null) { // 递归终止条件：链表为空或只有一个节点，直接返回原链表或头节点自身
        return head;
    }
    ListNode p = reverseList(head.next); // 递归调用反转下一个子链表
    head.next.next = head; // 将当前节点的下一个节点的next指向当前节点，实现指针反转
    head.next = null; // 将当前节点的next置空，避免与原链表相连
    return p; // 返回反转后的头节点（原本是尾节点）
}
```

## 146. LRU缓存机制
https://leetcode.cn/problems/lru-cache/description/

请你设计并实现一个满足  LRU (最近最少使用) 缓存 约束的数据结构。

实现 LRUCache 类：

LRUCache(int capacity) 以 正整数 作为容量 capacity 初始化 LRU 缓存

int get(int key) 如果关键字 key 存在于缓存中，则返回关键字的值，否则返回 -1 。

void put(int key, int value) 如果关键字 key 已经存在，则变更其数据值 value ；如果不存在，则向缓存中插入该组 key-value 。如果插入操作导致关键字数量超过 capacity ，则应该 逐出 最久未使用的关键字。

函数 get 和 put 必须以 O(1) 的平均时间复杂度运行。

 

示例：

输入

["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]

[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]

输出

[null, null, null, 1, null, -1, null, -1, 3, 4]

解释
- LRUCache lRUCache = new LRUCache(2);
- lRUCache.put(1, 1); // 缓存是 {1=1}
- lRUCache.put(2, 2); // 缓存是 {1=1, 2=2}
- lRUCache.get(1);    // 返回 1
- lRUCache.put(3, 3); // 该操作会使得关键字 2 作废，缓存是 {1=1, 3=3}
- lRUCache.get(2);    // 返回 -1 (未找到)
- lRUCache.put(4, 4); // 该操作会使得关键字 1 作废，缓存是 {4=4, 3=3}
- lRUCache.get(1);    // 返回 -1 (未找到)
- lRUCache.get(3);    // 返回 3
- lRUCache.get(4);    // 返回 4
 

提示：

- 1 <= capacity <= 3000
- 0 <= key <= 10000
- 0 <= value <= 10^5
- 最多调用 2 * 10^5 次 get 和 put

```java
class LRUCache {

    static class Node{
        int key;
        int value;
        Node pre;
        Node next;

        public Node(){

        }
        public Node(int key,int value){
            this.key = key;
            this.value = value;
        }
    }

    Map<Integer,Node> map = new HashMap<>();
    Node head,tail;
    int size;
    int cap;

    public LRUCache(int capacity) {
        this.cap = capacity;
        head = new Node();
        tail = new Node();
        head.next = tail;
        tail.pre = head;
    }
    
    public int get(int key) {
        Node n = map.get(key);
        if(n == null){
            return -1;
        }
        moveToHead(n);
        return n.value;
    }
    
    public void put(int key, int value) {
        Node n = map.get(key);
        if(n == null){
            Node node = new Node(key,value);
            map.put(key,node);
            addToHead(node);
            if(++size > cap){
                Node re = removeTail();
                map.remove(re.key);
            }
        }else{
            n.value = value;
            moveToHead(n);
        }
    }

    public Node remove(Node n){
        n.next.pre = n.pre;
        n.pre.next = n.next;
        return n;
    }

    public Node removeTail(){
        Node n = tail.pre;
        remove(n);
        return n;
    }

    public void addToHead(Node n){
        n.next = head.next;
        n.pre = head;
        head.next.pre = n;
        head.next = n;
        
    }

    public void moveToHead(Node n){
        remove(n);
        addToHead(n);
    }
}

/**
 * Your LRUCache object will be instantiated and called as such:
 * LRUCache obj = new LRUCache(capacity);
 * int param_1 = obj.get(key);
 * obj.put(key,value);
 */
```

