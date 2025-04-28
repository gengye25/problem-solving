# Roads and Libraries

## Problem

**Discription:** https://www.hackerrank.com/challenges/torque-and-development/problem <br>
**Difficulty:** medium <br>

## Solution 

First, with the case c_lib <= c_road, there's no need to repair any roads as the optimal way is to simply build a library in every cities. <br>
Otherwise we can see a road as a "discount" library, as long as we can find a path for the city to another one, who already has a library. So we can use disjiont sets to construct potential connectivity graphs among the given point set. <br>
And to calculate the total cost, we only need to find out both the amount of the sets (as the libraries we need to build) and the element numbers in each sets (as the number of roads we need to build is element - 1, according to the properties of spanning tree).

## Code

```cpp
/*
 * Complete the 'roadsAndLibraries' function below.
 *
 * The function is expected to return a LONG_INTEGER.
 * The function accepts following parameters:
 *  1. INTEGER n
 *  2. INTEGER c_lib
 *  3. INTEGER c_road
 *  4. 2D_INTEGER_ARRAY cities
 */

long roadsAndLibraries(int n, int c_lib, int c_road, vector<vector<int>> cities) {
    if(c_road >= c_lib) return (long)n * c_lib;
    long ans = 0L;
    vector<int> dsu;
    map<int, int> mp;
    for(int i = 0; i <= n; i++){
        dsu.push_back(i);
    }
    for(auto a : cities){
        int tmp_0 = a[0], tmp_1 = a[1];
        while(dsu[tmp_0] != tmp_0) tmp_0 = dsu[tmp_0];
        while(dsu[tmp_1] != tmp_1) tmp_1 = dsu[tmp_1];
        dsu[tmp_0] = tmp_1;
    }
    for(int i = 1; i <= n; i++){
        int tmp = i;
        if(i != dsu[i]){
            while(dsu[tmp] != tmp) tmp = dsu[tmp];
        }
        if(mp.find(tmp) == mp.end()) mp[tmp] = 1;
        else mp[tmp]++;
    }
    for(auto m : mp){
        ans += (c_lib + (m.second - 1) * c_road);
    }
    return ans;
}
```
