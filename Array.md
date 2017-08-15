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
