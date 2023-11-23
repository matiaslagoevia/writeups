# 290. Word Pattern

## Link

https://leetcode.com/problems/word-pattern/description/

## Prompt

> Given a pattern and a string s, find if s follows the same pattern.
>
> Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in s.

## Intuition

We want to associate a letter in pattern to a non-empty word in s. Different letters can map to the same word, but the same letter cannot refer to different words.

## Approach

If we don't have the same number of letters and words, we already know it's not possible.

Otherwise, we need to:

1. associate a letter to a word
2. disallow same letter to refer to different words

We can use a map to associate a letter to a word, and a set to keep track of the values present in the map.
At insertion time, if this is the first time we've seen a letter **and** the word isn't associated to another letter, then we associate it to this letter.
If it's not the first time we've seen a letter, we check that it's for the same word we've seen before.

## Complexity

### Time

> `O(max(M,N))`, where `M` is the pattern length and `N` is the length of s.

- We split `s` on it's `N` characters onto some `W` words
- We iterate over at most each of the `M` elements and populate the set/map accordingly

### Space

> `O(M+N)`, where `M` is the pattern length and `N` is the length of s.

- We store at most `N` characters in the words array
- We store at most `M` elements in the map & set

## Code

```js
/**
 * @param {string} pattern
 * @param {string} s
 * @return {boolean}
 */
var wordPattern = function (pattern, s) {
  const words = s.split(" ");
  if (pattern.length !== words.length) return false;

  const m = new Map(),
    seen = new Set();
  for (let i = 0; i < pattern.length; i++) {
    const key = pattern[i];
    if (!m.has(key)) {
      if (seen.has(words[i])) return false;
      m.set(key, words[i]);
      seen.add(words[i]);
    } else if (m.get(key) !== words[i]) return false;
  }
  return true;
};
```
