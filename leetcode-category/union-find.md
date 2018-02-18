

[http://blog.csdn.net/dm\_vincent/article/details/7655764](http://blog.csdn.net/dm_vincent/article/details/7655764)

Union Find

应用场景：在解决连通图问题，比如还有多少个孤岛，尤其在动态连通图的时候非常适合，因为可以O\(1\)时间insert 或者 remove岛屿。



建立方式：

private:

      一个count计算连通图数量

      一个parent array 存每个node的终极parentId

      一个size array 存此个node为root的子树大小

public:

      UnionFind\(\) {}  // 初始化

      void add\(int index\) {}

      void unite\(int p, int q\) {}

      int find\(int index\) {}

      int getCount\(\) {}





Code:

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
```



