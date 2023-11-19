# 937. Reorder Data in Log Files

## Link

https://leetcode.com/problems/reorder-data-in-log-files/description/

## Prompt

> You are given an array of logs. Each log is a space-delimited string of words, where the first word is the identifier.
>
> There are two types of logs:
>
> 1. Letter-logs: All words (except the identifier) consist of lowercase English letters.
> 2. Digit-logs: All words (except the identifier) consist of digits.
>
> Reorder these logs so that:
>
> - The letter-logs come before all digit-logs.
> - The letter-logs are sorted lexicographically by their contents. If their contents >are the same, then sort them lexicographically by their identifiers.
> - The digit-logs maintain their relative ordering.
>
> Return the final order of the logs.

## Intuition

We'll sort the letter logs and have them be followed by the digit logs in the order they were seen. We'll use a string representation of the content of a log entry to be able to sort letter entries.

## Approach

We need to be able to:

1. process each log entry and classify it into digit/letter group
2. be able to sort letter entries accordingly
3. have sorted letter logs be followed by digit logs

We can classify each entry based on whether the content's first value is a number or not.
To sort letter entries, we'll first compare both entries' contents to each other, and if they are equal, we'll compare themselves (effectively comparing their identifiers).
When we're done, we'll use the spread syntax on the letter & digit arrays in the result.

## Complexity

### Time

> `O(N * K log(K)`, where `N` is the number of logs and `K` is the average log entry length

- Processing all entries into their arrays takes `O(N*K)` time
- Sorting takes `O(N * K log(K))` time

### Space

> `O(N * K)`, where `N` is the number of logs and `K` is the average log entry length

- Letter and digit arrays store `N*K` characters

## Code

```js
const reorderLogFiles = (logs) => {
  const content = (e) => e.slice(e.indexOf(" ") + 1);
  const isNum = (c) => !isNaN(Number(c.slice(0, c.indexOf(" "))));
  const compare = (a, b) => {
    const n = content(a).localeCompare(content(b));
    if (n !== 0) return n;
    return a.localeCompare(b);
  };

  const letters = [];
  const digits = [];
  for (const entry of logs) {
    const c = content(entry);
    if (isNum(c)) digits.push(entry);
    else letters.push(entry);
  }

  return [...letters.sort(compare), ...digits];
};
```
