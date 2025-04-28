# Reverse a linked list

## Problem

**Description:** https://www.hackerrank.com/challenges/reverse-a-linked-list/problem

> Given the pointer to the head node of a linked list, change the next pointers of the nodes so that their order is reversed. The head pointer given may be null meaning that the initial list is empty.

**Difficulty:** easy

## Solution

## Code

``` cpp
SinglyLinkedListNode* reverse(SinglyLinkedListNode* llist) {
    SinglyLinkedListNode* h = nullptr;
    SinglyLinkedListNode* p = llist;
    if(p->next->next == nullptr) h = p->next;
    else h = reverse(p->next);
    p->next->next = p;
    p->next = nullptr;
    return h;
}
```
