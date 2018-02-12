1. Two Sum : for 循环里，用一个hashmap来记录\(key 为arr\[i\], value 为i\)，同时判断target - curVal在不在hashmap里

2. Valid String Palindrome:** Two Pointer**, 注意用find\__first\_not\_of\(" "\), find\_last\_not\_of\(" "\), isalnum\(\)_

3. String to Integer \(atoi\): 注意indicator作符号，溢出直接返回INT_MAX, INT\__MIN

4. Reverse String: swap\(s\[i\], s\[j\]\) **Two Pointer**

5. Reverse Words in a String: 先整体reverse, 再通过空格区分，再一个个word reverse

6. Reverse Words in a String II: 没有leading trailing zeros，更加简单

7. Valid Parentheses: Stack存左括号，碰到右括号就去匹配

8. Longest Palindromic Substring: 姊妹题LP Subsequence, DP来解决, base case差不多, dp\[i\]\[j\] = dp\[i+1\]\[j-1\] + 2 if 左右相等并且dp\[i+1\]\[j-1\] != 0, Subsequence 的话: dp\[i\]\[j\] = dp\[i+1\]\[j-1\] + 2 不用判断别的

9. Group Anagrams: Hashmap存这个anagram在vector的第几层

10. Trapping Rain Water: 经典题，找到最高处，然后左到右扫一遍，右到左扫一遍，有diff就相加

11. Set Matrix Zeroes: 用第一个0的行列做存储，然后对应的去置零，最后把这一列置零

12. Rotate Image: 先对折，再45度旋转，通过i 和 j的颠倒变换

13. Spiral Matrix: 4 pointers, Two pointer的变种，记得在中场休息时判断是否该return



# 1. Two Sum

Given an array of integers, return**indices**of the two numbers such that they add up to a specific target.

You may assume that each input would have**exactly**one solution, and you may not use thesameelement twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

**Solution:**

```cpp
vector<int> twoSum(vector<int>& nums, int target) {
    unordered_map<int, int> mp;
    vector<int> res;
    mp[nums[0]] = 0;
    for (int i = 1; i < nums.size(); i++) {
        if (mp.count(target - nums[i]) > 0) {
            vector<int> res1({mp[target - nums[i]], i});
            return res1;
        }
        mp[nums[i]] = i;
    }
    return res;
}
```

# 2. Valid Palindrome

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

For example,  
`"A man, a plan, a canal: Panama"`is a palindrome.  
`"race a car"`isnota palindrome.

**Note:**  
Have you consider that the string might be empty? This is a good question to ask during an interview.

For the purpose of this problem, we define empty string as valid palindrome.

**Solution:**

```cpp
bool isPalindrome(string s) {
    int i = s.find_first_not_of(" ");
    if (i > s.length()) return true;
    int j = s.find_last_not_of(" ");
    while (i < j) {
        if (!isalnum(s[i])) i++;
        else if (!isalnum(s[j])) j--;
        else if (tolower(s[i]) != tolower(s[j])) return false;
        else {
            i++;j--;
        }
    }
    return true;
}
```

# 3. String to Integer \(atoi\)

Implement`atoi`to convert a string to an integer.

**Solution:**

```cpp
int myAtoi(string str) {
    long result = 0;
    int indicator = 1;
    int flag = 0;
    for(int i = 0; i<str.size();)
    {
        i = str.find_first_not_of(' ');
        while (str[i] == '-' || str[i] == '+') {
            indicator = (str[i++] == '-')? -1 : 1;
            flag++;
        }
        if (flag > 1) return 0;
        while(isdigit(str[i])) 
        {
            result = result*10 + (str[i++]-'0');
            if(result*indicator >= INT_MAX) return INT_MAX;
            if(result*indicator <= INT_MIN) return INT_MIN;                
        }
        return result*indicator;
    }
    return result*indicator;
}
```

# 4. Reverse String

Write a function that takes a string as input and returns the string reversed.

**Example:**  
Given s = "hello", return "olleh".

```cpp
string reverseString(string s) {
    int i = 0, j = s.length() - 1;
    while (i < j) {
        swap(s[i], s[j]);
        i++;
        j--;
    }
    return s;
}
```

# 5. Reverse Words in a String

Given an input string, reverse the string word by word.

For example,  
Given s = "`the sky is blue`",  
return "`blue is sky the`".

**Solution:**

```cpp
void reverseWords(string &s) {
    if (s.length() == 0) return;
    while(s[0] == ' ') {
        s.erase(s.begin());
    }
    while(s[s.length()-1] == ' ') {
        s.erase(s.end() - 1);
    }
    for (int i = 1;i < s.length();) {
        if(s[i]==' ' && s[i-1] == ' ') s.erase(i,1);
        else i++;
    }
    reverse(s.begin(),s.end());
    int left = 0;
    for (int i = 0;i < s.length();i++) {
        if (s[i] == ' ') {
            reverse(s.begin()+left,s.begin()+i);
            left = i + 1;
        }
    }
    reverse(s.begin()+left,s.end());
}
```

# **6. Reverse Words in a String II**

Given an input string, reverse the string word by word. A word is defined as a sequence of non-space characters.

The input string does not contain leading or trailing spaces and the words are always separated by a single space.

For example,  
Given s = "`the sky is blue`",  
return "`blue is sky the`".

**Solution:**

```cpp
void reverseWords(vector<char>& str) {
    reverse(str.begin(), str.end());
    int start = 0, end = -1;
    for (int i = 0; i < str.size(); i++) {
        if (str[i] == ' ') {
            end = i;
            reverseSingleWord(str, start, end - 1);
            start = i + 1;
        }
    }
    reverseSingleWord(str, start, str.size() - 1);
}

void reverseSingleWord(vector<char>& str, int start, int end) {
    while (start < end) {
        swap(str[start], str[end]);
        start++;
        end--;
    }
}
```

# 7. Valid Parentheses

Given a string containing just the characters`'('`,`')'`,`'{'`,`'}'`,`'['`and`']'`, determine if the input string is valid.

The brackets must close in the correct order,`"()"`and`"()[]{}"`are all valid but`"(]"`and`"([)]"`are not.

**Solution:**

```cpp
bool isValid(string s) {
    stack<char> stk;
    for (char x: s) {
        if (x == '(' || x == '[' || x == '{') stk.push(x);
        else if (x == ')') {
            if (stk.empty() || stk.top() != '(') {
                return false;
            }
            stk.pop();
        }
        else if (x == ']') {
            if (stk.empty() || stk.top() != '[') {
                return false;
            }
            stk.pop();
        }
        else if (x == '}') {
            if (stk.empty() || stk.top() != '{') {
                return false;
            }
            stk.pop();
        }
    }
    return stk.empty();
}
```

# 8. Longest Palindromic Substring & Subsequence

**Idea: **

```js
Dynamic Programming
Base Case: dp[i][i] = 1, dp[i][i+1] = s[i] == s[i+1] ? 1 : 0;
General Case:

if (s[i] != s[j]):
For Substring: dp[i][j] = 0 
For Subsequence: dp[i][j] = max(dp[i+1][j], dp[i][j-1])

if (s[i] == s[j]):
For Substring: dp[i][j] = dp[i+1][j-1] == 0 ? 0 :  dp[i+1][j-1] + 2
For Subsequence: dp[i][j] = dp[i+1][j-1] + 2

另外注意i,j的 for循环要求从 
1,2  2,3  3,4  4,5
1,3  2,4  3,5
1,4  2,5
1,5
倒三角进行 
for i start from 1 to len - 1
for j start from 0 to len - 1

left = j, right = j + i (j + i < len)
```

**Solution: **

```cpp
string longestPalindrome(string s) {
    int len = s.length();
    vector<vector<int>> dp(len, vector<int> (len, 0));
    int longestLength = 1;
    int startIndex = 0;
    for (int i = 0; i < len; i++) {
        dp[i][i] = 1;
    }
    for (int i = len - 1; i >= 0; i--) { // take "babad" as example, start from 4 to 0
        for (int j = 0; j < i; j++) { // start from 0 to i-1
            if (s[j] != s[j + len - i]) {
                dp[j][j + len - i] = 0;
            } else {
                if (len - i == 1) {
                    dp[j][j + len - i] = 2;
                } else {
                    dp[j][j + len - i] = dp[j + 1][j + len - i - 1] == 0 ? 0 : dp[j + 1][j + len - i - 1] + 2;
                }
                if (dp[j][j + len - i] > longestLength) {
                    longestLength = dp[j][j + len - i];
                    startIndex = j;
                }
            }
        }
    }
    return s.substr(startIndex, longestLength);
}

int longestPalindromeSubseq(string s) {
    int len = s.length();
    if (len <= 1) return len;
    int res = 0;
    vector<vector<int>> dp(len, vector<int>(len, 0));
    for (int i = 0; i < len; i++) {
        dp[i][i] = 1;
    }
    for (int i = len - 1; i >= 0; i--) {
        for (int j = 0; j < i; j++) {
            int left = j; // just to make it readable
            int right = j + len - i;
            if (s[left] != s[right]) {
                dp[left][right] = max(dp[left + 1][right], dp[left][right - 1]);
            } else {
                if (left + 1 == right) {
                    dp[left][right] = 2;
                } else {
                    dp[left][right] = dp[left + 1][right - 1] + 2;
                }
            }
            res = max(res, dp[left][right]);
        }
    }
    return res;
}
```

# 9. Group Anagrams

Given an array of strings, group anagrams together.

For example, given:`["eat", "tea", "tan", "ate", "nat", "bat"]`,  
Return:

```
[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

**Solution:**

```cpp
vector<vector<string>> groupAnagrams(vector<string>& strs) {
    vector<vector<string>> result;
    unordered_map<string, int> mp;
    int index = 0;
    for (int i = 0; i < strs.size(); i++) {
        string curr = strs[i];
        sort(curr.begin(), curr.end());
        if (mp.count(curr) > 0) {
            result[mp[curr]].push_back(strs[i]);
        } else {
            result.push_back(vector<string> ({strs[i]}));
            mp[curr] = index++;
        }
    }
    return result;
}
```

# 10. Trapping Rain Water

![](/assets/import_trapping_water.png)

**Solution:**

```cpp
int trap(vector<int>& height) {
    if (height.size() <= 2) return 0;
    int result = 0;
    int globalPeak = 0, gloablPeakIndex = 0;
    for (int i = 0; i < height.size(); i++) {
        if (height[i] > globalPeak) {
            globalPeak = height[i];
            gloablPeakIndex = i;
        }
    }
    // left to right
    int tempPeak = 0;
    for (int i = 0; i < gloablPeakIndex; i++) {
        if (height[i] > tempPeak) {
            tempPeak = height[i];
        } else result += tempPeak - height[i];
    }
    tempPeak = 0;
    for (int i = height.size() - 1; i > gloablPeakIndex; i--) {
        if (height[i] > tempPeak) {
            tempPeak = height[i];
        } else result += tempPeak - height[i];
    }
    return result;
}
```

# 11. Set Matrix Zeroes

**Solution: **

```cpp
void setZeroes(vector<vector<int>>& matrix) {
    // sanity check
    if (matrix.size() == 0) return;
    // find the target row and col
    int row = 0, col = 0;
    bool flag = true;
    for (int i = 0; i < matrix.size(); i++) {
        for (int j = 0; j < matrix[0].size(); j++) {
            if (matrix[i][j] == 0) {
                row = i; col = j; 
                flag = false;
                break;
            }
        }
    }
    
    if (flag) return;
    
    // Use the target row and col as temporary space
    for (int i = 0; i < matrix.size(); i++) {
        for (int j = 0; j < matrix[0].size(); j++) {
            if (matrix[i][j] == 0) {
                matrix[row][j] = 0;
                matrix[i][col] = 0;
            }
        }
    }
    
    // Then process the matrix using the known target row & col
    for (int i = 0; i < matrix.size(); i++) {
        for (int j = 0; j < matrix[0].size(); j++) {
            if (row == i || col == j) continue;
            if (matrix[row][j] == 0 || matrix[i][col] == 0) {
                matrix[i][j] = 0;
            }
        }
    }
    for (int i = 0; i < matrix.size(); i++) {
        matrix[i][col] = 0;
    }
    for (int j = 0; j < matrix[0].size(); j++) {
        matrix[row][j] = 0;
    }
    return;
}
```

# 12. Rotate Image

You are given annxn2D matrix representing an image.

Rotate the image by 90 degrees \(clockwise\).

**Solution:**

```cpp
void rotate(vector<vector<int>>& matrix) {
    // sanity check
    int n = matrix.size();
    if (!n) return;
    
    // Y axis first flip
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n / 2; j++) {
            swap(matrix[i][j], matrix[i][n - 1 - j]);
        }
    }
    
    // y = x, 45 degree flip
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n - i; j++) {
            swap(matrix[i][j], matrix[n - 1 - j][n - 1- i]);
        }
    }
    return;
}
```

# 13. Spiral Matrix

Given a matrix ofmxnelements \(mrows,ncolumns\), return all elements of the matrix in spiral order.

For example,  
Given the following matrix:

```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
```

You should return`[1,2,3,6,9,8,7,4,5]`

**Solution:**

```cpp
vector<int> spiralOrder(vector<vector<int>>& matrix) {
    vector<int> res;
    int m = matrix.size();
    if (m == 0) return res;
    int n = matrix[0].size();
    
    int left = 0, right = n - 1, top = 0, bottom = m - 1;
    int i, j;
    while (left <= right && top <= bottom) {
        j = left;
        while (j <= right) {
            res.push_back(matrix[top][j]);
            j++;
        }
        top++;
        i = top;
        while (i <= bottom) {
            res.push_back(matrix[i][right]);
            i++;
        }
        right--;
        
        if (left > right || top > bottom) return res;
        
        j = right;
        while (j >= left) {
            res.push_back(matrix[bottom][j]);
            j--;
        }
        bottom--;
        i = bottom;
        while(i >= top) {
            res.push_back(matrix[i][left]);
            i--;
        }
        left++;
    }
    return res;
}
```



