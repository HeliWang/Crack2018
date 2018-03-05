Merge Intervals:

```cpp
static bool cmp(Interval& a, Interval& b) {
    return a.start < b.start;
}

vector<Interval> merge(vector<Interval>& intervals) {
    vector<Interval> res;
    if (intervals.size() == 0) return res;
    sort(intervals.begin(), intervals.end(), cmp);
    res.push_back(intervals[0]);
    for (int i = 1; i < intervals.size(); i++) {
        if (intervals[i].start <= res.back().end) {
            Interval elem(res.back().start, max(intervals[i].end, res.back().end));
            res.pop_back();
            res.push_back(elem);
        } else {
            res.push_back(intervals[i]);
        }
    }
    return res;
}
```

Why Yelp

[Yelp.com](http://Yelp.com)

Put vs Post: 

POST: Used to modify and update a resource

PUT: Used to create a resource, or overwrite it. While you specify the resources new URL.

PUT is idempotent, so if you PUT an object twice, it has no effect. This is a nice property, so I would use PUT when possible.



