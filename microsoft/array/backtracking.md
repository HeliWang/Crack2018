# Wild Card Matching

Implement wildcard pattern matching with support for `'?'`and `'*'`

```
'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).

The matching should cover the 
entire
 input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "*") → true
isMatch("aa", "a*") → true
isMatch("ab", "?*") → true
isMatch("aab", "c*a*b") → false
```

**Idea:**

```
http://bangbingsyb.blogspot.com/2014/11/leetcode-wildcard-matching.html

和Regular Expression Matching很像，这里的'?'相当于Regular Expression中的'.'，
但'*'的用法不一样。这里'*'与前一个字符没有联系，并且无法消去前一个字符，但可以表示任意一串字符。
递推公式的推导和Regular Expression Matching也基本类似。

p[j-1] == s[i-1] || p[j-1] == '?'：dp[i][j] = dp[i-1][j-1]
p[j-1] == '*'：
1. 匹配0个字符：dp[i][j] = dp[i][j-1]
2. 匹配1个字符：dp[i][j] = dp[i-1][j-1]
3. 匹配多个字符：dp[i][j] = dp[i-1][j]
```

**Solution**:

```cpp
bool isMatch(string s, string p) {
    int m = s.length(), n = p.length();
    vector<vector<bool>> dp(m+1, vector<bool>(n+1,false));
    dp[0][0] = true;
    for(int i=0; i<=m; i++) {
        for(int j=1; j<=n; j++) {
            if(i>0 && (p[j-1]==s[i-1] || p[j-1]=='?') && dp[i-1][j-1]) {
                dp[i][j] = true;
            }
            else if(p[j-1]=='*') {
                if (dp[i][j-1]) dp[i][j] = true;
                else if (i>0 && (dp[i-1][j-1] || dp[i-1][j])) {
                    dp[i][j] = true;
                }
            }

        }
    }
    return dp[m][n];
}
```

# Regular Expression Matching

Implement regular expression matching with support for`'.'`and`'*'`

```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
```

**Idea:**

```
http://bangbingsyb.blogspot.com/2014/11/leetcode-regular-expression-matching.html

关键在于如何处理这个'*'号。

状态：和Mininum Edit Distance这类题目一样。
dp[i][j]表示s[0:i-1]是否能和p[0:j-1]匹配。

递推公式：由于只有p中会含有regular expression，所以以p[j-1]来进行分类。
p[j-1] != '.' && p[j-1] != '*'：dp[i][j] = dp[i-1][j-1] && (s[i-1] == p[j-1])
p[j-1] == '.'：dp[i][j] = dp[i-1][j-1]

而关键的难点在于 p[j-1] = '*'。由于星号可以匹配0，1，乃至多个p[j-2]。
1. 匹配0个元素，即消去p[j-2]，此时p[0: j-1] = p[0: j-3]
dp[i][j] = dp[i][j-2]

2. 匹配1个元素，此时p[0: j-1] = p[0: j-2]
dp[i][j] = dp[i][j-1]

3. 匹配多个元素，此时p[0: j-1] = { p[0: j-2], p[j-2], ... , p[j-2] }
dp[i][j] = dp[i-1][j] && (p[j-2]=='.' || s[i-1]==p[j-2])

***注意最后一个通项式***
我们只需要往i-1回退一步就可以了，因为如果更多的匹配的话，会在for循环里先setup好，所以最后的一次是可以得到之前累计的结果的
```

**Solution:**

```cpp
bool isMatch(string s, string p) {
    int m = s.length(), n = p.length();
    vector<vector<bool>> dp(m + 1, vector<bool>(n + 1, false));
    dp[0][0] = true;
    for (int i = 0; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if(p[j-1] == '.' && i > 0 && dp[i-1][j-1]) dp[i][j] = true;
            if (p[j-1] != '.' && p[j-1] != '*' && i>0 && p[j-1] == s[i-1] && dp[i-1][j-1]) dp[i][j] = true;
            if (j > 1 && p[j-1] == '*') {
                if (dp[i][j-1] || dp[i][j-2]) dp[i][j] = true;
                if (i > 0 && (s[i-1] == p[j-2] || p[j-2] == '.') && dp[i-1][j]) dp[i][j] = true;
            }
        }        
    }
    return dp[m][n];
}
```

# Word Search

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

For example,  
Given **board **=

```
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
```

**word**=`"ABCCED"`, -&gt; returns `true`

**Idea:**

```
DFS
```

**Solution:**

```
bool exist(vector<vector<char>>& board, string word) {
    if (word.length() == 0) return true;
    if (board.size() == 0 || board[0].size() == 0) return 0;
    vector<vector<bool>> visited(board.size(), vector<bool>(board[0].size(), false));
    for (int i = 0; i < board.size(); i++) {
        for (int j = 0; j < board[0].size(); j++) {
            if (board[i][j] == word[0]) {
                if (dfs(board, word, visited, i, j, 0)) return true;
            }
        }
    }
    return false;
}

bool dfs(vector<vector<char>>& board, string word, vector<vector<bool>> visited, int i, int j, int start) {
    if (start == word.length() - 1 && board[i][j] == word[start]) return true;
    visited[i][j] = true;
    if (board[i][j] == word[start]) {
        if (i < board.size() - 1 && !visited[i + 1][j] &&  dfs(board, word, visited, i + 1, j, start + 1)) return true;
        if (j < board[0].size() - 1 && !visited[i][j + 1] && dfs(board, word, visited, i, j + 1, start + 1)) return true;
        if (i > 0 && !visited[i - 1][j] && dfs(board, word, visited, i - 1, j, start + 1)) return true;
        if (j > 0 && !visited[i][j - 1] && dfs(board, word, visited, i, j - 1, start + 1)) return true;
    } 
    return false;
}
```

# Word Search II

Given a 2D board and a list of words from the dictionary, find all words in the board.

Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

For example,  
Given **words**=`["oath","pea","eat","rain"]`and **board **=

```
[
  ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]
```

Return

`["eat","oath"]`

Idea:

```
Trie + DFS
Trie照常建，注意在words array上建而不是二维矩阵
然后对矩阵里每一个元素进行word search based on Trie root
```

Solution:

```cpp
class TrieNode {
public:
    bool hasWord;
    unordered_map<char, TrieNode*> children;
    TrieNode () {
        hasWord = false;
    }
};

class Trie {
private:
    TrieNode* root;
public:
    /** Initialize your data structure here. */
    Trie() {
        root = new TrieNode();
    }

    TrieNode* getRoot() {
        return root;
    }

    /** Inserts a word into the trie. */
    void insert(string word) {
        TrieNode* curr = root;
        for (int i = 0; i < word.length(); i++) {
            if (curr->children.count(word[i]) == 0) curr->children[word[i]] = new TrieNode();
            curr = curr->children[word[i]];
        }
        curr->hasWord = true;
    }

    /** Returns if the word is in the trie. */
    bool search(string word) {
        TrieNode* curr = root;
        for (int i = 0; i < word.length(); i++) {
            if (curr->children.count(word[i]) > 0) curr = curr->children[word[i]];
            else return false;
        }
        return curr->hasWord == true;
    }
};

class Solution {
public:
    vector<string> findWords(vector<vector<char>>& board, vector<string>& words) {
        vector<string> res;
        if (words.size() == 0 || board.size() == 0 || board[0].size() == 0) return res;

        sort(words.begin(), words.end() );
        words.erase( unique( words.begin(), words.end() ), words.end());
        string line;
        vector<vector<bool>> visited(board.size(), vector<bool>(board[0].size(), false));
        Trie *trie = new Trie();
        for (auto x: words) trie->insert(x);
        TrieNode* root = trie->getRoot();
        for (int i = 0; i < board.size(); i++) {
            for (int j = 0; j < board[0].size(); j++) {
                dfs(board, root, line, res, visited, i, j);
            }
        }
        sort(res.begin(), res.end() );
        res.erase(unique(res.begin(), res.end()), res.end());
        return res;
    }

    void dfs(vector<vector<char>>& board, TrieNode* root, string line, vector<string>& res, vector<vector<bool>> visited, int i, int j) {
        if (!root || i < 0 || j < 0 || i == board.size() || j == board[0].size() || visited[i][j]) return;
        visited[i][j] = true;
        if (root->children.count(board[i][j]) > 0) {
            line += board[i][j];
            root = root->children[board[i][j]];
            if (root->hasWord) res.push_back(line);
            dfs(board, root, line, res, visited, i + 1, j);
            dfs(board, root, line, res, visited, i, j + 1);
            dfs(board, root, line, res, visited, i - 1, j);
            dfs(board, root, line, res, visited, i, j - 1);
        }
    }
};
```

# Letter Combinations of a Phone Number

Given a digit string, return all possible letter combinations that the number could represent.

A mapping of digit to letters \(just like on the telephone buttons\) is given below.

![](/assets/import.png)

```
Input:Digit string "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

Idea:

```
Backtracking, constructed a candidates array at first
```

Solution:

```cpp
vector<string> letterCombinations(string digits) {
    vector<string> candidates = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    string line;
    vector<string> res;
    if (digits.length() == 0) return res;
    helper(res, line, candidates, digits, 0);
    return res;
}
void helper(vector<string>& res, string line, vector<string> candidates, string digits, int start) {
    if (line.length() == digits.length()) {
        res.push_back(line);
        return;
    }
    if (start >= digits.length()) return;
    int index = digits[start] - '0';
    for (int i = 0; i < candidates[index].length(); i++) {
        line.push_back(candidates[index][i]);
        helper(res, line, candidates, digits, start + 1);
        line.pop_back();
    }
}
```



