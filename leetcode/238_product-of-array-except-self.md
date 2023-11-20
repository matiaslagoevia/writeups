# 238. Product of Array Except Self

## Link

https://leetcode.com/problems/product-of-array-except-self/description/

## Prompt

> Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].
>
> The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.
>
> You must write an algorithm that runs in O(n) time and without using the division operation.

## Intuition

For a given index `i`, `result[i] = product[0:i) * product(i,n)`, or `result[i] = pre[i-1] * post[i+1]`. We can populate `pre` forwards, and `post` backwards in a single pass. Though, we can apply each contribution separately to the result directly.

## Approach

We need to be able to:

1. process each `pre` contribution
2. process each `post` contribution

We'll have the result be filled with `1`s initially.

1. `pre`:

- `pre = 1`
- for `0 <= i < n`, `result[i] *= pre; pre *= nums[i]`

2. `post`:

- `post = 1`
- on `n > i >= 0`, `result[i] *= post; post *= nums[i]`

## Complexity

### Time

> `O(N)`, where `N` is the number of elements

- For `pre`, we process `N` elements' contribution to the result
- For `post`, we process `N` elements' contribution to the result

### Space

> `O(1)`

- We don't use any extra space (besides the result array) that depends on the input size

## Code

```js
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var productExceptSelf = function (nums) {
  const N = nums.length,
    ans = Array(N).fill(1);
  let pre = 1;
  for (let i = 0; i < N; i++) {
    ans[i] *= pre;
    pre *= nums[i];
  }
  let post = 1;
  for (let i = N - 1; i >= 0; i--) {
    ans[i] *= post;
    post *= nums[i];
  }
  return ans;
};
```
