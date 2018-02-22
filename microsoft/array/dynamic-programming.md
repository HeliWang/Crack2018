1. Best Time to Buy and Sell Stock
2. Maximum Subarray
3. Longest Increasing Subsequence

# 1. Best Time to Buy and Sell Stock

Say you have an array for which theithelement is the price of a given stock on dayi.

If you were only permitted to complete at most one transaction \(ie, buy one and sell one share of the stock\), design an algorithm to find the maximum profit.

**Solution:**

```cpp
int maxProfit(vector<int>& prices) {
    if (prices.size() <= 1) return 0;
    int temp = prices[1] - prices[0], global = temp;
    for (int i = 2; i < prices.size(); i++) {
        int diff = prices[i] - prices[i-1];
        temp = max(temp + diff, diff);
        global = max(global, temp);
    }
    return global < 0 ? 0 : global;
}
```

# 2. Maximum Subarray

Find the contiguous subarray within an array \(containing at least one number\) which has the largest sum.

For example, given the array`[-2,1,-3,4,-1,2,1,-5,4]`,  
the contiguous subarray`[4,-1,2,1]`has the largest sum =`6`.

```cpp
int maxSubArray(vector<int>& nums) {
    int temp = nums[0];
    int global = nums[0];
    for (int i = 1; i < nums.size(); i++) {
        temp = max(nums[i] + temp, nums[i]);
        global = max(global, temp);
    }
    return global;
}
```

# 3. Longest Increasing Subsequence

Given an unsorted array of integers, find the length of longest increasing subsequence.

For example,  
Given`[10, 9, 2, 5, 3, 7, 101, 18]`,  
The longest increasing subsequence is`[2, 3, 7, 101]`, therefore the length is`4`. Note that there may be more than one LIS combination, it is only necessary for you to return the length.

Your algorithm should run in O\(n2\) complexity.

```cpp
int lengthOfLIS(vector<int>& nums) {
    if (nums.size() == 0) return 0;
    vector<int> dp(nums.size() + 1, 1);
    int res = 1;
    for (int i = 0; i < nums.size(); i++) {
        for (int j = 0; j < i; j++) {
            if (nums[i] > nums[j]) {
                dp[i] = max(dp[i], dp[j] + 1);
                res = max(res, dp[i]);
            }
        }
    }
    return res;
}
```



