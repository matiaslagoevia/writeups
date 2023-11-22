# 271. Encode and Decode Strings

## Link

https://leetcode.com/problems/encode-and-decode-strings/description/

## Prompt

> Design an algorithm to encode a list of strings to a string. The encoded string is then sent over the network and is decoded back to the original list of strings.
>
> Implement the encode and decode methods.
>
> **You are not allowed to solve the problem using any serialize methods (such as eval).**

## Intuition

Trivial solution is to join and split on a character outside the alphabet. Non-trivial solution is to escape a separator on encoding, and to process words on decoding.

## Approach

We need to:

1. decide a separator/encoding approach
2. encode input strings into an output string, separated by the separator, and escaping non-delimiting instances of the separator
3. decode input string into output strings, processing what characters to keep & in what words

Choice of a separator is arbitrary — too short escapes too many non-delimiting instances, and too long makes the delimiters longer.
For encoding: we escape all non-delimiting instances first, and then join the array with the separator.
For decoding: we process each character one by one.

- if we're at `\`, look ahead and see if this is escaping our separator
- if we're at `sep[0]`, look ahead and see if this is the start of a delimiting instance; if it is, add the current word and clean up for the next one
- otherwise, add this character to the current word

## Complexity

### Time

> `O(N*K)`, where `N` is the number of strings and `K` is the length of the longest string

- For each of the `N` input strings to `encode()`, we look through at most `K` characters to escape the separator, and then join the `N` strings into the output string
- During decoding, we look through at most `N*K` characters of the encoded string as we process each of its characters

### Space

> `O(N*K)`, where `N` is the number of strings and `K` is the length of the longest string

- Encoding creates a new string holding at most `N*K` characters
- Decoding creates an outcome array of at most `N*K` characters, across different words

## Code

```js
const sep = "/:";
/**
 * Encodes a list of strings to a single string.
 *
 * @param {string[]} strs
 * @return {string}
 */
var encode = function (strs) {
  return strs.map((s) => s.replaceAll(sep, `\\${sep}`)).join(sep);
};

/**
 * Decodes a single string to a list of strings.
 *
 * @param {string} s
 * @return {string[]}
 */
var decode = function (s) {
  let ans = [],
    i = 0,
    curr = "";
  while (i < s.length) {
    if (s[i] === "\\") {
      if (s[i + 1] === sep[0] && s[i + 2] === sep[1]) {
        // escaped, add the sequence as is
        curr += sep;
        i += sep.length + 1;
      } else {
        curr += "\\";
        i++;
      }
    } else if (s[i] === sep[0] && s[i + 1] === sep[1]) {
      // word is over, reset
      ans.push(curr);
      curr = "";
      i += 2;
    } else {
      // character for word
      curr += s[i++];
    }
  }
  // add the last word
  ans.push(curr);
  return ans;
};

/**
 * Your functions will be called as such:
 * decode(encode(strs));
 */
```
