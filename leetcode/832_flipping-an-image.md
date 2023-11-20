# 832. Flipping an Image

## Link

https://leetcode.com/problems/flipping-an-image/

## Prompt

> Given an n x n binary matrix image, flip the image horizontally, then invert it, and return the resulting image.
>
> To flip an image horizontally means that each row of the image is reversed.
> For example, flipping [1,1,0] horizontally results in [0,1,1].
>
> To invert an image means that each 0 is replaced by 1, and each 1 is replaced by 0.
> For example, inverting [0,1,1] results in [1,0,0].

## Intuition

Basically following the prompt, noticing that reversal & inversion can be done at the same time as we iterate through each row.

## Approach

We need to be able to:

1. reverse a row and invert the contents

We can have a left and right pointer that move inwards, swapping the opposite contents.

## Complexity

### Time

> `O(N^2)`, where `N` is the dimension of the image matrix.

- For each of the `N` rows, we reverse & swap `N` elements in one pass

### Space

> `O(1)`

- The space used by our variables is independent of the size of our input

## Code

```js
/**
 * @param {number[][]} image
 * @return {number[][]}
 */
var flipAndInvertImage = function (image) {
  const N = image.length;
  for (let i = 0; i < N; i++) {
    for (let l = 0, r = N - 1; l <= r; l++, r--) {
      [image[i][l], image[i][r]] = [!image[i][r], !image[i][l]];
    }
  }
  return image;
};
```
