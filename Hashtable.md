### Hashtable
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
// author:Then
class Solution {
    public int findMaxLength(int[] nums) {
        int  []numsMap = new int[2*nums.length+1];
        int result = 0;
        int sum = nums.length;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i]==0 ? -1 : 1;
            if(sum == nums.length ){
                result = i+1;
                continue;
            }
            if(numsMap[sum]==0){
                numsMap[sum] = i+1;
            }else {
                result = Math.max(result, i-numsMap[sum]+1);
            }
        }
        return result;
    }
}
//author: KillersDeath
class Solution {
    public int findMaxLength(int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, -1);
        int count=0, maxlen=0;
        for(int i=0; i<nums.length;i++){
            count += nums[i]==1?1:-1;
            if(map.containsKey(count)){
                maxlen = Math.max(maxlen, i-map.get(count));
            }else{
                map.put(count, i);
            }
        }
        return maxlen;
    }
}
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
// author:Then
class Solution {
    public int[] findErrorNums(int[] nums) {
        int []result = new int[2];
        result[1] = (1+nums.length)*nums.length/2;
        int []map = new int[nums.length];
        for(int tmp:nums){
            if(map[tmp-1]==1){
                result[0] = tmp;
            }else{
                map[tmp-1]=1;
                result[1]-=tmp;
            }
        }
        return result;
    }
}
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
