# Introduction

Author: Biao \(Stefan\) He

Github: [hebiao064](https://github.com/hebiao064)

有套路，如果问最短，最少，BFS

如果问连通性，静态就是 DFS,BFS，动态就 UF

如果问依赖性就 topo sort

DAG 的问题就 dfs+memo

矩阵和 Array 通常都是 DP

问数量的通常都是 DP

问是否可以，也很有可能 DP

求所有解的，基本 backtracking

排序总是可以想一想的

再不行就数据结构头脑风暴

对了，别忘了还有分治这个好东西

其实从数据规模或者说要求的复杂度上也能看出解法

最小堆好好利用，往往可以把问题复杂度从 n^2 降为 n

如果遇到二维 dp 不会，先考虑一维情况如何解

**Basic C++ Skills**

```cpp
#include <iostream> // cin cout
```

```cpp
#include <climits> // for INT_MAX, INT_MIN maybe not required
#include <algorithm> // Sort
#include <queue> // queue and dequeue
#include <stack> // stack
#include <vector>
#include <string>
#include <utility> // pair
#include <unordered_map> 
#include <map> // map and multimap
#include <set> // set and multiset
#include <list>
#include <stdlib.h> // rand
```

取pair

```cpp
pair<int, int> a = make_pair(1,2);
a.first;
a.second;
```

取list

```cpp
list<Node*>::iterator it;
*it->key;
*it->value;

map::iterator
it->first
it->second
```

priority\_queue

```cpp
priority_queue<int, vector<int>, cmp> pq;
// cmp is comparator, default is less<T>, for maxheap

1. Struct or Class 一定要initialize再传进去
struct cmp {
    bool operator() (pair<int, int> &a, pair<int,int> &b) {
        return a.second < b.second;
    }
} cmp;


2. method的话，如果在class里一定要加static，在class外不用
static bool cmp (Interval a, Interval b) {
    return a.start < b.start;
}
```

Getline usage:

```cpp
#include <sstream>
stringstream ss(path);
while (getline(ss,tmp,'/')) {
    // then we can get the split single element one by one
}
```

Iterator:

```cpp
容器         支持的迭代器类     include
vector          随机访问       vector                         
set               双向         set                                    
multimap          双向         map                           
deque           随机访问       deque
multiset          双向         set
stack            不支持        stack
list              双向         list
map               双向          map
queue            不支持        queue
priority_queue   不支持        queue

*it 用于set list 这种一对一容器
it->first, it->second 用于 一对多容器
```



