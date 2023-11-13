# 541. Reverse String II

## Link

https://leetcode.com/problems/reverse-string-ii/description/

## Prompt

> Given a string s and an integer k, reverse the first k characters for every 2k characters counting from the start of the string.
> If there are fewer than k characters left, reverse all of them. If there are less than 2k but greater than or equal to k characters, then reverse the first k characters and leave the other as original.

## Intuition

Possible replacement ranges are [0, k), [2k, 3k), [4k, 5k), and so on. We can reverse the characters in each range and then return the result. The last possible replacement range isn't guaranteed to be complete, so process however many characters are available for it.

## Approach

We need to be able to:

1. process all replacement ranges
2. determine the last replacement range end correctly
3. reverse the string characters within a range

Strings are immutable in JS, so we'll use `.split()` and `.join("")` to alternate between a character array and a string representation.
We can reverse a range by swapping values as we move inwards within that range.
The `i`th range (0-indexed) is `[i*k, i*k+k-1)`; we can iterate over these with a for loop.
The last replacement range, if incomplete, will not go past the end of the array.

## Complexity

### Time

> `O(N)`, where `N` is the length of the string.

- We process all ranges' elements, which are at most all `N` elements.
- Both `.split()` and `.join()` process all `N` elements.

### Space

> `O(N)`, where `N` is the length of the string.

- `.split()` creates an array with `N` elements.
- `.join()` converts the array with `N` elements to a string.

## Code

```js
/**
 * @param {string} s
 * @param {number} k
 * @return {string}
 */
var reverseStr = function (s, k) {
  s = s.split("");
  for (let i = 0; i < s.length; i += 2 * k) {
    for (let l = i, r = min(s.length - 1, i + k - 1); l < r; l++, r--) {
      const temp = s[l];
      s[l] = s[r];
      s[r] = temp;
    }
  }
  return s.join("");
};
```
