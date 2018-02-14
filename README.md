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
#include <climits> // for INT_MAX, INT_MIN
#include <algorithm> // Sort
#include <queue>
#include <stack>
#include <vector>
#include <string>
#include <priority_queue>
#include <unordered_map>
#include <map>
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
```

priority\_queue

```cpp
priority_queue<int, vector<int>, cmp> pq;
// cmp is comparator, default is less<T>, for maxheap

struct cmp {
    bool operator() (pair<int, int> &a, pair<int,int> &b) {
        return a.second < b.second;
    }
} cmp;

or

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



