### String
[537. Complex Number Multiplication ](https://leetcode.com/problems/complex-number-multiplication/description/)

 Given two strings representing two complex numbers.

You need to return a string representing their multiplication. Note i2 = -1 according to the definition.

**Example 1:**
```
Input: "1+1i", "1+1i"
Output: "0+2i"
Explanation: (1 + i) * (1 + i) = 1 + i2 + 2 * i = 2i, and you need convert it to the form of 0+2i.
```

**Example 2:**
```
Input: "1+-1i", "1+-1i"
Output: "0+-2i"
Explanation: (1 - i) * (1 - i) = 1 + i2 - 2 * i = -2i, and you need convert it to the form of 0+-2i.
```

**Note:**
```
    The input strings will not have extra blank.
    The input strings will be given in the form of a+bi, where the integer a and b will both belong to the range of [-100, 100]. And the output should be also in this form.
```

```python
# author long
class Solution(object):
    def complexNumberMultiply(self, a, b):
        """
        :type a: str
        :type b: str
        :rtype: str
        """
        pi_a=a.find('+') #plus_index
        pi_b=b.find('+')
        A,B,C,D=int(a[:pi_a]),int(a[pi_a+1:-1]),int(b[:pi_b]),int(b[pi_b+1:-1]) # 截取
        return "{real}+{image}i".format(real=A*C-B*D,image=A*D+B*C)  
```

[657. Judge Route Circle ](https://leetcode.com/problems/judge-route-circle/description/)

Initially, there is a Robot at position (0, 0). Given a sequence of its moves, judge if this robot makes a circle, which means it moves back to **the original place.**

The move sequence is represented by a string. And each move is represent by a character. The valid robot moves are `R` (Right), `L` (Left), `U` (Up) and `D` (down). The output should be true or false representing whether the robot makes a circle.



**Example 1:**
```
Input: "UD"
Output: true
```

**Example 2:**
```
Input: "LL"
Output: false
```

```python
# author long
class Solution(object):
    def judegeCircle(self, moves):
        """
        :type moves: str
        :rtype: bool
        """
        from collections import defaultdict
        d = defaultdict(int)
        for move in moves:
          d[move] += 1
        return d['D'] == d['U'] and d['L'] = d['R']
```

```java
// author: KillersDeath
class Solution {
    public boolean judgeCircle(String moves) {
        int x = 0, y = 0;
        for (char c : moves.toCharArray()) {
            if (c == 'R') x++;
            else if (c == 'L') x--;
            else if (c == 'U') y--;
            else if (c == 'D') y++;
        }
        return x == 0 && y == 0;
    }
}
```

[647. Palindromic Substrings ](https://leetcode.com/problems/palindromic-substrings/description/)

Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

**Example 1:**
```
Input: "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
```

**Example 2:**
```
Input: "aaa"
Output: 6
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
```

```python
# author: KillersDeath
class Solution:
    def countSubstrings(self, s):
        """
        :type s: str
        :rtype: int
        """
        N = len(s)
        cnt = 0
        for center in range(2*N - 1):
            left = int(center / 2)
            right = left + center % 2
            while left >= 0 and right < N and s[left] == s[right]:
                cnt += 1
                left -= 1
                right += 1
        return cnt
```

```java
// author: KillersDeath
class Solution {
    int cnt = 0;
    public int countSubstrings(String s) {
        if(s.length() == 0){ return cnt; }
        for(int i=0; i < s.length(); i++){ // 以 i 作为中间字符
            extentPalindromic(s, i, i); // 考虑单数的回文子串
            extentPalindromic(s, i, i+1); // 考虑双数的回文子串
        }
        return cnt;
    }
    public void extentPalindromic(String s, int left, int right){
        while(left >= 0 && right < s.length() && s.charAt(left) == s.charAt(right)){
            cnt++; left--; right++; //移动游标
        }
    }
}
```

[632. Smallest Range ](https://leetcode.com/problems/smallest-range/description/)

You have `k` lists of sorted integers in ascending order. Find the smallest range that includes at least one number from each of the `k` lists.

We define the range [a,b] is smaller than range [c,d] if `b-a < d-c` or `a < c` if `b-a == d-c`.

**Example 1:**
```
Input:[[4,10,15,24,26], [0,9,12,20], [5,18,22,30]]
Output: [20,24]
Explanation:
List 1: [4, 10, 15, 24,26], 24 is in range [20,24].
List 2: [0, 9, 12, 20], 20 is in range [20,24].
List 3: [5, 18, 22, 30], 22 is in range [20,24].
```

**note:**
- The given list may contain duplicates, so ascending order means >= here.
- 1 <= `k` <= 3500
- -10^5 <= `value of elements` <= 10^5.
- **For Java users, please note that the input type has been changed to List<List<Integer>>. And after you reset the code template, you'll see this point.**

```python
# author:
```

```java
// author: None
class Solution {
    public int[] smallestRange(List<List<Integer>> nums) {
	PriorityQueue<int[]> minHeap = new PriorityQueue<int[]>(nums.size(), new Comparator<int[]>(){
		public int compare(int[] o1, int[] o2) {
			return o1[0] - o2[0];
		}
	});

	int max = nums.get(0).get(0);
	for(int i=0; i<nums.size(); i++) {
		minHeap.add(new int[]{nums.get(i).get(0), i, 0});
		max = Math.max(max, nums.get(i).get(0));
	}

	int minRange = Integer.MAX_VALUE;
	int start = -1;
	while(minHeap.size() == nums.size()) {
		int[] t = minHeap.poll();
		if(max - t[0] < minRange) {
			minRange = max - t[0];
			start = t[0];
		}

		if(t[2]+1 < nums.get(t[1]).size()) {
			t[0] = nums.get(t[1]).get(t[2]+1);
			t[2] ++;
			minHeap.add(t);
			max = Math.max(max, t[0]);
		}
	}

	return new int[]{start, start+minRange};
}
}
```

[606. Construct String from Binary Tree](https://leetcode.com/problems/construct-string-from-binary-tree/description/)

You need to construct a string consists of parenthesis and integers from a binary tree with the preorder traversing way.

The null node needs to be represented by empty parenthesis pair `"()"`. And you need to omit all the empty parenthesis pairs that don't affect the one-to-one mapping relationship between the string and the original binary tree.

**Example 1:**
```
Input: Binary tree: [1,2,3,4]
       1
     /   \
    2     3
   /    
  4     

Output: "1(2(4))(3)"

Explanation: Originallay it needs to be "1(2(4)())(3()())",
but you need to omit all the unnecessary empty parenthesis pairs.
And it will be "1(2(4))(3)".
```

**Example 2:**
```
Input: Binary tree: [1,2,3,null,4]
       1
     /   \
    2     3
     \  
      4

Output: "1(2()(4))(3)"

Explanation: Almost the same as the first example,
except we can't omit the first parenthesis pair to break the one-to-one mapping relationship between the input and the output.
```

```python
# author:
```

```java
// author: KillersDeath
class Solution{
  public String tree2str(TreeNode t){
    if (t == null) return "";
    String result = t.val + "";
    if(t.right != null){
      return result + "(" + tree2str(t.left) + ")(" + tree2str(t.right) + ")";
    }else if (t.left != null){
      return result + "(" + tree2str(t.left) + ")";
    }else{
      return result;
    }
  }
}
```

```python
#author: sweatsword

# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):
    def tree2str(self, t):
        """
        :type t: TreeNode
        :rtype: str
        """
        res=[]
        self.pre_order(t,res)
        if res:
            return ''.join(res[1:-1])
        else:
            return ''

    def pre_order(self,T, res):
        if T:
            res.extend(['(', str(T.val)]) # 进入新树时(T.val
            if T.left:
                self.pre_order(T.left,res)
            elif T.right: # T只有右子树,加()
                res.extend(['(',')'])
            if T.right:
                self.pre_order(T.right,res)
            res.append(')') # 退出该数时加)

```

[551. Student Attendance Record I](https://leetcode.com/problems/student-attendance-record-i/description/)

You are given a string representing an attendance record for a student. The record only contains the following three characters:

1. **'A'** : Absent.
2. **'L'** : Late.
3. **'P'** : Present.
A student could be rewarded if his attendance record doesn't contain **more than one 'A' (absent)** or **more than two continuous 'L' (late)**.

You need to return whether the student could be rewarded according to his attendance record.

**Example 1:**
```
Input: "PPALLP"
Output: True
```

**Example 2:**
```
Input: "PPALLL"
Output: False
```

```python
# author:
class Solution(object):
    def checkRecord(self, s):
        """
        :type s: str
        :rtype: bool
        """
        L_nums = A_nums = 0
        flag = False
        for c in s:
            if c == 'A':
                A_nums += 1
                if A_nums > 1:
                    return False
            if c == 'L':
                if not flag:# 进入连续区
                    L_nums = 1
                    flag = True
                else:
                    # 连续区
                    L_nums += 1
                    if L_nums > 2:
                        return False
            else: # 退出连续区
                flag = False
                L_nums = 0
        return True
```

```java
// author: KillersDeath
class Solution {
  public boolean checkRecord(String s){
    int A=0, L=0;
    for(int i = 0; i < s.length(); i++){
      if(s.charAt(i) == 'L'){
        L ++;
        if (L > 2) return false;
      }else{
        L = 0;
        if(s.charAt(i) == 'A'){
          A ++;
          if(A > 1) return false;
        }
      }
    }
    return true;
  }
}
```

[583. Delete Operation for Two Strings](https://leetcode.com/problems/delete-operation-for-two-strings/description/)

Given two words word1 and word2, find the minimum number of steps required to make word1 and word2 the same, where in each step you can delete one character in either string.

**Example 1:**
```
Input: "sea", "eat"
Output: 2
Explanation: You need one step to make "sea" to "ea" and another step to make "eat" to "ea".
```

**Note:**
1. The length of given words won't exceed 500.
2. Characters in given words can only be lower-case letters.


```python
#author:sweatsword
class Solution(object):
    # d(i,j)= d(i+1,j+1) if A[i]=B[j]     d(app add)->d(pp dd)
    # d(i,j) =min d(i+1,j),d(j+1,i) if A[i]!=B[j] d(sea,tea)->min d(ea,tea),d(sea,ea)
    # d(i,j)=len(A)-j   if i=0    d('','sea')=3
    # d(i,j)=len(B)-i if j=0   
    def minDistance(self, word1, word2):
        """
        :type word1: str
        :type word2: str
        :rtype: int
        """
        self.word1=word1
        self.word2=word2
        self.d={}
        return self.Dist(len(word1)-1, len(word2)-1)

    def Dist(self,i, j):
        d=self.d
        if (i,j) not in d:  
            if i == -1:
                d[(i, j)] = j+1
                return d[(i, j)]
            elif j == -1:
                d[(i, j)] = i+1
                return d[(i, j)]
            elif self.word1[i] == self.word2[j]:
                d[(i, j)] = self.Dist(i - 1, j - 1)
                return d[(i, j)]
            elif self.word1[i] != self.word2[j]:
                d[(i, j)] = min(self.Dist(i - 1, j), self.Dist( i, j - 1)) + 1
                return d[(i, j)]
        return d[(i,j)]
```

```java
//author: KillersDeath
class Solution {
  public int minDistance(String word1, String word2){
    int len1 = word1.length(), len2 = word2.length();
    //保留最长公共子串长度
    int dp[][] = new int[len1+1][len2+1]

    for(int i=0; i<=len1; i++){
      for(int j=0; j<=len2; j++){
        dp[i][j] = word1.charAt(i-1) == word2.charAt(j-1) ? dp[i-1][j-1]+1 : Math.max(dp[i-1][j], dp[i][j-1]);
      }
    }
    return len1 + len2 - 2 * dp[len1][len2];
  }
}
```

[115. Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/description/)

Given a string S and a string T, count the number of distinct subsequences of S which equals T.

A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, `"ACE"` is a subsequence of `"ABCDE"` while `"AEC"` is not).

Here is an example:
**S** = `"rabbbit"`, **T** = `"rabbit"`

Return `3`.


```python
#author:
```

```java
//author: KillersDeath
class Solution {
    public int numDistinct(String s, String t) {
        int lenS=s.length(), lenT = t.length();
        int [][]mem = new int[lenT+1][lenS+1];

        //把第一行置为1，表示空字符串是任何字符的子序列
        for(int j=0; j<=lenS; j++){
            mem[0][j] = 1;
        }
        //依次遍历s和t
        for(int i=0; i<lenT; i++){
            for(int j=0; j<lenS; j++){
                if(t.charAt(i) == s.charAt(j)){
                    mem[i+1][j+1] = mem[i][j] + mem[i+1][j];
                }else{
                    mem[i+1][j+1] = mem[i+1][j];
                }
            }
        }
        return mem[lenT][lenS];
    }
}
```

[541. Reverse String II](https://leetcode.com/problems/reverse-string-ii/description/)

Given a string and an integer `k`, you need to reverse the first k characters for every `2k` characters counting from the start of the string. If there are less than `k` characters left, reverse all of them. If there are less than `2k` but greater than or equal to `k` characters, then reverse the first `k` characters and left the other as original.

**Example 1:**
```
Input: s = "abcdefg", k = 2
Output: "bacdfeg"
```

**Restrictions:**
1. The string consists of lower English letters only.
2. Length of the given string and k will in the range [1, 10000]

```python
#author:
```

```java
//author:
```

[557. Reverse Words in a String III](https://leetcode.com/problems/reverse-words-in-a-string-iii/description/)

Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

**Example 1:**
```
Input: "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"
```

**Note:**
1. In the string, each word is separated by single space and there will not be any extra space in the string.


```python
#author:
```

```java
//author:
```
