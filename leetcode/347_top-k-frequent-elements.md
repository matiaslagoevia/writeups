# 347. Top K Frequent Elements

## Link

https://leetcode.com/problems/top-k-frequent-elements/description/

## Prompt

> Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

## Intuition

If we know the each number's frequency, we can group frequencies together and iterate to find the top k values.

## Approach

We need to be able to:

1. know each number's frequency
2. group frequencies together
3. iterate groups to find k values

We can use a `Map` as we iterate over the array to associate number -> frequency.
We can use a `Map` as we iterate over our frequency map to group frequency -> numbers w/ that frequency.
We can iterate backwards from N and populate results until we have k elements. We start from N as that is the highest possible frequency for a number in the input (i.e. it's the same number 1+ times).

## Complexity

### Time

> `O(N)`, where `N` is the length of the array.

- We process N numbers to form the frequency map
- We process at most N numbers to form the frequency groups
- We process at most N numbers to get the K top values

### Space

> `O(N)`, where `N` is the length of the array.

- We store at most N numbers in the frequency map
- We store at most N numbers across at most N buckets

## Code

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
var topKFrequent = function (nums, k) {
  const freq = new Map();
  const bucket = [];

  for (const n of nums) {
    freq.set(n, (freq.get(n) || 0) + 1);
  }

  for (const [num, count] of freq) {
    bucket[count] = (bucket[count] || new Set()).add(num);
  }

  const ans = [];
  for (let i = bucket.length - 1; i > 0; i--) {
    if (bucket[i]) ans.push(...bucket[i]);
    if (ans.length === k) break;
  }

  return ans;
};
```
