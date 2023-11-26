# 167. Two Sum II — Input Array Is Sorted

## Link

https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/

## Prompt

> Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 < numbers.length.
>
> Return the indices of the two numbers, index1 and index2, added by one as an integer array [index1, index2] of length 2.
>
> The tests are generated such that there is exactly one solution. You may not use the same element twice.
>
> Your solution must use only constant extra space.

## Intuition

Because the array is sorted, we can start at the smallest and largest elements, and compare to the target sum. If we're short, we'll take a larger small element next time (i.e. we're now looking at the next smallest element); if we're long, we'll take a smaller large element next time (i.e. we're now looking at the next largest element). We continue this process as long as there's 2 elements to compare.

## Approach

We need to be able to:

1. start at the smallest and largest element
2. compare to target sum and adjust them accordingly

We'll start with the `l=0` and `r=N-1`, and do the following while `l<r`.

- Store the sum `x=a[l]+a[r]`.
- If `x>target`, then `r--`
- If `x<target`, then `l++`
- Otherwise, return `[l+1,r+1]` (1-indexed)

## Complexity

### Time

> `O(N)`, where `N` is the number of elements.

- We'll compare at most `N` large/small elements, doing `O(1)` work on each

### Space

> `O(1)`.

- Our space is independent of the input size

## Code

```js
/**
 * @param {number[]} numbers
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function (numbers, target) {
  let l = 0,
    r = numbers.length - 1;
  while (l < r) {
    const x = numbers[l] + numbers[r];
    if (x > target) {
      r--;
    } else if (x < target) {
      l++;
    } else {
      return [l + 1, r + 1];
    }
  }
  return null;
};
```
