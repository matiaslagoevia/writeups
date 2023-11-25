# 20. Valid Parentheses

## Link

https://leetcode.com/problems/valid-parentheses/description

## Prompt

> Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.
>
> An input string is valid if:
>
> 1.  Open brackets must be closed by the same type of brackets.
> 2.  Open brackets must be closed in the correct order.
> 3.  Every close bracket has a corresponding open bracket of the same type.

## Intuition

Opening characters are always valid, but closing ones are valid only if the last opening character seen corresponds to it. Opening characters that don't have a corresponding closing character aren't valid either. We can use a stack to hold opening characters in that order.

## Approach

We need to be able to:

1. use a stack for the opening characters
2. handle invalid closing characters
3. handle invalid opening characters

We can iterate over all characters and use a stack for the opening characters.
We'll add opening characters no matter what at this point by pushing them to the stack.
For closing characters, if the last opening character doesn't match it, we return false.
Finally, if there's any opening characters left (i.e. stack isn't empty), we also return false.

## Complexity

### Time

> `O(N)`, where `N` is the length of the string.

- We iterate over at most `N` characters of the string, doing `O(1)` work on each

### Space

> `O(N)`, where `N` is the length of the string.

- The stack can hold at most `N` opening characters

## Code

```js
/**
 * @param {string} s
 * @return {boolean}
 */
var isValid = function (s) {
  const stack = [],
    pairs = { "}": "{", "]": "[", ")": "(" };
  for (const x of s) {
    if (x === "(" || x === "{" || x === "[") {
      stack.push(x);
    } else {
      if (stack.pop() !== pairs[x]) return false;
    }
  }
  return stack.length === 0;
};
```
