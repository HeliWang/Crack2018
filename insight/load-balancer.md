[https://www.quora.com/What-is-a-load-balancer](https://www.quora.com/What-is-a-load-balancer)

[https://www.jianshu.com/p/90a07f0eb878](https://www.jianshu.com/p/90a07f0eb878)

Def: A load balancer is a device that acts as a reverse proxy and distributes network or application traffic across a number of servers.

For what: Load balancers are used to increase capacity \(concurrent users\) and reliability of applications.

Zynga GWF use Elastic Load Balance to split traffic

\* Round robin

\* Weighted round robin

\* Least connections

\* Least response time

\*Random

**Random Solution:**

Idea:

```
LC 380
insert remove getRandom 都是O(1)
表明新加服务器 删除服务器 得到Node都是常数时间
用一个cache array来存有多少个服务器，这样随机O(1)得到保证
如果新增就push_back
如果删除就需要用到hashmap找到index，将其替换成cache.back() 然后pop_back()
其实就是替换删除
```

Code:

```cpp
class RandomizedSet {
private:
    vector<int> cache;
    unordered_map<int, int> mp;
public:
    /** Initialize your data structure here. */
    RandomizedSet() {

    }

    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    bool insert(int val) {
        if (mp.count(val) == 0) {
            cache.push_back(val);
            mp[val] = cache.size() - 1;
            return true;
        }
        return false;
    }

    /** Removes a value from the set. Returns true if the set contained the specified element. */
    bool remove(int val) {
        if (mp.count(val) > 0) {
            int pos = mp[val];
            cache[pos] = cache.back();
            mp[cache.back()] = pos;
            cache.pop_back();
            mp.erase(val);
            return true;
        }
        return false;
    }

    /** Get a random element from the set. */
    int getRandom() {
        int randomPos = rand() % cache.size();
        return cache[randomPos];
    }
};
```

Weighted Round Robin:

```cpp
class LoadBalancer {  // Round Robin
private:
    vector<pair<int, int> > cache;
    vector<int> presum;
    int total;
    int curSum;
    int index;

public:
    LoadBalancer () {
        total = 0;
        index = 0;
        curSum = -1;
    }

    void add(int capacity) {
        cache.push_back(make_pair(cache.size(), capacity));
        total += capacity;
        presum.push_back(total);
    }

    int dispatch() {
        curSum = curSum % total + 1;
        index = index % cache.size();
        if (curSum < presum[index]) {
            return cache[index].first;
        }
        else {
            index++;
        }
        return cache[index].first;
    }
};
```



