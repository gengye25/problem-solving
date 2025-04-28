# Array Manipulation

## Problem

**Description:** https://www.hackerrank.com/challenges/crush/problem <br>
**Difficulty:** hard

## Solution

It'll be quite inefficient to "physically" maintain the array, since every query cost at worst O(n) time. I first thought of construct and maintaining a linked list to record same adjacent values of the array, as values in the arry are stored in blocks (the nodes of the linked list), but that's still too slow:

``` cpp

/*
 * Complete the 'arrayManipulation' function below.
 *
 * The function is expected to return a LONG_INTEGER.
 * The function accepts following parameters:
 *  1. INTEGER n
 *  2. 2D_INTEGER_ARRAY queries
 */
struct Node{
    int l, r;
    long sum;
    Node* next;
    Node();
    Node(int left, int right){
        l = left;
        r = right;
        sum = 0;
        next = nullptr;
    }
};

Node* split(Node* p, int a, bool l){
    Node* q = new Node(p->l, p->r);
    q->sum = p->sum;
    q->next = p->next;
    p->next = q;
    if(l){
        p->r = a - 1;
        q->l = a;
        return q;
    } else{
        p->r = a;
        q->l = a + 1;
        return p;
    }
}

Node* update(Node* ll, int a, int b, int k){
    Node* p = ll;
    while(a > p->r) p = p->next;
    if(a > p->l) p = split(p, a, true);
    while(b > p->r){
        p->sum += k;
        p = p->next;
    }
    if(b < p->r) p = split(p, b, false);
    p->sum += k;
    return ll;
}

long arrayManipulation(int n, vector<vector<int>> queries) {
    Node* ll = new Node(1, n);
    for(auto a : queries){
        update(ll, a[0], a[1], a[2]);
        
    }
    long ans = -1;
    Node* p = ll;
    while(p != nullptr){
        if(p->sum > ans) ans = p->sum;
        p = p->next;
    }
    return ans;
}

```

(TBD)
