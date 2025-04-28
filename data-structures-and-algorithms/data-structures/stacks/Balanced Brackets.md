# Balanced Brackets

## Problem

**Description:** https://www.hackerrank.com/challenges/balanced-brackets/problem <br>
**Difficulty:** medium

## Solution
Classic brackets matching problem.

## Code

``` cpp
/*
 * Complete the 'isBalanced' function below.
 *
 * The function is expected to return a STRING.
 * The function accepts STRING s as parameter.
 */

string isBalanced(string s) {
    std::stack<char> st;
    int len = s.length();
    for(int i = 0; i < len; i++){
        switch (s[i]) {
            case '{':
            case '[':
            case '(':
                st.push(s[i]);
                break;
            case '}':
                if(!st.empty() && st.top() == '{') st.pop();
                else return "NO";
                break;
            case ']':
                if(!st.empty() && st.top() == '[') st.pop();
                else return "NO";
                break;
            case ')':
                if(!st.empty() && st.top() == '(') st.pop();
                else return "NO";
                break;                
        }
    }
    if(st.empty()) return "YES";
    else return "NO";
}
```
