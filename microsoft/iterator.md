# [Flatten 2D Vector](https://leetcode.com/problems/flatten-2d-vector/)

```cpp
// Solution 1
用一个array来存




// Solution 2
class Vector2D {
private:
    int x, y;
    vector<vector<int>> v;
public:
    Vector2D(vector<vector<int>>& vec2d) {
        x = 0;
        y = 0;
        v = vec2d;
    }

    int next() {
        return v[x][y++];
    }

    bool hasNext() {
        while(x < v.size() && y == v[x].size()) {
            x++; 
            y = 0;
        }
        return x < v.size();
    }
};

/**
 * Your Vector2D object will be instantiated and called as such:
 * Vector2D i(vec2d);
 * while (i.hasNext()) cout << i.next();
 */
```

# Zigzag Iterator

```cpp
// Solution 1
class ZigzagIterator {
private:
    vector<int> v;
    int i;
public:
    ZigzagIterator(vector<int>& v1, vector<int>& v2) {
        int m = v1.size();
        int n = v2.size();
        i = 0;
        int index = 0;
        while (index < max(m,n)) {
            if (index < v1.size()) v.push_back(v1[index]);
            if (index < v2.size()) v.push_back(v2[index]);
            index++;
        }
    }

    int next() {
        return v[i++];
    }

    bool hasNext() {
        return i < v.size();
    }
};



//Solution 2:
class ZigzagIterator {
public:
    ZigzagIterator(vector<int>& v1, vector<int>& v2) {
        if (!v1.empty()) q.push(make_pair(v1.begin(), v1.end()));
        if (!v2.empty()) q.push(make_pair(v2.begin(), v2.end()));
    }
    int next() {
        auto it = q.front().first, end = q.front().second;
        q.pop();
        if (it + 1 != end) q.push(make_pair(it + 1, end));
        return *it;
    }
    bool hasNext() {
        return !q.empty();
    }
private:
    queue<pair<vector<int>::iterator, vector<int>::iterator>> q;
};
```

# Flatten Nested List Iterator

Idea:

用一个stack，每次hasnext的时候把栈顶的元素pop出来，如果是数字就直接压进去，如果是list的话就从尾到头压进来



```cpp
class NestedIterator {
private:
    stack<NestedInteger> st;
public:
    NestedIterator(vector<NestedInteger> &nestedList) {
        for (int i = nestedList.size() - 1; i >= 0; i--) {
            st.push(nestedList[i]);
        }
    }

    int next() {
        int res = st.top().getInteger();
        st.pop();
        return res;
    }

    bool hasNext() {
        if (st.empty()) return false;
        NestedInteger cur = st.top();
        st.pop();
        if (cur.isInteger()) {
            st.push(cur);
            return true;
        }
        vector<NestedInteger> nestedList = cur.getList();
        for (int i = nestedList.size() - 1; i >= 0; i--) {
            st.push(nestedList[i]);
        } 
        return hasNext();
    }
};
```



