# 346. Moving Average From Data Stream

## Link

https://leetcode.com/problems/moving-average-from-data-stream/description/

## Prompt

> Given a stream of integers and a window size, calculate the moving average of all integers in the sliding window.

> Implement the MovingAverage class:
>
> 1. MovingAverage(int size) Initializes the object with the size of the window size.
> 2. double next(int val) Returns the moving average of the last size values of the stream.

## Intuition

Because we're only interested in at most `size` elements at a time, we can use a fixed array using circular indexing to replace elements. Additionally, because only one element changes at a time, we can keep track of the current sum, adjust as necessary, and then return the average without having to add up the other `size-1` elements again.

## Approach

We need to be able to:

1. declare the fixed array
2. use circular indexing
3. track sum to avoid recalculating unchanged elements

We'll declare an array of the fixed size filled with zeroes initially.
For circular indexing, we'll keep track of how many times `next` was called, and have a current call's index be that number's remainder of the size of the array.
To track the sum, we'll subtract the "old" index value, add the "new" index value, and divide the sum by the number of "valid" elements we have in the array so far.

## Complexity

### Time

> `O(N)`, where `N` is the number of operations.

- We process `N` of them, each doing `O(1)` work

### Space

> `O(1)`.

- Other than on the first call where we allocate the array, each operation uses `O(1)` space

## Code

```js
/**
 * @param {number} size
 */
var MovingAverage = function (size) {
  this.nextCount = 0;
  this.values = Array(size).fill(0);
  this.sum = 0;
};

/**
 * @param {number} val
 * @return {number}
 */
MovingAverage.prototype.next = function (val) {
  let idx = this.nextCount % this.values.length;
  this.sum -= this.values[idx];
  this.sum += val;
  this.values[idx] = val;
  this.nextCount++;
  return this.sum / Math.min(this.nextCount, this.values.length);
};

/**
 * Your MovingAverage object will be instantiated and called as such:
 * var obj = new MovingAverage(size)
 * var param_1 = obj.next(val)
 */
```
