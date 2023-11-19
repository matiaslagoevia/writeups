# Leetcode

My solutions to some Leetcode problems.

| **problem**                                                        | **takeaway**                                                                                                                         |
| ------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------ |
| [217. Contains Duplicate](217_contains-duplicate.md)               | `Set`s help with unique elements/constraints; `O(1)` insertion and searching.                                                        |
| [242. Valid Anagram](242_valid-anagram.md)                         | freq array trick on small & contiguous ranges vs `Map`s.                                                                             |
| [1. Two Sum](1_two-sum.md)                                         | check first then add avoids counting same index on single pass.                                                                      |
| [49. Group Anagrams](49_group-anagrams.md)                         | don't use arrays as map keys because of reference issues; favor counting sort over other approaches if possible to avoid log factor. |
| [541. Reverse String II](541_reverse-string-ii.md)                 | strings immutable, use `.split()` and `.join()` to move b/w array & string; last range `r=min(n-1, i+len-1)`.                        |
| [22. Generate Parentheses](22_generate-parentheses.md)             | stack unnecessary, order of checks matters for validity (`open < n` followed by `closed < open`)                                     |
| [937. Reorder Data in Log Files](937_reorder-data-in-log-files.md) | spread syntax; `s1.localeCompare(s2)`; `Number(s)` & `isNaN()`; `s.slice()` and `s.indexOf()`                                        |
