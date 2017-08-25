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

[41. First Missing Positive](https://leetcode.com/problems/first-missing-positive/description/)

Given an unsorted integer array, find the first missing positive integer.

For example,
Given [1,2,0] return 3,
and [3,4,-1,1] return 2.

**Example 1:**
```
Given [1,2,0] return 3,
and [3,4,-1,1] return 2.
```

**Note:**

Your algorithm should run in O(n) time and uses constant space.

```Java
class Solution {
	// author: Then
    //整体思路:第一个缺失的正整数范围只能在1-nums.length+1，
    //因此只要标记1-nums.length这些数有没有出现过，就可以得到第一个miss的正整数
    // 这里使用nums[i]=i+1来标记i+1这个数字已经出现过
    public int firstMissingPositive(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            mark(nums,i);
        }
        //遍历数组找到第一个miss的正整数
        for (int i = 0; i < nums.length; i++) {
            if(nums[i]!=i+1){
                return i+1;
            }
        }
        //如果1-nums.length没有miss那肯定是nums.length+1这个数miss了
        return nums.length+1;
    }

    private void mark(int []nums, int i){
        //如果第i个元素不再范围内或者已经出现过，跳出递归
        if(nums[i]<=0 || nums[i]>nums.length || nums[i] == i+1){
            return;
        }
        int tmp = nums[i];
        //已经处理过的元素赋值为0，避免无线循环递归
        nums[i] = 0;
        mark(nums,tmp-1);
        //出现过的数字打上标记
        nums[tmp-1] = tmp;
    }
}
```

```python
// author: SweatSword
def firstMissingPositive(self, nums):
    """
    :type nums: List[int]
    :rtype: int
    """
    # idea: i should in nums[i]
    N=len(nums)
    nums=nums+[0]
    # 循环结束后 nums[i]=i ,for all i,expect missing positive
    for i in range(N+1):
        k = nums[i]
        while 0<= k <= N and k != nums[k]:
            nums[k],k=k,nums[k]
    # 第一个不等于0的位置
    for i in range(N+1):
        if nums[i] != i:
            return i
    return N+1
```

[57. Insert Interval](https://leetcode.com/problems/insert-interval/description/)

Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

**Example 1:**
```
Given intervals [1,3],[6,9], insert and merge [2,5] in as [1,5],[6,9].
```

**Example 2:**
```
Given [1,2],[3,5],[6,7],[8,10],[12,16], insert and merge [4,9] in as [1,2],[3,10],[12,16].
This is because the new interval [4,9] overlaps with [3,5],[6,7],[8,10].
```

```Java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
 //author:seasidesly
class Solution {
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        List<Interval> result = new LinkedList<>();
        int count = 0;
        //插入比start小的区间
        while ((count < intervals.size()) && (newInterval.start > intervals.get(count).end)) {
            result.add(intervals.get(count++));
        }

        //merge区间
        while ((count < intervals.size()) && (newInterval.end >= intervals.get(count).start)) {
            newInterval.start = Math.min(newInterval.start, intervals.get(count).start);
            newInterval.end = Math.max(newInterval.end, intervals.get(count).end);
            count ++;
        }
        result.add(newInterval);

        //后续区间
        while (count < intervals.size()) {
            result.add(intervals.get(count++));
        }
        return result;
    }
}
```

```java
class Solution {
    // author: Then
    //基本思路：遍历intervals，根据newInterval.start和end先后确定merge后的新区间
    //遍历的同时进行插入，在确定newInterval.start和end的过程中包含的区间不用再插入
    //如果newInterval.end在最后一个区间内，那么这个区间不用再插入，否则仍需要插入
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        List<Interval> resultList = new LinkedList<>();
        int size = intervals.size();
        int i = 0;
        //确认newInterval.start
        for (; i < size ;i++) {
            Interval interval = intervals.get(i);
            if(interval.end >= newInterval.start){
                if(interval.start <= newInterval.start){
                    newInterval.start = interval.start;
                }
                break;
            }
            resultList.add(interval);
        }

        //确认newInterval.end
        for (; i < size; i++) {
            Interval interval = intervals.get(i);
            if(interval.end >= newInterval.end){
                if(interval.start <= newInterval.end){
                    newInterval.end = interval.end;
                    i++;
                }
                break;
            }

        }

        //插入merge后的区间
        resultList.add(newInterval);

        //插入后续区间
        for (; i < size; i++) {
            resultList.add(intervals.get(i));
        }
        return resultList;
    }
}
```

[661. Image Smoother](https://leetcode.com/problems/image-smoother/description/)

Given a 2D integer matrix M representing the gray scale of an image, you need to design a smoother to make the gray scale of each cell becomes the average gray scale (rounding down) of all the 8 surrounding cells and itself. If a cell has less than 8 surrounding cells, then use as many as you can.  

**Example 1:**
```
Input:
[[1,1,1],
 [1,0,1],
 [1,1,1]]
Output:
[[0, 0, 0],
 [0, 0, 0],
 [0, 0, 0]]
Explanation:
For the point (0,0), (0,2), (2,0), (2,2): floor(3/4) = floor(0.75) = 0
For the point (0,1), (1,0), (1,2), (2,1): floor(5/6) = floor(0.83333333) = 0
For the point (1,1): floor(8/9) = floor(0.88888889) = 0
```
**Note:**
- The value in the given matrix is in the range of [0, 255].
- The length and width of the given matrix are in the range of [1, 150].

```java
class Solution {
    // author: Then
    public int[][] imageSmoother(int[][] M) {
        int xsize = M.length;
        int ysize = M[0].length;
        int result[][] = new int[xsize][ysize];
        for (int i = 0; i < xsize; i++) {
            for (int j = 0; j < ysize; j++) {
                int ii=i-1,jj=j-1,row=3,col=3;
                if( i == 0 ){
                    ii = i;
                    row--;
                }
                if( i == xsize-1 ){
                    row--;
                }
                if( j == 0){
                    jj = j;
                    col--;
                }
                if( j == ysize-1 ){
                    col--;
                }
                result[i][j] = avgCells(M,ii,jj,row,col);
            }
        }
        return result;
    }

    //计算下标为i，j的坐标为左上角cell开始，row行，col列cell组的平均值
    private  int avgCells(int[][] M, int i, int j,int row,int col){
        int tol = 0;
        for (int k = 0; k < row; k++) {
            for (int l = 0; l < col ; l++) {
                tol += M[i+k][j+l];
            }
        }
        return tol/(col*row);
    }
}
```

[495. Teemo Attacking](https://leetcode.com/problems/teemo-attacking/description/)

In LOL world, there is a hero called Teemo and his attacking can make his enemy Ashe be in poisoned condition. Now, given the Teemo's attacking ascending time series towards Ashe and the poisoning time duration per Teemo's attacking, you need to output the total time that Ashe is in poisoned condition.

You may assume that Teemo attacks at the very beginning of a specific time point, and makes Ashe be in poisoned condition immediately.   

**Example 1:**
```
Input: [1,4], 2
Output: 4
Explanation: At time point 1, Teemo starts attacking Ashe and makes Ashe be poisoned immediately.
This poisoned status will last 2 seconds until the end of time point 2.
And at time point 4, Teemo attacks Ashe again, and causes Ashe to be in poisoned status for another 2 seconds.
So you finally need to output 4.
```

**Example 2:**
```
Input: [1,2], 2
Output: 3
Explanation: At time point 1, Teemo starts attacking Ashe and makes Ashe be poisoned.
This poisoned status will last 2 seconds until the end of time point 2.
However, at the beginning of time point 2, Teemo attacks Ashe again who is already in poisoned status.
Since the poisoned status won't add up together, though the second poisoning attack will still work at time point 2, it will stop at the end of time point 3.
So you finally need to output 3.
```

**Note:**
- You may assume the length of given time series array won't exceed 10000.
- You may assume the numbers in the Teemo's attacking time series and his poisoning time duration per attacking are non-negative integers, which won't exceed 10,000,000.

```java
class Solution {
    // author: Then
    public int findPoisonedDuration(int[] timeSeries, int duration) {
        int result = 0;
        for (int i = 1; i < timeSeries.length; i++) {
            result += Math.min(duration,timeSeries[i]-timeSeries[i-1]);
        }
        if( timeSeries.length > 0){
            result += duration;
        }
        return result;
    }
}
```

[560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/description/)

Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to **k**.  

**Example 1:**
```
Input: nums = [1,1,1], k = 2
Output: 2
```

**Note:**
- The length of the array is in range [1, 20,000].
- The range of numbers in the array is [-1000, 1000] and the range of the integer k is [-1e7, 1e7].

```Java
public class Solution {
  // author: KillersDeath
    public int subarraySum(int[] nums, int k) {
        int count = 0;
        int sum = 0;
        HashMap < Integer, Integer > sum_map = new HashMap < > ();
        // 起始和为 0
        sum_map.put(0, 1);

        for (int i = 0; i < nums.length; i++) {
            // 当前和
            sum += nums[i];
            if (sum_map.containsKey(sum - k)){
                // 当前到i和为sum, 之前某个点j和为sum-k， 则[j, i]区间的和就为 k
                count += sum_map.get(sum - k);
            }
            // 和为sum的k自动加1
            sum_map.put(sum, sum_map.getOrDefault(sum, 0) + 1);
        }
        return count;
    }
}
```

[442. Find All Duplicates in an Array](https://leetcode.com/problems/find-all-duplicates-in-an-array/description/)
Given an array of integers, 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements that appear twice in this array.
Could you do it without extra space and in O(n) runtime?

**Example:**
```
Input:
[4,3,2,7,8,2,3,1]

Output:
[2,3]
```


```
class Solution(object):
    def findDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        # 每当i([1,N])出现1次,就在nums[i]加上N+1.最后只需要计算商为2的数即可
        N = len(nums)+1
        res = []
        for i in range(N-1):
            nums[nums[i] %N- 1] += N
        res=[i+1 for i in range(N-1) if nums[i]//N==2]
        return res
        
```



