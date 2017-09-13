### Tree
[662. Maximum Width of Binary Tree ](https://leetcode.com/problems/maximum-width-of-binary-tree/description/)

Given a binary tree, write a function to get the maximum width of the given tree. The width of a tree is the maximum width among all levels. The binary tree has the same structure as a **full binary tree**, but some nodes are `null`.

The width of one level is defined as the length between the end-nodes (the leftmost and right most `non-null` nodes in the level, where the `null` nodes between the end-nodes are also counted into the length calculation.

**Example 1:**
```
Input:

           1
         /   \
        3     2
       / \     \  
      5   3     9

Output: 4
Explanation: The maximum width existing in the third level with the length 4 (5,3,null,9).
```

**Example 2:**
```
Input:

          1
         /  
        3    
       / \       
      5   3     

Output: 2
Explanation: The maximum width existing in the third level with the length 2 (5,3).
```

**Example 3:**
```
Input:

          1
         / \
        3   2
       /        
      5      

Output: 2
Explanation: The maximum width existing in the second level with the length 2 (3,2).
```

**Example 4:**
```
Input:

          1
         / \
        3   2
       /     \  
      5       9
     /         \
    6           7
Output: 8
Explanation:The maximum width existing in the fourth level with the length 8 (6,null,null,null,null,null,null,7).
```

**Note:**
1. Answer will in the range of `32-bit` signed integer.

```python
# author
```

```java
# author
```

[654. Maximum Binary Tree ](https://leetcode.com/problems/maximum-binary-tree/description/)

Given an integer array with no duplicates. A maximum tree building on this array is defined as follow:

1. The root is the maximum number in the array.
2. The left subtree is the maximum tree constructed from left part subarray divided by the maximum number.
3. The right subtree is the maximum tree constructed from right part subarray divided by the maximum number.
Construct the maximum tree by the given array and output the root node of this tree.

**Example 1:**
```
Input: [3,2,1,6,0,5]
Output: return the tree root node representing the following tree:

      6
    /   \
   3     5
    \    /
     2  0   
       \
        1
```

**Note:**
1. The size of the given array will be in the range [1,1000].

```python
# author
```

```java
# author
```
