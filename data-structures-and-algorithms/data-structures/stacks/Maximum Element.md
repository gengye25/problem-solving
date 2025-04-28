# Maximum Element

## Problem

**Description:** https://www.hackerrank.com/challenges/maximum-element/problem <br>
**Difficulty:** easy

## Solution
## Code

``` cpp
vector<int> getMax(vector<string> operations) {
    vector<int> st;
    vector<int> ans;
    for(auto a : operations){
        switch (a[0]) {
            case '1':
                st.push_back(stoi(a.substr(2, a.length() - 2)));
                break;
            case '2':
                st.pop_back();
                break;
            case '3':
                int max = *max_element(st.begin(), st.end());
                ans.push_back(max);
                break;
        }
    }
    return ans;
}
```
