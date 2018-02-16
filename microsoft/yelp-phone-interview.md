Find Kth Most Common String

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <unordered_map>
#include <utility>
#include <queue>
using namespace std;

bool cmp (pair<string, int> &a, pair<string, int> &b) {
	return a.second > b.second;
}

string findKthCommonString (vector<string>& strList, int k) {
	unordered_map<string, int> mp;
	for (auto x: strList) {
		mp[x]++;
	};

	priority_queue<pair<string, int> > pq;
	for (auto it = mp.begin(); it != mp.end(); it++) {
		if (pq.size() < k || it->second > pq.top().second) {
			pq.push(make_pair(it->first, it->second));
			if (pq.size() > k) pq.pop();
		}
	}

	return pq.top().first;
}

int main() {
	vector<string> strList = {"hello", "hello", "world"};
	cout << findKthCommonString(strList, 1);
	return 0;
}
```



