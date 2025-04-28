# Down to Zero II

## Problem

**Discription:** https://www.hackerrank.com/challenges/down-to-zero-ii/problem <br>
**Difficulty:** medium

## Solution



## Code

``` cpp
struct num{
    int v = 0, layer = 0;
    num(int _v, int _l){
        v = _v;
        layer = _l;
    }
};

int downToZero(int n) {
    std::queue<num> qu;
    vector<int> visited;
    qu.push(num(n, 0));
    visited.push_back(n);
    num k = qu.front();
    int tmp = 0;
    while(n != 0){
        if(k.v == 1){
            k.layer++;
            break;
        } else tmp = k.v - 1;
        if(find(visited.begin(), visited.end(), tmp) == visited.end()){
            qu.push(num(tmp, k.layer + 1));
            visited.push_back(tmp);  
        }
        for(int i = 2; i * i <= k.v; i++){
            if(k.v % i == 0){
                int tmp = k.v / i;
                if(find(visited.begin(), visited.end(), tmp) == visited.end()){
                    qu.push(num(tmp, k.layer + 1));
                    visited.push_back(tmp);  
                }
            }
        }
        qu.pop();
        k = qu.front();
    }
    return k.layer;
}
```
