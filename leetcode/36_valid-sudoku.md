# 36. Valid Sudoku

## Link

https://leetcode.com/problems/valid-sudoku/description/

## Prompt

> Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:
>
> 1. Each row must contain the digits 1-9 without repetition.
> 2. Each column must contain the digits 1-9 without repetition.
> 3. Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without >repetition.
>
> **Note:** A Sudoku board (partially filled) could be valid but is not necessarily solvable.
> Only the filled cells need to be validated according to the mentioned rules.

## Intuition

We can use nested loops to process the rows & columns. During one of those, we can also process the subgrids. Processing means checking 1+ of the corresponding rules above. Ignore empty cells. Fail as soon as any of the rules is broken.

## Approach

We need to:

1. process rows
2. process columns
3. process subgrids

We'll combine row & subgrid processing, and do columns separately.
For each row, we prepare an empty seen array; populate, check and reject if a duplicate is seen.
Same for the column, just in a different loop (because of indexing).
For the subgrids, we'll have a 9x9 array where each cell is itself an empty seen array of 9 elements. In the same way as above, ew populate, check and reject if a duplicate is seen.

## Complexity

### Time

> `O(1)`.

- Input is always a 9x9 grid

### Space

> `O(1)`.

- Input is always a 9x9 grid

## Code

```js
/**
 * @param {character[][]} board
 * @return {boolean}
 */
var isValidSudoku = function(board) {
    const subgrid = [
      [
        Array(9).fill(0),Array(9).fill(0),Array(9).fill(0)
      ],
      [
        Array(9).fill(0),Array(9).fill(0),Array(9).fill(0)
      ],
      [
        Array(9).fill(0),Array(9).fill(0),Array(9).fill(0)
      ],
    ];

    // rows & subgrids
    for(let i=0; i<9; i++) {
      const seen = Array(9).fill(false);
      for(let j=0; j<9; j++) {
        const x = board[i][j] - 1; // 0 based
        if(isNaN(x)) continue;
        if(seen[x]) return false;
        if(subgrid[Math.floor(i / 3)][Math.floor(j / 3)][x]) return false;
        seen[x] = true;
        subgrid[Math.floor(i / 3)][Math.floor(j / 3)][x] = true;
      }
    }
    // columns
    for(let i=0; i<9; i++) {
      const seen = Array(9).fill(false);
      for(let j=0; j<9; j++) {
        const x = board[j][i] - 1; // 0 based
        if(isNaN(x)) continue;
        if(seen[x]) return false;
        seen[x] = true;
      }
    }
    return true;
};
```