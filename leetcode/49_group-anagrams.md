# 49. Group Anagrams

## Link

https://leetcode.com/problems/group-anagrams/description/

## Prompt

> Given an array of strings strs, group the anagrams together. You can return the answer in any order.
> An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

## Intuition

If we decide on an unique representation for each anagram, we can group them together for our result.

## Approach

We need to be able to:

1. group anagrams together based on their unique representation
2. decide how we'll represent them

`Map`s can be helpful to associate one value to another.
We'll use our unique representations as keys and the grouped anagrams as values.
We could use a string's lexicographically sorted equivalent as the unique representation, but a character count approach is more efficient.
Since JS would be comparing array references and not their values, we'll serialize them into strings before using them as keys.

## Complexity

### Time

> `O(N*K)`, where `N` is the number of strings and `K` is the longest string in `nums`.

- We process `N` strings.
- For each string, we'll process at most `K` characters.
- Serializing the count array is O(1), since we have a fixed alphabet of size 26.
- Inserting the string into it's group is O(1) on average.

### Space

> `O(N*K)`, where `N` is the number of strings and `K` is the longest string in `nums`.

- Our map will hold at most `N*K` characters.
- The answer array will hold at most `N*K` characters.

## Code

```js
/**
 * @param {string[]} strs
 * @return {string[][]}
 */
var groupAnagrams = function (strs) {
  const m = new Map();
  for (const s of strs) {
    let count = Array(26).fill(0);
    for (const c of s) {
      count[c.charCodeAt(0) - 97]++;
    }
    // we serialize the count array to a string to avoid issues with them as map keys
    count = String(count);
    if (m.get(count) === undefined) {
      m.set(count, []);
    }
    m.get(count).push(s);
  }

  const ans = [];
  for (const x of m.values()) {
    ans.push(x);
  }
  return ans;
};
```
