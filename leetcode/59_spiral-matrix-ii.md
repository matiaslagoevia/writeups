# 59. Spiral Matrix II

## Link

https://leetcode.com/problems/spiral-matrix-ii/description/

## Prompt

> Given a positive integer n, generate an n x n matrix filled with elements from 1 to n2 in spiral order.

## Intuition

The spiral movement loops in directions: right, down, left, up, (...). Each direction loop works as a wrapper/bound to the next one, limiting it's movements. For each direction, move one step further than allowed, then undo it and prepare for the next direction.

## Approach

We need to:

1. repeat spirals until all N^2 cells/numbers are processed
2. process the b'th spiral

We can loop spirals until we've processed all N^2 cells.
For a given spiral, we move in all directions, marking each cell.
For the b'th spiral, it's bounds will be narrower by b cells in all directions.

## Complexity

### Time

> `O(N^2)`, where `N` is the dimension of the square matrix.

- We process each of the N^2 cells

### Space

> `O(1)` extra space.

- Other than the result array, our variables aren't proportionate to the size of the input

## Code

```js
/**
 * @param {number} n
 * @return {number[][]}
 */
var generateMatrix = function(n) {
    const a = Array(n).fill([]).map(_ => Array(n));
    let i=1, r=0, c=0, b=0;
    while(i <= n*n) {
      // try right
      while(c < n-b) a[r][c++] = i++;
      c--; r++;
      // try down
      while(r < n-b) a[r++][c] = i++;
      r--; c--;
      // try left
      while(c >= 0+b) a[r][c--] = i++;
      c++; r--;
      // try up
      while(r > 0+b) a[r--][c] = i++;
      r++; c++;
      
      b++;
    }
    return a;
};
```