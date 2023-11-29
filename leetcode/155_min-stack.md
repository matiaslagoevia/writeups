# 115. Min Stack

## Link

https://leetcode.com/problems/min-stack/description

## Prompt

> Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.
>
> Implement the MinStack class:
>
> - MinStack() initializes the stack object.
> - void push(int val) pushes the element val onto the stack.
> - void pop() removes the element on the top of the stack.
> - int top() gets the top element of the stack.
> - int getMin() retrieves the minimum element in the stack.
>
> You must implement a solution with O(1) time complexity for each function.

## Intuition

Though O(1) `getMin` seems tricky at first, it's doable. Elements are inserted/removed one at a time, and only in a specific position (the end). That means that an insertion/removal won't affect anything other than the last element. For insertions, the new minimum is the smallest value between the one being inserted and the minimum seen for the current last element; for removals, the minimum the one for the new last element.

Basically, though `getMin` would seem to have to be `O(N)` each time something was added/removed, because insertions and removals only happen in a fixed place/affect at most one element, the rest of the problem state is unaffected and we have an `O(1)` comparison between two values.

## Approach

We need to:

1. decide between a LL or array based implementation
2. for each value, store the minimum seen at that point
3. implement operations accordingly

Though array's push() has `O(N)` complexity in cases where a resize is needed, it's still more efficient than a LL implementation due to a lower constant factor (cache/memory contiguous, no object references, etc) — so, we'll go with that.
We'll store two separate arrays: one that tracks the values, and another one that stores the minimum values and their count — this helps us avoid unnecessary bloat of the minimums array when a minimum happens repeatedly.

- `top()` will return the last element of the values array
- `push()` will push the value to the end of the values array, and either increment the count of the last minimum or push a new minimum with a count of 1
- `pop()` will pop the value from the values array and either decrement the count of the last minimum or pop its subarray.
- `getMin()` will return the last element (value) on the minimums array

## Complexity

### Time

> `O(1)`.

- Despite resizing, `Array.push()` has amortized `O(1)` complexity
- Each operation performs `O(1)` work

### Space

> `O(N)`, where `N` is the number of elements pushed to the stack

- We store at most `N` values in the values array
- We store at most `N` subarrays in the minimums array

## Code

```js
var MinStack = function () {
  this.values = [];
  this.min = [];
};

/**
 * @param {number} val
 * @return {void}
 */
MinStack.prototype.push = function (val) {
  this.values.push(val);
  const lastMinValue =
    this.min.length === 0 ? Infinity : this.min[this.min.length - 1][0];
  if (val < lastMinValue) {
    this.min.push([val, 1]);
  } else {
    this.min[this.min.length - 1][1]++;
  }
};

/**
 * @return {void}
 */
MinStack.prototype.pop = function () {
  const val = this.values.pop();
  const lastMinCount = this.min[this.min.length - 1][1];
  if (lastMinCount === 1) {
    this.min.pop();
  } else {
    this.min[this.min.length - 1][1]--;
  }
  return val;
};

/**
 * @return {number}
 */
MinStack.prototype.top = function () {
  return this.values[this.values.length - 1];
};

/**
 * @return {number}
 */
MinStack.prototype.getMin = function () {
  return this.min[this.min.length - 1][0];
};

/**
 * Your MinStack object will be instantiated and called as such:
 * var obj = new MinStack()
 * obj.push(val)
 * obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.getMin()
 */
```
