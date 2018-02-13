# Combination Sum IV

Given an integer array with all positive numbers and no duplicates, find the number of possible combinations that add up to a positive integer target.

```
nums = [1, 2, 3]
target = 4

The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)

Note that different sequences are counted as different combinations.

Therefore the output is 7.
```

Idea:

```
Dynamic Programming
Thinking of the last step to reach dp[target]
dp[target] = sum of (dp[target - nums[i]]);

Base Case: dp[0] = 1;
```

Solution:

```cpp
int combinationSum4(vector<int>& nums, int target) {
    vector<int> dp(target + 1, 0);
    for (auto x: nums) {
        if (x <= target) dp[x] = 1;
    }

    for (int i = 0; i <= target; i++) {
        for (auto x : nums) {
            if (x <= i) {
                dp[i] += dp[i - x];
            }
        }
    }
    return dp[target];
}
```



