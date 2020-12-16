---
layout: pages
---

*  目录
{:toc}
hashmap  currenthashmap



根据负载因子扩容



|                |                        | 加锁            |
| -------------- | ---------------------- | --------------- |
| hashmap        | 数组+链表//数组+红黑树 |                 |
| currenthashmap | 数组+链表//数组+红黑树 | 分段-->CAS+sync |
|                |                        |                 |

```
https://crossoverjie.top/2018/07/23/java-senior/ConcurrentHashMap/
```

