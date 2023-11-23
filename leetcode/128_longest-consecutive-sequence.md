# 128. Longest Consecutive Sequence

## Link

https://leetcode.com/problems/longest-consecutive-sequence/description/

## Prompt

> Given an unsorted array of integers `nums`, return the length of the longest consecutive elements sequence.
> You must write an algorithm that runs in O(n) time.

## Intuition

A sequence will have a starting point (it's smallest number) and 0+ consecutive numbers after that one. For all possible starting points, compute their consecutive sequence length and return the longest one. A number that isn't a starting point will only be considered within one sequence — therefore, an `O(N)` time solution is possible.

## Approach

We need to:

1. determine possible starting points
2. for each starting point, compute it's consecutive sequence length

We'll put `nums` into a hashset, for `O(1)` lookups of unique elements, and iterate over it's contents.
A number `x` is a starting point if there's no `x-1` present. We can compute it's consecutive sequence by repetitively asking if `x+1` is present, and updating `x`, while tracking the length. When there's no `x+1` present, we update our answer if necessary.

## Complexity

### Time

> `O(N)`, where `N` is the length of `nums`.

- We construct the hashset of at most `N` elements in `O(N)` time
- We consider each element of the set at most once
  - Non-starting points are considered only within one starting point's sequence
  - Starting points are only considered once (themselves)

### Space

> `O(N)`, where `N` is the length of `nums`.

- We store at most `N` elements in the set

## Code

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var longestConsecutive = function (nums) {
  const s = new Set(nums);
  let best = 0;
  // only consider unique values within input
  for (let x of s) {
    // only consider possible starting points
    if (!s.has(x - 1)) {
      let len = 1;
      // look to grow sequence from this start point
      while (s.has(x + 1)) {
        len++;
        x++;
      }
      best = Math.max(best, len);
    }
  }
  return best;
};
```
