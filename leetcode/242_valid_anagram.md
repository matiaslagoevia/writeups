# 217. Contains Duplicate

## Link

https://leetcode.com/problems/valid-anagram/description/

## Prompt

> Given two strings s and t, return true if t is an anagram of s, and false otherwise.
> An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Intuition

Both strings must be made up of exactly the same characters in a different order. If we had a way to keep track of the frequency of characters in one string and then iterate over the other one, we could see if we are missing characters or not.

## Approach

For different length strings, we immediately know that the answer is false.
Otherwise, we need to be able to:

1. have a character count
2. for any character, be able to check, subtract, and add to it's count

`Map`s have O(1) check, subtract, add operations, so they'd be a good fit. However, because our alphabet range here is small & contiguous, we can use a frequency array. `a[i]` will hold the character count for the character with ascii code (number) `i`.

## Complexity

### Time

> `O(N)`, where `N` is the length of the strings `s` and `t`

- We first iterate one string and then the other.
- We do constant work for each iteration.

### Space

> `O(1)`

- We always store 26 values, regardless of the size of N.

## Code

```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isAnagram = function (s, t) {
  if (t.length != s.length) return false;
  function getFreqIdx(ch) {
    return ch.charCodeAt(0) - "a".charCodeAt(0);
  }
  const freq = new Array(26).fill(0);
  for (const c of t) {
    freq[getFreqIdx(c)]++;
  }
  for (const c of s) {
    if (freq[getFreqIdx(c)] <= 0) return false;
    freq[getFreqIdx(c)]--;
  }
  return true;
};
```
