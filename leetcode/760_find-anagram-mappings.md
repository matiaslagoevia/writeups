# 760. Find Anagram Mappings

## Link

https://leetcode.com/problems/find-anagram-mappings/description

## Prompt

> You are given two integer arrays nums1 and nums2 where nums2 is an anagram of nums1. Both arrays may contain duplicates.
>
> Return an index mapping array mapping from nums1 to nums2 where mapping[i] = j means the ith element in nums1 appears in nums2 at index j. If there are multiple answers, return any of them.
>
> An array a is an anagram of an array b means b is made by randomizing the order of the elements in a.

## Intuition

We're guaranteed that a word in nums1 will be in nums2 since it's an anagram. So, we want to put the index it has on nums2 as a result.

## Approach

We need to:

1. lookup a word on nums2
2. iterate on words on nums1 and place the result of the nums2 lookup in that index

We can put nums2 into a hashmap for O(1) lookups.
We can use `Array.map` on nums1 to replace the contents of an index with where they appear in nums2.

## Complexity

### Time

> `O(N)`, where `N` is the number of words.

- We populate `N` elements of `nums2` into a map
- We iterate/replace `N` elements of `nums1` with their index on `nums2`

### Space

> `O(N)`, where `N` is the number of nodes.

- The `nums2` map holds `N` elements
- The resulting array holds `N` elements

## Code

```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var anagramMappings = function (nums1, nums2) {
  const m2 = new Map();
  for (let i = 0; i < nums2.length; i++) {
    m2[nums2[i]] = i;
  }
  return nums1.map((e) => m2[e]);
};
```
