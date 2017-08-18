### Array
[643. Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i/description/)

Given an array consisting of n integers, find the contiguous subarray of given length k that has the maximum average value. And you need to output the maximum average value.

**Example 1:**
```
Input: [1,12,-5,-6,50,3], k = 4
Output: 12.75
Explanation: Maximum average is (12-5-6+50)/4 = 51/4 = 12.75
```

**Note:**

1. <= `k` <= `n` <= 30,000.
2. Elements of the given array will be in the range [-10,000, 10,000].

```Java
// author: Then
public class solution{
  public double findMaxAverage(int[] nums, int k){
    double max = 0;
    double presentTal = 0;
    for(int i = 0; i < k; i++){
      max += nums[i];
    }
    presentTal = max;
    for(int i = k; i < nums.length; i++){
      presentTal += nums[i];
      presentTal -= nums[i-k];
      if(presentTal > max){
        max = presentTal;
      }
    }
    return max/k;
  }
}
```

[611. Valid Triangle Number I](https://leetcode.com/problems/valid-triangle-number/description/)

Given an array consists of non-negative integers, your task is to count the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.

**Example 1:**
```
Input: [2,2,3,4]
Output: 3
Explanation:
Valid combinations are:
2,3,4 (using the first 2)
2,3,4 (using the second 2)
2,2,3
```

**Note:**

1. The `length` of the given array won't exceed `1000`.
2. The integers in the given array are in the range of [0, 1000].

```Java
// author: KillersDeath
public class Solution {
    public int triangleNumber(int[] nums) {
        if (nums.length <= 2) return 0;
        Arrays.sort(nums);
        int n = nums.length;
        int cnt = 0;
        // 因为 nums[i] + nums[j] 是递增的
        // 所以在i=0找到的边，可以直接加到i=1的边上
        for(int i = 0; i < n; ++i){
            int pos = i + 2;
            for(int j = i + 1; j < n - 1 && nums[i] != 0; ++j){
                // 循环内共享上次查找的pos位置
                int sum = nums[i] + nums[j];
                while (pos < n && sum > nums[pos]) pos ++;
                cnt += pos - j - 1;
            }
        }
        return cnt;
    }
}
```

[605. Can Place Flowers ](https://leetcode.com/problems/valid-triangle-number/description/)

Suppose you have a long flowerbed in which some of the plots are planted and some are not. However, flowers cannot be planted in adjacent plots - they would compete for water and both would die.

Given a flowerbed (represented as an array containing 0 and 1, where 0 means empty and 1 means not empty), and a number **n**, return if **n** new flowers can be planted in it without violating the no-adjacent-flowers rule.

**Example 1:**
```
Input: flowerbed = [1,0,0,0,1], n = 1
Output: True
```

**Example 2:**
```
Input: flowerbed = [1,0,0,0,1], n = 2
Output: False
```

**Note:**

1. The input array won't violate no-adjacent-flowers rule.
2. The input array size is in the range of [1, 20000].
3. **n** is a non-negative integer which won't exceed the input array size.

```Python
// author: SweatSword
class Solution:
    def canPlaceFlowers(self, flowerbed, n):
        """
        :type flowerbed: List[int]
        :type n: int
        :rtype: bool
        """
        flowerbed = [1,0] + flowerbed + [0,1]
        width = cnt = 0
        for num in flowerbed:
            if num == 1:
                cnt += int((width - 1)/2)
                width = 0
            else:
                width += 1
        return cnt >= n
```

```Java
public class Solution {
    //author : Then
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int left=-2;
        for (int i = 0; i < flowerbed.length; i++) {
            if(flowerbed[i] == 1){
                int emptyPlotNum = i-left-1;
                if(emptyPlotNum>=3){
                    n -= (emptyPlotNum-1)>>1;
                }
                left = i;
            }
        }
        int emptyPlotNum = flowerbed.length-left;
        if(emptyPlotNum>=3){
            n -= (emptyPlotNum-1)>>1;
        }
        return n>0?false:true;
    }
}
```

[565. Array Nesting ](https://leetcode.com/problems/array-nesting/description/)

A zero-indexed array A consisting of N different integers is given. The array contains all integers in the range [0, N - 1].

Sets S[K] for 0 <= K < N are defined as follows:

S[K] = { A[K], A[A[K]], A[A[A[K]]], ... }.

Sets S[K] are finite for each K and should NOT contain duplicates.

Write a function that given an array A consisting of N integers, return the size of the largest set S[K] for this array.

**Example 1:**
```
Input: A = [5,4,0,3,1,6,2]
Output: 4
Explanation:
A[0] = 5, A[1] = 4, A[2] = 0, A[3] = 3, A[4] = 1, A[5] = 6, A[6] = 2.

One of the longest S[K]:
S[0] = {A[0], A[5], A[6], A[2]} = {5, 6, 2, 0}
```

**Note:**

1. `N` is an integer within the range [1, 20,000].
2. The elements of `A` are all distinct.
3. Each element of array `A` is an integer within the range [0, N-1].

```Java
class Solution {
    // author: Then
    public int arrayNesting(int[] nums) {
        int max = 0;
        for(int i = 0; i < nums.length;i++){
            if(nums[i] != -1){
                int k = i;
                int count = 1;
                while(nums[k] != i){
                    int temp = nums[k];
                    nums[k] = -1;
                    k = temp;
                    count ++;
                }
                nums[k] = -1;
                nums[i] = -1;
                if(count > max){
                    max = count;
                }
            }
        }
        return max;

    }
}
```
