

# Wild Card Matching

Implement wildcard pattern matching with support for `'?' `and `'*'`

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

Idea:

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

Solution:

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

Idea:

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

Solution:

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



