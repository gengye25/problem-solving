# House Robber

## Problem

**Description:** https://leetcode.com/problems/house-robber <br>
**Difficulty:** medium

## Solution

TBD

## Code

``` cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int n = nums.size();
        vector<int> dp;
        dp.push_back(0);
        dp.push_back(nums[0]);
        for(int i = 1; i < n; i++){
            dp[i - 1] + nums[i] > dp[i] ? dp.push_back(dp[i - 1] + nums[i]) : dp.push_back(dp[i]);
        }
        return dp[n];
    }
};
```
