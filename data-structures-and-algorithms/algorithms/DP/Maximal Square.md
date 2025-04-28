# Maximal Square

## Problem 

**Description:** https://leetcode.com/problems/maximal-square
> Given an `m x n` binary matrix filled with `0`'s and `1`'s, find the largest square containing only `1`'s and return its area.

**Difficulty:** medium

## Solution

TBD

## Code

``` cpp
class Solution {
public:

    struct rectangle{
        int length, width; // row, col
        rectangle(): length(), width(){}
        rectangle(int a, int b): length(a), width(b){}
    }ans = {0, 0};

    int maximalSquare(vector<vector<char>>& matrix) {
        int m = matrix.size(), n = matrix[0].size();
        bool flag = 0;
        rectangle dp[305][305];

        if(matrix[0][0] == '1'){
            dp[0][0] = {1, 1};
            flag = 1;
        } else{
            dp[0][0] = {0, 0};
        }

        for(int i = 1; i < n; i++){
            if(matrix[0][i] == '1'){
                dp[0][i] = {1, 1};
                flag = 1;
            }
            else dp[0][i] = {0, 0};
        }

        for(int i = 1; i < m; i++){
            if(matrix[i][0] == '1'){
                dp[i][0] = {1, 1};
                flag = 1;
            } else dp[i][0] = {0, 0};
            for(int j = 1; j < n; j++){
                if(matrix[i][j] == '0') dp[i][j] = {0, 0};
                else{
                    dp[i][j].length = min(dp[i - 1][j - 1].length, dp[i][j - 1].length) + 1;
                    dp[i][j].width = min(dp[i - 1][j - 1].width, dp[i - 1][j].width) + 1;
                    if(min(dp[i][j].length, dp[i][j].width) > min(ans.length, ans.width)) ans = dp[i][j];
                }
            }  
        }
        if(ans.length == 0 && ans.width == 0 && flag) ans = {1, 1};

        int len = min(ans.length, ans.width);
        return len * len;
    }
};
```
