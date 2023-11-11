# 217. Contains Duplicate

## Link

https://leetcode.com/problems/contains-duplicate/description/

## Prompt

> Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

## Intuition

If we can remember what numbers we've seen so far, we can stop immediately after seeing a number we've seen before. If we don't see a number we've seen before, we know every element is distinct.

## Approach

We need to be able to:

1. check whether we've seen a number before
2. mark a number as seen

`Set`s are particularly useful to track unique values.
We'll use their `has()` and `add()` methods for our needs above.

## Complexity

### Time

> `O(N)`, where `N` is the number of elements in `nums`.

- We process at most `N` numbers.
- `Set.has()` and `Set.add()` have O(1) average complexity.

### Space

> `O(N)`, where `N` is the number of elements in `nums`.

- We store at most `N` numbers in the set.

## Code

```js
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var containsDuplicate = function (nums) {
  const seen = new Set();
  for (let x of nums) {
    if (seen.has(x)) return true;
    seen.add(x);
  }
  return false;
};
```
