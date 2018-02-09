599. Minimum Index Sum of Two Lists

```cpp
vector<string> findRestaurant(vector<string>& list1, vector<string>& list2) {
    unordered_map<string, int> mp;
    int mn = INT_MAX;
    vector<string> res;
    for (int i = 0; i < list1.size(); i++) mp[list1[i]] = i;
    for (int j = 0; j < list2.size(); j++) {
        if (mp.count(list2[j]) > 0) {
            if (j + mp[list2[j]] < mn) {
                res.clear();
                mn = j + mp[list2[j]];
                res.push_back(list2[j]);
            } 
            else if (j + mp[list2[j]] == mn) {
                res.push_back(list2[j]);
            }
        }
    }
    return res;
}
```

**1 CSS应该在HTML的头部还是body尾？ （head）**

**2 div是inline还是block？ （block）**

**3 CSS是declarative还是imperative? （declarative）**

**4 实现圆角的CSS属性 （border-radius）**

**5 what function can be called to re-assign the "this" keyword in a function \(any one is sufficient\)?  （求解，这个真不知道）**

**6 页面所有assets都加载完之后会触发哪个JavaScript事件, DOMContentLoaded or load? （load）**

The`DOMContentLoaded`event will fire as soon as the DOM hierarchy has been fully constructed, the`load`event will do it when all the images and sub-frames have finished loading.

**7 没有CSRF保护的怕哪个，XSS / Phishing / Man in the middle? （XSS） （求确认）**

**8 在http POST request中没有被加密的是：domain / query / headers / body / none of above? （headers） （求确认）**

**9 What compression is typically used to compress a HTTP request? （gzip） （求确认）**

Nowadays, only two are relevant:`gzip`, the most common one, and`br`the new challenger.

**10 添加数据的SQL命令 add / append / update / insert? \(insert\)**

**11 SQL inner join -&gt; intersect / union / difference? \(intersect\)**

**12 Python哪个是immutable -&gt; list / tuple / dictionary? \(tuple\)**

**13 TDD是什么? \(test-driven development\)**

**14 JavaScript哪个创建实例更快？  （用prototype的）**

**15 Command to determine CPU/Memory load on a unix machine? \(vmstat\) （求确认）**

**16 JavaScript声明变量时没用var会怎么样？ syntax error / 变global / scoped to block/ scoped to function / runtime undefined function （我选的最后一个，求确认）**

https://segmentfault.com/a/1190000000638445

**18 任意语言，full binary tree中有多少个节点？ 答案需要是一行mathematical equation。**

**19 JavaScript，实现getElementsByClassName。输入输出都给好了，json结构也给好了，给了两个test。用dfs。**

