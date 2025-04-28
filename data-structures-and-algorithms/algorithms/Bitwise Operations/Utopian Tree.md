# Utopian Tree

## Problem

**Discription:** https://www.hackerrank.com/challenges/utopian-tree/problem

> The Utopian Tree goes through 2 cycles of growth every year. Each spring, it doubles in height. Each summer, its height increases by 1 meter. <br>
> A Utopian Tree sapling with a height of 1 meter is planted at the onset of spring. How tall will the tree be after `n` growth cycles?

**Difficulty:** Easy

## Solution

First, I came up with recursion, as:
``` cpp
int utopianTree(int n) {
    if(!n) return 1;
    else if(n&1) return 2 * utopianTree(n - 1);
    else return 1 + utopianTree(n - 1);
}
```
And it's mostly the same with other kinds of loops, f.x.:
``` cpp
int utopianTree(int n) {
    int ans = 1;
    for(int i = 1; i <= n; i++){
        if(i & 1) ans = ans * 2;
        else ans++;
    }
    return ans;
}
```
However as I found in the comments, there's a wiser (and ofc faster) solution using bit shifting and a little bit more calculation, as the height of our tree **doubles** whenever it's an odd round, it can simply be presented by one bit of left shift. <br>
Then suppose n is even. We find out that the height of the tree always have the form of: <br>
`(2(2...(2(1)+1)...+1)+1 = 2^{n/2} + 2^(n/2 - 1) + ... + 1 = 2^(n/2 + 1) - 1`
And for n is odd, it's simply another left shift after calculated the case n - 1.
``` cpp
int utopianTree(int n){
    return !(n & 1) ?  (1 << (n / 2 + 1)) - 1 : ((1 << (n / 2 + 1)) - 1) << 1;
}
```
