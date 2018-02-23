Given`n`balloons, indexed from`0`to`n-1`. Each balloon is painted with a number on it represented by array`nums`. You are asked to burst all the balloons. If the you burst balloon`i`you will get`nums[left] * nums[i] * nums[right]`coins. Here`left`and`right`are adjacent indices of`i`. After the burst, the`left`and`right`then becomes adjacent.

Find the maximum coins you can collect by bursting the balloons wisely.

**Note:**  
\(1\) You may imagine`nums[-1] = nums[n] = 1`. They are not real therefore you can not burst them.  
\(2\) 0 ≤`n`≤ 500, 0 ≤`nums[i]`≤ 100

**Example:**

Given`[3, 1, 5, 8]`

Return`167`

**Idea:**

```
扎气球经典题，二维DP
先讨论General Case
DP[i][j] 表示扎破i到j的气球暂时拿到的分数，考虑在[i,j]的闭区间内第k个气球如果是最后一个扎破的？
关键点在于怎么想到最后一个扎破的：因为最后一个扎破的话，可以写出通项为 nums[left-1]*nums[k]*nums[right+1]
如果是第一个扎破的话，你永远不知道下一个扎破的是哪一个，所以这是一个bottom-up的递归 or 动态规划

其实类似于dp[i][j]依赖于中间内部的元素，自内而外的DP都是bottom up的，比如longest palindrome substring
先从小范围set up，作为扩张的基础。

因此通项为
dp[left][right] = max(dp[left][right], 
                  nums[left - 1]*nums[k]*nums[right + 1]
                  + dp[left][k-1] 
                  + dp[k+1][right]);
            
再来讨论Base Case
dp[k][k] 即 left == k == right
dp[k][k] = nums[k-1]*nums[k]*nums[k+1]

for循环用bottomup自内而外的模式，
for (int step)
    for (int left)
        int right = left + step;
其中left right可能相等，因此step从0到n-1

*** 记得在nums左边和右边加上一个1
```

**Solution:**

```cpp
int maxCoins(vector<int>& nums) {
    int n = nums.size();
    nums.insert(nums.begin(), 1);
    nums.push_back(1);
    vector<vector<int> > dp(nums.size(), vector<int>(nums.size(), 0));
    
    for (int step = 0; step < n; step++) {
        for (int left = 1; left + step <= n; left++) {
            int right = left + step;
            for (int k = left; k <= right; k++) {
                dp[left][right] = max(dp[left][right], nums[left - 1]*nums[k]*nums[right + 1] + dp[left][k-1] + dp[k+1][right]);
            }
        }
    }
    
    
    return dp[1][n];
}
```



