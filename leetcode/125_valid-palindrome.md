# 125. Valid Palindrome

## Link

https://leetcode.com/problems/valid-palindrome/description

## Prompt

> A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.
>
> Given a string s, return true if it is a palindrome, or false otherwise.

## Intuition

If the input is well formed (i.e. only lowercase letters and digits), then it's a matter of comparing the leftmost character to the rightmost character, the 2nd leftmost to the 2nd rightmost, and so on until there's one or zero characters left to compare.

## Approach

We need to:

1. remove non-alphanumeric/lowercase characters from the input
2. for each leftmost/rightmost pair, check for equality

We can remove unwanted characters by first transforming characters to be lowercase and then removing non alphanumeric characters.
We process leftmost/rightmost pairs with a for loop while `l<r`.

## Complexity

### Time

> `O(N)`, where `N` is the length of the string.

- We look at `N` characters when transforming to lowercase
- We look at `N` characters when removing non-alphanumeric characters
- We look at most at `N` characters when looking at leftmost/rightmost pairs

### Space

> `O(N)`, where `N` is the length of the string.

- We create strings of at most `N` elements during the lowercase and non-alphanumeric transformations

## Code

```js
/**
 * @param {string} s
 * @return {boolean}
 */
var isPalindrome = function (s) {
  s = s.toLowerCase().replaceAll(/[^a-z0-9]/g, "");
  for (let l = 0, r = s.length - 1; l < r; l++, r--) {
    if (s[l] !== s[r]) return false;
  }
  return true;
};
```
