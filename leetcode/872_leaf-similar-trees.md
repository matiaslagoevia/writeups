# 872. Leaf Similar Trees

## Link

https://leetcode.com/problems/leaf-similar-trees/

## Prompt

> Consider all the leaves of a binary tree, from left to right order, the values of those leaves form a leaf value sequence.
> Two binary trees are considered leaf-similar if their leaf value sequence is the same.
> Return true if and only if the two given trees with head nodes root1 and root2 are leaf-similar.

## Intuition

We can process the first tree and store it's leaf sequence; as we process the second tree, if the current leaf doesn't match the same index on the first tree, we can terminate early (false). After we finish processing the second tree, if there are no other leaves from the first tree that we haven't processed, we return true.

## Approach

We need to be able to:

1. process a tree to find it's leaves
2. store the first tree's leaf sequence
3. check the second tree's leaves against the first tree's leaf sequence
4. check there's no extra first tree leaves

We can use DFS to process a tree and find its leaves.
If it's the first tree, we'll push the leaf to an array.
If it's the second tree, we'll check against a current index and increment it.
After processing the second tree, we'll check whether the current index matches the length of the leaf sequence (i.e. no extra elements).

## Complexity

### Time

> `O(N+M)`, where `N` and `M` are the nodes in the first and second tree respectively

- For the first tree, we process `N` nodes
- For the second tree, we process at most `M` nodes

### Space

> `O(N+M)`, where `N` and `M` are the nodes in the first and second tree respectively

- During the first tree traversal, the call stack has a depth of at most `N`
- During the second tree traversal, the call stack has a depth of at most `M`
- The leaf sequence array has at most `N` elements

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
 * @param {TreeNode} root1
 * @param {TreeNode} root2
 * @return {boolean}
 */
var leafSimilar = function (root1, root2) {
  const a = [];
  let i = 0;
  dfs(root1, true);
  return dfs(root2, false) && i === a.length;

  function dfs(n, isFirst) {
    if (!n) return true;
    if (!n.left && !n.right) {
      if (isFirst) {
        a.push(n.val);
        return true;
      }
      if (a[i++] !== n.val) {
        return false;
      }
      return true;
    }
    return dfs(n.left, isFirst) && dfs(n.right, isFirst);
  }
};
```
