Top interview questions asked by Microsoft as voted by the community.

We compile this list thoroughly so you can save time and get well-prepared for a Microsoft interview.

Completing this card should give you a good idea of the type of questions you would encounter in your Microsoft interview.

```cpp
#include <iostream> // cin cout
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

```
pair<int, int> a = make_pair(1,2);
a.first;
a.second;
```

取list

```
list<Node*>::iterator it;
*it->key;
*it->value;
```

priority\_queue

```
priority_queue<int, vector<int>, cmp> pq;
// cmp is comparator, default is less<T>, for maxheap

struct cmp {
    bool operator() (pair<int, int> &a, pair<int,int> &b) {
        return a.second < b.second;
    }
};
```

Getline usage:

```cpp
#include <sstream>
stringstream ss(path);
while (getline(ss,tmp,'/')) {
    // then we can get the split single element one by one
}
```



