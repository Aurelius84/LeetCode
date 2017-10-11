### Tree
[525. Contiguous Array](https://leetcode.com/problems/contiguous-array/description/)

Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

**Example 1:**
```
Input: [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
```

**Example 2:**
```
Input: [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
```

**Note:**
1. The length of the given binary array will not exceed 50,000.

```python
# author：
```

```java
// author:
```

[76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/description/)

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

**Example 1:**
```
S = "ADOBECODEBANC"
T = "ABC"
Minimum window is "BANC".
```

**Note:**
1. If there is no such window in S that covers all characters in T, return the empty string `""`.
2. If there are multiple such windows, you are guaranteed that there will always be only one unique minimum window in S.

```python
# author：
```

```java
// author:
```

[645. Set Mismatch](https://leetcode.com/problems/set-mismatch/description/)

The set `S` originally contains numbers from 1 to `n`. But unfortunately, due to the data error, one of the numbers in the set got duplicated to another number in the set, which results in repetition of one number and loss of another number.

Given an array `nums` representing the data status of this set after the error. Your task is to firstly find the number occurs twice and then find the number that is missing. Return them in the form of an array.

**Example 1:**
```
Input: nums = [1,2,2,4]
Output: [2,3]
```

**Note:**
1. The given array size will in the range [2, 10000].
2. The given array's numbers won't have any order.

```python
# author：
```

```java
// author:
```

[451. Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency/description/)

Given a string, sort it in decreasing order based on the frequency of characters.

**Example 1:**
```
Input:
"tree"

Output:
"eert"

Explanation:
'e' appears twice while 'r' and 't' both appear once.
So 'e' must appear before both 'r' and 't'. Therefore "eetr" is also a valid answer.
```

**Example 2:**
```
Input:
"cccaaa"

Output:
"cccaaa"

Explanation:
Both 'c' and 'a' appear three times, so "aaaccc" is also a valid answer.
Note that "cacaca" is incorrect, as the same characters must be together.
```

**Example 3:**
```
Input:
"Aabb"

Output:
"bbAa"

Explanation:
"bbaA" is also a valid answer, but "Aabb" is incorrect.
Note that 'A' and 'a' are treated as two different characters.
```

**Note:**
1. The given array size will in the range [2, 10000].
2. The given array's numbers won't have any order.

```python
# author：
```

```java
// author:
```

[599. Minimum Index Sum of Two Lists](https://leetcode.com/problems/minimum-index-sum-of-two-lists/description/)

Suppose Andy and Doris want to choose a restaurant for dinner, and they both have a list of favorite restaurants represented by strings.

You need to help them find out their **common interest** with the **least list index sum**. If there is a choice tie between answers, output all of them with no order requirement. You could assume there always exists an answer.

**Example 1:**
```
Input:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["Piatti", "The Grill at Torrey Pines", "Hungry Hunter Steakhouse", "Shogun"]
Output: ["Shogun"]
Explanation: The only restaurant they both like is "Shogun".
```

**Example 2:**
```
Input:
["Shogun", "Tapioca Express", "Burger King", "KFC"]
["KFC", "Shogun", "Burger King"]
Output: ["Shogun"]
Explanation: The restaurant they both like and have the least index sum is "Shogun" with index sum 1 (0+1).
```


**Note:**
1. The length of both lists will be in the range of [1, 1000].
2. The length of strings in both lists will be in the range of [1, 30].
3. The index is starting from 0 to the list length minus 1.
4. No duplicates in both lists.

```python
# author：
```

```java
// author:KillersDeath
class Solution {
    public String[] findRestaurant(String[] list1, String[] list2) {
        Map<String, Integer> map = new HashMap<>();
        List<String> res = new LinkedList<>();

        int minSum = Integer.MAX_VALUE;
        for(int i=0;i<list1.length;i++) map.put(list1[i], i);
        for(int i=0;i<list2.length;i++){
            Integer j = map.get(list2[i]);
            if(j!=null && i+j<=minSum){
                if(i+j<minSum){
                    res.clear();
                    minSum = i+j;
                }
                res.add(list2[i]);
            }
        }
        return res.toArray(new String[res.size()]);
    }
}
```

[3. Longest Substring Without Repeating Characters](https://leetcode.com/problems/minimum-index-sum-of-two-lists/description/)

Given a string, find the length of the longest substring without repeating characters.

Examples:

Given `"abcabcbb"`, the answer is `"abc"`, which the length is 3.

Given `"bbbbb"`, the answer is `"b"`, with the length of 1.

Given `"pwwkew"`, the answer is `"wke"`, with the length of 3. Note that the answer must be a substring, `"pwke"` is a subsequence and not a substring.



```python
# author：
```

```java
// author:
```
