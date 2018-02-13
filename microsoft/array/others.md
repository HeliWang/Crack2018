1. Single Number
2. Roman to Integer
3. Excel Sheet Column Number 
4. Find the Celebrity
5. Integer to English Words
6. The Skyline Problem

# 1. Single Number

```cpp
int singleNumber(vector<int>& nums) {
    int res = 0;
    for (int i = 0; i < nums.size(); i++) {
        res ^= nums[i];
    }
    return res;
}
```



# 2. Roman to Integer

```cpp
int romanToInt(string s) {
    int result = 0;
    unordered_map<char, int> mp = {{'M', 1000},{'D', 500},{'C', 100},{'L', 50},{'X', 10},{'V', 5},{'I', 1}};
    for (int i = 0; i < s.length(); i++) {
        int num = mp[s[i]];
        int indicator = 1;
        if (i < s.length() - 1 && mp[s[i]] < mp[s[i+1]]) {
            indicator = -1;
        }
        result += num * indicator;
    }
    return result;
}

string intToRoman(int num) {
    vector<string> dict = {"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};
    vector<int> val = {1000,900,500,400,100,90,50,40,10,9,5,4,1};
    string result = "";
    for (int i = 0; i < val.size(); i++) {
        int count = num / val[i];
        num %= val[i];
        for (int j = 0; j < count; j++) {
            result += dict[i];
        }
    }
    return result;
}
```

# 3. Excel Sheet Column Number

```cpp
int titleToNumber(string s) {
    int res = 0;
    for (int i = 0; i < s.length(); i++) {
        res = res * 26 + s[i] - 'A' + 1;
    }
    return res;
}
```

# 4. Find the Celebrity

```cpp
int findCelebrity(int n) {
    if (n == 1) return -1;
    int i = 0, j = 1;
    while (j < n) {
        if (knows(i,j)) {
            i = j;
        }
        j++;
    }
    int k = 0;
    while (k < n) {
        if (k != i) {
            if (!knows(k, i) || knows(i, k)) return -1;
        }
        k++;
    }
    return i;
}
```

# 5. Integer to English Words

```cpp
string numberToWords(int num) {
    if (num == 0) return "Zero";
    vector<string> thousandStr = {"Billion ", "Million ", "Thousand ", ""};
    vector<int> thousandNum = {1000000000, 1000000, 1000, 1};
    string res;
    for (int i = 0; i < thousandNum.size(); i++) {
        if (num >= thousandNum[i]) {
            int temp = num / thousandNum[i];
            res += helper(temp) + thousandStr[i];
            num = num % thousandNum[i];
        }
    }
    if (res.back() == ' ') res.pop_back();
    return res;
}

string helper(int num) {
    string res;
    vector<string> one({"","One ", "Two ", "Three ", "Four ", "Five ", "Six ", "Seven ", "Eight ", "Nine ","Ten ", "Eleven ", "Twelve ", "Thirteen ", "Fourteen ", "Fifteen ", "Sixteen ", "Seventeen ", "Eighteen ", "Nineteen "});
    vector<string> twenty({"","","Twenty ","Thirty ","Forty ","Fifty ","Sixty ","Seventy ","Eighty ","Ninety "});
    if (num >= 100) {
        res += one[num / 100];
        res += "Hundred ";
        num = num % 100;
    }
    if (num >= 20) {
        res += twenty[num / 10];
        res += one[num % 10];
    }
    else {
        res += one[num];
    }
    return res;
}
```

# 6. The Skyline Problem

**Idea:**

```
先讲做法，将building的(start，-h)和(end, h) 放入vector，然后根据first来排序
然后for loop，遇到-h时放入multiset中，遇到h时则将其删除，表示矩阵已经走完了
multiset中的最大高度如果发生变化，则push_back到结果array中去。

理由：
相当于在图上做垂直扫描，遇到start则入set，反之弹出set，如果set中的最大高度发生变化，则记录到结果中去
```

**Solution:**

```cpp
struct cmp {
    bool operator() (pair<int, int> &a, pair<int, int> &b) {
        return a.first < b.first;
    }
} cmp;

vector<pair<int, int>> getSkyline(vector<vector<int>>& buildings) {
    vector<pair<int, int>> res; // store the result
    multiset<int> m;            // store the height, and output the highest height 
    vector<pair<int,int>> h;    // store those [start, -height], [end, height]  
    for (int i = 0; i < buildings.size(); i++) {
        h.push_back({buildings[i][0], 0 - buildings[i][2]});
        h.push_back({buildings[i][1], buildings[i][2]});
    }
    sort(h.begin(), h.end(), cmp);
    int pre = 0, cur = 0;
    m.insert(0);
    for (int i = 0; i < h.size(); i++) {
        if (h[i].second < 0) m.insert(-h[i].second);
        else m.erase(m.find(h[i].second));
        cur = *m.rbegin();
        if (pre != cur) {
            res.push_back({h[i].first, cur});
            pre = cur;
        }
    }
    return res;
}
```



