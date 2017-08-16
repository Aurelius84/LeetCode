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
