# 1. Two Sum

## Link

https://leetcode.com/problems/two-sum/description/

## Prompt

> Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
> You may assume that each input would have exactly one solution, and you may not use the same element twice.
> You can return the answer in any order.

## Intuition

If we are currently on index `i` with `nums[i]=x`, we'll be able to form a sum equal to `target` with some index `j` if `nums[j]=target-x`. If we're able to remember the numbers we have seen so far, as we iterate over each index `i` we can see if we already have seen some `j` that satisfies the condition above.

## Approach

We need to be able to:

1. check whether we've seen a number before
2. mark a number as seen, and it's index

`Map`s are particularly useful to associate one value to another.
We want to perform our checks based on value, not index, so we'll associate `<value>-><index>`.
Because the values' range is too sparse, we choose a map over an array.
To avoid using the same index twice, we check for `target-x` first and then mark `x` as seen.

## Complexity

### Time

> `O(N)`, where `N` is the number of elements in `nums`.

- We process at most `N` numbers.
- `Map` lookup and insertion are O(1) on average.

### Space

> `O(N)`, where `N` is the number of elements in `nums`.

- We store at most `N` numbers in the set.

## Code

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function (nums, target) {
  const seen = new Map();
  for (let i = 0; i < nums.length; i++) {
    const x = nums[i],
      remaining = target - x;
    if (seen[remaining] !== undefined) {
      return [i, seen[remaining]];
    }
    seen[x] = i;
  }
};
```
