# Number of Connected Components in an Undirected Graph

Given`n`nodes labeled from`0`to`n - 1`and a list of undirected edges \(each edge is a pair of nodes\), write a function to find the number of connected components in an undirected graph.



**Solution:**

```cpp
class UnionFind {
private:
    int count;
    vector<int> root;
    vector<int> sz;
public:
    UnionFind(int n) {
        count = 0;
    }
    int getCount() {
        return count;
    }
    
    void add(int i) {
        root.push_back(i);
        sz.push_back(1);
        count++;
    }
    
    int find(int i) {
        while (root[i] != root[root[i]]) {
            root[i] = root[root[i]];
        }
        return root[i];
    }
    
    void unite(int p, int q) {
        int pId = find(p);
        int qId = find(q);
        if (pId == qId) return;
        if (sz[p] < sz[q]) swap(pId,qId);
        sz[pId] += sz[qId];
        root[qId] = pId;
        count--;
    }
};

class Solution {
public:
    int countComponents(int n, vector<pair<int, int>>& edges) {
        UnionFind uf(n);
        for (int i = 0; i < n; i++) uf.add(i);
        for (auto x: edges) {
            uf.unite(x.first, x.second);
        }
        return uf.getCount();
    }
};
```



