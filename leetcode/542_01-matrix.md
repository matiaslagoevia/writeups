# 542. 01 Matrix

## Link

https://leetcode.com/problems/01-matrix/description

## Prompt

> Given an m x n binary matrix mat, return the distance of the nearest 0 for each cell.
> The distance between two adjacent cells is 1.

## Intuition

It could be possible to do a multisource BFS from all zeroes, visiting other nodes and marking each depth for them. It's also possible to do a DP approach — if I'm at a given cell, I could've arrived here from 4 directions: the shortest path would be 1 + the minimum of all those other cells' distance to a zero.

With all 4 directions at once, it's difficult to know how to iterate over the matrix to compute values. To avoid that, it's possible to split the work into 2 directions that modify the answer accordingly.

## Approach

We need to:

1. split the 4 directions so that the recursive DP relationship is clear
2. reflect the minimum distance across all 4 directions

It's possible to iterate over the matrix in a down-and-right and a up-and-left directions. For down-and-right, we'll consider the previous states to be up and left (i.e. we're coming from those directions); viceversa for up-and-left.
In the first pass, for non-zero matrix values we'll set a high value (Infinity) and then for each direction we'll update it if that direction is closer to a zero.
For the second pass, we'll do the same w/o setting the high value (to avoid overriding a possible minimum value of the first pass).

## Complexity

### Time

> `O(M*N)`, where `M` and `N` are the matrix's dimensions.

- Each traversal looks at `M*N` elements separately

### Space

> `O(1)`.

- We operate on the input array directly.

## Code

```js
/**
 * @param {number[][]} mat
 * @return {number[][]}
 */
var updateMatrix = function (mat) {
  const M = mat.length,
    N = mat[0].length;

  // right & down traversal
  for (let r = 0; r < M; r++) {
    for (let c = 0; c < N; c++) {
      if (mat[r][c] === 0) continue;
      mat[r][c] = Infinity;
      if (r - 1 >= 0) mat[r][c] = Math.min(mat[r][c], 1 + mat[r - 1][c]);
      if (c - 1 >= 0) mat[r][c] = Math.min(mat[r][c], 1 + mat[r][c - 1]);
    }
  }

  // left & up traversal
  for (let r = M - 1; r >= 0; r--) {
    for (let c = N - 1; c >= 0; c--) {
      if (mat[r][c] === 0) continue;
      if (r + 1 < M) mat[r][c] = Math.min(mat[r][c], 1 + mat[r + 1][c]);
      if (c + 1 < N) mat[r][c] = Math.min(mat[r][c], 1 + mat[r][c + 1]);
    }
  }
  return mat;
};
```
