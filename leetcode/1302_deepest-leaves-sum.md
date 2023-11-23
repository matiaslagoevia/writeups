# 1302. Deepest Leaves Sum

## Link

https://leetcode.com/problems/deepest-leaves-sum/description

## Prompt

> Given the root of a binary tree, return the sum of values of its deepest leaves.

## Intuition

We traverse the tree with DFS, keeping track of the deepest level seen so far and all the nodes' values for leaves at that level. After we're done, we return the sum of all those values.

## Approach

We need to:

1. dfs traversal aware of depth level
2. processing/updating the max level and it's values
3. return the sum of all the final values

We can use a recursive DFS w/ a depth parameter.
When we get to a leaf:

- if the depth is lesser than the max depth so far, do nothing
- if the depth is equal to the max depth so far, add this node's value to the list
- if the depth is greater than the max depth, update it and set this as the only value so far

Finally, we add all the values and return the sum.

## Complexity

### Time

> `O(N)`, where `N` is the number of nodes.

- BFS visits all `N` nodes of the tree
- The result consists of a sum of at most `N` elements

### Space

> `O(N)`, where `N` is the number of nodes.

- The values array holds at most `N` elements
- The call stack for `dfs()` holds at most `N` calls at a time.

## Code

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var deepestLeavesSum = function (root) {
  let maxDepth = 0,
    values = [];
  dfs(root, 0);
  return values.reduce((a, b) => a + b, 0);

  function dfs(node, depth) {
    if (!node) return;
    if (!node.left && !node.right) {
      if (depth > maxDepth) {
        values = [node.val];
        maxDepth = depth;
      } else if (depth === maxDepth) {
        values.push(node.val);
      }
      return;
    }
    node.left && dfs(node.left, depth + 1);
    node.right && dfs(node.right, depth + 1);
  }
};
```
