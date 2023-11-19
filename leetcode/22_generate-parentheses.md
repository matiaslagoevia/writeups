# 1. Two Sum

## Link

https://leetcode.com/problems/generate-parentheses/

## Prompt

> Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

## Intuition

Since the constraints on `n` are small (`1 <= n <= 8`), a complete search approach is possible. Recursively trying to add `(` followed by recursively trying to add `)` searches the entire solution space. Adding a `)` only makes sense if there's a corresponding `(` available — checking order matters to avoid invalid combinations.

## Approach

We need to be able to:

1. add each valid combination to the result
2. explore possible paths from choosing an opening brace
3. explore possible paths from choosing a closing brace

A valid combination has a length of `2*n`, assuming that only valid paths got it there.
A valid opening brace path is available if `open < n`.
A valid closing brace path is available if `closed < open`.

## Complexity

### Time

> `O(4^n/sqrt(n))`, where `N` is the number of pairs.

- Catalan number — abstract it away for now

### Space

> `O(N)`, where `N` is the number of pairs.

- The call stack consists of at most `2N` calls
- The `curr` string consists of at most `2N` characters

## Code

```js
/**
 * @param {number} n
 * @return {string[]}
 */
var generateParenthesis = function(n) {
    const ans = [];
    gen(1,0,"(");
    return ans;

    function gen(open, closed, curr) {
        if(curr.length === 2*n) ans.push(curr);
        if(open < n) gen(open+1, closed, curr+"(");
        if(closed < open) gen(open, closed+1, curr+")");
    }
};
};
```
