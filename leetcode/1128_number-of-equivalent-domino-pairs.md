# 1128. Number of Equivalent Domino Pairs

## Link

https://leetcode.com/problems/number-of-equivalent-domino-pairs/description

## Prompt

> Given a list of dominoes, dominoes[i] = [a, b] is equivalent to dominoes[j] = [c, d] if and only if either (a == c and b == d), or (a == d and b == c) - that is, one domino can be rotated to be equal to another domino.
>
> Return the number of pairs (i, j) for which 0 <= i < j < dominoes.length, and dominoes[i] is equivalent to dominoes[j].

## Intuition

Two dominoes are equal if they're the same (a == c and b == d) or "flipped" (a == d and b == c). If we know the total number of appearances for each domino type, we can form pairs out of those numbers.

## Approach

We need to:

1. serialize dominoes uniquely
2. have the total number of appearances for each unique domino
3. calculate the number of pairs from each unique domino's appearances

We'll serialize the dominoes in sorted order.
We can iterate over the input and populate a `Map` to keep track of appearances, with the key being the serialized domino.
To calculate number of pairs, we can use N choose R formula, with N = appearances, R = 2.

## Complexity

### Time

> `O(N)`, where `N` is the number of dominoes.

- We iterate over each domino to populate the map
- We iterate over at most `N` unique dominoes' values when calculating pairs

### Space

> `O(N)`, where `N` is the number of dominoes.

- The map holds at most `N` unique dominoes

## Code

```js
/**
 * @param {number[][]} dominoes
 * @return {number}
 */
var numEquivDominoPairs = function (dominoes) {
  const serialize = (a, b) => `${Math.min(a, b)},${Math.max(a, b)}`;
  let count = new Map();
  for (const [a, b] of dominoes) {
    const s = serialize(a, b);
    count.set(s, (count.get(s) || 0) + 1);
  }
  let total = 0;
  for (const v of count.values()) {
    total += (v * (v - 1)) / 2;
  }
  return total;
};
```
