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
# author：KillersDeath
class Solution(object):
    def widthOfBinaryTree(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if root is None: return 0
        self.width = 1
        next_nodes = {0:root}
        while next_nodes:
            next_nodes = self.nextLevel(next_nodes)
        return self.width

    def nextLevel(self, ind_node):
        from collections import OrderedDict
        # 有序字典，只需统计头尾的index差值即可
        next_nodes = OrderedDict()
        min_ind, max_ind, min_flag= 0, 0, 1
        for ind, node in ind_node.items():
            if node is not None:
                if min_flag:
                    min_ind, min_flag = ind, 0
                if node.left is not None:   # 向下一层，index 左孩子index翻倍
                    next_nodes[2*ind] = node.left
                if node.right is not None:  # 向下一层，index 右孩子index翻倍+1
                    next_nodes[2*ind+1] = node.right
                max_ind = ind
        self.width = max(self.width, max_ind - min_ind + 1)
        return next_nodes
```

```java
public class Solution{
    //author:Then
    public int widthOfBinaryTree(TreeNode root) {
        if(root == null){
            return 0;
        }
        int result = 1;
        int left = -1,right;
        List<TreeNode> treeNodeList = new LinkedList<>();
        root.val = 0;
        treeNodeList.add(root);
        int size;
        while((size = treeNodeList.size())!=0){
            TreeNode treeNode = null;
            for (int i = 0; i < size; i++) {
                treeNode = treeNodeList.remove(0);
                if(treeNode.left!=null){
                    treeNode.left.val = treeNode.val*2;
                    treeNodeList.add(treeNode.left);
                }
                if(treeNode.right!=null){
                    treeNode.right.val = treeNode.val*2+1;
                    treeNodeList.add(treeNode.right);
                }
                if(left == -1){
                    left = treeNode.val;
                }
            }
            right = treeNode.val;
            result = Math.max(result,right-left+1);
            left = -1;
        }
        return result;
    }
}
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
# author sweatsword
class TreeNode(object):
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
class Solution(object):
    def constructMaximumBinaryTree(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        if not nums:
            return
        max_num=max(nums)
        k=nums.index(max_num)
        T=TreeNode(max_num)
        T.left=self.constructMaximumBinaryTree(nums[:k])
        T.right=self.constructMaximumBinaryTree(nums[k+1:])
        return T
```

[111. Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/description/)

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

```python
# author sweatsword
class Solution(object):
    def minDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:return 0
        from collections import deque
        Q = deque([(root, 1)])  # Queue for Width-First-Travelsal
        while Q:
            T, level = Q.popleft()  # 出队
            if T.right==T.left==None:   # Fisrt time visit a leaf node ,return  
                return level
            if T.left:
                Q.append((T.left, level + 1))
            if T.right:
                Q.append((T.right, level + 1))
        return -1
```

```java
//author Then
class Solution {
    public int minDepth(TreeNode root) {
       if(root == null){
            return 0;
        }
        Queue<TreeNode> treeNodeQueue = new LinkedList<>();
        treeNodeQueue.add(root);
        int size,level=0;
        while((size = treeNodeQueue.size())!=0){
            level++;
            for (int i = 0; i < size; i++) {
                TreeNode treeNode = treeNodeQueue.poll();
                if(treeNode.left==null && treeNode.right==null){
                    return level;
                }
                if(treeNode.left!=null){
                    treeNodeQueue.offer(treeNode.left);
                }
                if(treeNode.right!=null){
                    treeNodeQueue.offer(treeNode.right);
                }
            }
        }
        return -1;
    }
}

```

[99. Recover Binary Search Tree ](https://leetcode.com/problems/recover-binary-search-tree/description/)
Two elements of a binary search tree (BST) are swapped by mistake.

Recover the tree without changing its structure.
Note:
A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?

```python
# author sweatsword
class Solution(object):
    def recoverTree(self, root):
        """
        :type root: TreeNode
        :rtype: void Do not return anything, modify root in-place instead.
        """
        # Inorder-traversal of BFS are ascending series.
        # Find two elements which violate this rule,then swap them
        self.pre = self.mistake1 =self.mistake2=None
        self.inoder(root)
        self.mistake1.val, self.mistake2.val = self.mistake2.val, self.mistake1.val # swap
    def inoder(self, T):
        if T:
            if T.left:
                self.inoder(T.left)
            if not self.pre:
                self.pre = T
            if T.val < self.pre.val:
                if not self.mistake1:  # violation 1
                    self.mistake1=self.pre
                    self.mistake2=T
                else:
                    self.mistake2=T # violation 2
            self.pre=T
            if T.right:
                self.inoder(T.right)
```

```java
author: KillersDeath
class Solution {
    TreeNode firstNode, secondNode;
    TreeNode preNode = new TreeNode(Integer.MIN_VALUE);

    public void recoverTree(TreeNode root) {
        //顺序遍历找到不合法节点
        traverse(root);
        // 交换值
        int tmp = firstNode.val;
        firstNode.val = secondNode.val;
        secondNode.val = tmp;
    }

    private void traverse(TreeNode root){
        if(root == null)
            return ;
        traverse(root.left);

        if(firstNode == null && preNode.val >= root.val){
            firstNode = preNode;
        }

        if(firstNode != null && preNode.val >= root.val){
            secondNode = root;
        }
        preNode = root;
        traverse(root.right);
    }
}
```

[297. Serialize and Deserialize Binary Tree ](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/description/)
Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

For example, you may serialize the following tree
```
   1
  / \
 2    3
     / \
    4   5
```
as `"[1,2,3,null,null,4,5]"`, just the same as [how LeetCode OJ serializes a binary tree](https://leetcode.com/faq/#binary-tree). You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

**Note:** Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.

**Credits**:Special thanks to @Louis1992 for adding this problem and creating all test cases.

```python
```

```java
author:
```

[669. Trim a Binary Search Tree](https://leetcode.com/problems/trim-a-binary-search-tree/description/)
Given a binary search tree and the lowest and highest boundaries as L and R, trim the tree so that all its elements lies in `[L, R]` (R >= L). You might need to change the root of the tree, so the result should return the new root of the trimmed binary search tree.

**Example 1:**
```
Input:
    1
   / \
  0   2

  L = 1
  R = 2
Output:
    1
      \
       2
```

**Example 2:**
```
Input:
    3
   / \
  0   4
   \
    2
   /
  1

  L = 1
  R = 3
Output:
      3
     /
   2   
  /
 1
```


```python
# author: sweatsword
class Codec:
    def serialize(self, root):
        """Encodes a tree to a single string.

        :type root: TreeNode
        :rtype: str
        """
        from collections import deque, defaultdict
        res = defaultdict(str)
        if not root:
            return res
        Q = deque([(root, 1)])  # Queue for Width-First-Travelsal
        while Q:
            T, pos = Q.popleft()  # 出队
            res[pos] = T.val
            if T.left:
                Q.append((T.left, 2 * pos))
            if T.right:
                Q.append((T.right, 2 * pos + 1))
        return res

    def deserialize(self, data):
        """Decodes your encoded data to tree.

        :type data: str
        :rtype: TreeNode
        """
        if not data: return None
        T = self.construct(data, 1)
        Solution().WFS(T)
        return T

    def construct(self, data, k): # recursively construct bi-tree
        T = TreeNode(data[k])
        if data[2 * k]:
            T.left = self.construct(data, 2 * k)
        if data[2 * k + 1]:
            T.right = self.construct(data, 2 * k + 1)
        return T

```

```java
//author:
```

[515. Find Largest Value in Each Tree Row](https://leetcode.com/problems/find-largest-value-in-each-tree-row/description/)
You need to find the largest value in each row of a binary tree.

**Example :**
```
Input:

          1
         / \
        3   2
       / \   \  
      5   3   9

Output: [1, 3, 9]
```

```python
# author:
```

```java
//author:
```

[145. Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/description/)
Given a binary tree, return the postorder traversal of its nodes' values.

For example:
Given binary tree `{1,#,2,3}`,

**Example :**
```
Input:

    1
     \
      2
     /
    3

Output: [3, 2, 1]
```

**Note:** Recursive solution is trivial, could you do it iteratively?

```python
# author:
```

```java
//author:
```
