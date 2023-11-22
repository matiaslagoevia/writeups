# 994. Rotting Oranges

## Link

https://leetcode.com/problems/rotting-oranges/

## Prompt

> You are given an m x n grid where each cell can have one of three values:
>
> 0 representing an empty cell,
> 1 representing a fresh orange, or
> 2 representing a rotten orange.
>
> Every minute, any fresh orange that is 4-directionally adjacent to a rotten orange becomes rotten.
>
> Return the minimum number of minutes that must elapse until no cell has a fresh orange. If this is impossible, return -1.

## Intuition

We can search all elements of the grid to know the number of fresh oranges and each cell that has a rotten orange. We perform a BFS including all rotten cells for fresh oranges, marking them as rotten, for each minute. Once we're done, if there's no oranges left, we have our answer.

Some special cases where we wouldn't perform BFS:

- there's 0 fresh oranges => we're already done, 0 minutes
- there's 1+ fresh oranges but 0 rotten ones => it's impossible, -1 minutes

## Approach

We need to:

1. search all elements and find # of fresh oranges and rotten cells
2. handle special cases of no BFS
3. perform BFS
4. check number of fresh oranges left & return result

We can search all elements in O(M\*N) time with nested loops, counting the # of fresh oranges and all the rotten cells indices.
We can handle the special cases based on the returned values of the search.
We can perform the BFS as follows:

- a queue that will be populated with arrays
- each array will hold the cells that would be rotten at a specific minute
- we process each minutes' rotten cells, marking them as rotten, updating the # of fresh oranges & minutes processed

## Complexity

### Time

> `O(M*N)`, where `M` and `N` are the dimensions of the matrix.

- We search all `M*N` elements for the initial state
- We process at most `M*N` elements during our BFS

### Space

> `O(M*N)`, where `M` and `N` are the dimensions of the matrix.

- The rotten cells array holds at most all `M*N` elements
- The BFS queue holds at most all `M*N` across the minute arrays
- The next minute cells array holds at most all `M*N` elements across all BFS iterations

## Code

```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var orangesRotting = function(grid) {
    const M = grid.length, N = grid[0].length, dir=[[0,1],[1,0],[0,-1],[-1,0]];
    let {fresh, rottenCells} = getStartingState();
    if(fresh === 0) return 0;
    if(rottenCells.length === 0) return -1;

    let q = [rottenCells], minutes=0;
    while(q.length !== 0) {
      let currentMinCells = q.shift(), nextMinCells = [];
      for(const [r,c] of currentMinCells) {
        for(const [dr,dc] of dir) {
          const nr=r+dr, nc=c+dc;
          if(isInBounds(nr,nc) && grid[nr][nc] === 1) {
            grid[nr][nc] = 2;
            nextMinCells.push([nr,nc]);
            fresh--;
          }
        }
      }
      if(nextMinCells.length !== 0) {
        q.push(nextMinCells);
        minutes++;
      }
    }

    return fresh === 0 ? minutes : -1;

    function isInBounds(r, c) {
      return r >= 0 && r < M && c >= 0 && c < N;
    }

    function getStartingState() {
      let ans = {fresh: 0, rottenCells: []};
      for(let i=0; i<M; i++) {
        for(let j=0; j<N; j++) {
          if(grid[i][j] === 1) {
            ans.fresh++;
          } else if(grid[i][j] === 2) {
            ans.rottenCells.push([i,j]);
          }
        }
      }
      return ans;
    }
};
```