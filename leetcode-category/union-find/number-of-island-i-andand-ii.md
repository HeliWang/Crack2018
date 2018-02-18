# Number of Islands

Given a 2d grid map of`'1'`s \(land\) and`'0'`

s \(water\), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

```
11110
11010
11000
00000
```

Answer: 1

**Example 2:**

```
11000
11000
00100
00011
```

Answer: 3

**Solution**: DFS

```cpp
int numIslands(vector<vector<char>>& grid) {
    if (grid.size() == 0 || grid[0].size() == 0) return 0;
    int res = 0;
    for (int i = 0; i < grid.size(); i++) {
        for (int j = 0; j < grid[0].size(); j++) {
            if (grid[i][j] == '1') {
                res++;
                clearSurrounding(grid, i, j);
            }
        }
    }
    return res;
}

void clearSurrounding(vector<vector<char>>& grid, int i, int j) {
    grid[i][j] = '0';
    if (i > 0 && grid[i-1][j] == '1') clearSurrounding(grid, i-1, j);
    if (j > 0 && grid[i][j-1] == '1') clearSurrounding(grid, i, j-1);
    if (i < grid.size() - 1 && grid[i+1][j] == '1') clearSurrounding(grid, i+1, j);
    if (j < grid[0].size() - 1 && grid[i][j + 1] == '1') clearSurrounding(grid, i, j + 1);
}
```

# Number of Islands II

A 2d grid map of`m`rows and`n`columns is initially filled with water. We may perform an add Land operation which turns the water at position \(row, col\) into a land. Given a list of positions to operate, **count the number of islands after each addLand operation**. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Solution**:

```cpp
class UnionFind {
private:
    int count;
    vector<int> root;
    vector<int> sz;
public:
    UnionFind(int n) {
        count = 0;
        root.resize(n, -1);
        sz.resize(n, 0);
    }

    int getCount() {
        return count;
    }

    void add(int i) {
        root[i] = i;
        sz[i] = 1;
        count++;
    }

    int find(int i) {
        if (root[i] == -1) return -1;
        while (root[i] != root[root[i]]) {
            root[i] = root[root[i]];
        }
        return root[i];
    }

    void unite(int p, int q) {
        int pId = find(p), qId = find(q);
        if (pId == qId) return;
        if (sz[pId] < sz[qId]) swap(pId, qId);
        sz[pId] += sz[qId];
        root[qId] = pId;
        count--;
    }
};

class Solution {
public:
    vector<int> numIslands2(int m, int n, vector<pair<int, int>>& positions) {
        UnionFind uf(m * n);
        vector<vector<int> > directions = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};
        vector<int> res;
        for (auto x: positions) {
            int index = x.first * n + x.second;
            uf.add(index);
            for (auto y: directions) {
                if (x.first + y[0] >= 0 && x.first + y[0] < m && x.second + y[1] >= 0 && x.second + y[1] < n) {
                    int newIndex = (x.first + y[0]) * n + x.second + y[1];
                    if (uf.find(newIndex) != -1) {
                        uf.unite(index, newIndex);
                    }
                }
            }
            res.push_back(uf.getCount());
        }
        return res;
    }
};
```



