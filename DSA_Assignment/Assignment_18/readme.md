Q1.
```java
/*
 Given an array of intervals where intervals[i] = [starti, endi], merge all overlapping intervals, and return an array of the non-overlapping intervals that cover all the intervals in the input.
 Input: intervals = [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlap, merge them into [1,6].

 */

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Comparator;
import java.util.List;

public class Question1 {
    public int[][] mergeIntervals(int[][] intervals) {
        Arrays.sort(intervals, Comparator.comparingInt(a -> a[0]));
        
        List<int[]> merged = new ArrayList<>();
        int[] currentInterval = intervals[0];
        merged.add(currentInterval);
        
        for (int[] interval : intervals) {
            int currentEnd = currentInterval[1];
            int nextStart = interval[0];
            int nextEnd = interval[1];
            
            if (currentEnd >= nextStart) {
                currentInterval[1] = Math.max(currentEnd, nextEnd);
            } else {
                currentInterval = interval;
                merged.add(currentInterval);
            }
        }
        
        return merged.toArray(new int[merged.size()][]);
    }
    
    public static void main(String[] args) {
        int[][] intervals = {{1, 3}, {2, 6}, {8, 10}, {15, 18}};
        
        Question1 merger = new Question1();
        int[][] mergedIntervals = merger.mergeIntervals(intervals);
        
        for (int[] interval : mergedIntervals) {
            System.out.println(Arrays.toString(interval));
        }
    }
}
```

Q2.
```java
import java.util.HashSet;

/*

Given an array `nums` with `n` objects colored red, white, or blue, sort them **[in-place](https://en.wikipedia.org/wiki/In-place_algorithm)** so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

We will use the integers `0`, `1`, and `2` to represent the color red, white, and blue, respectively.

You must solve this problem without using the library's sort function.


Input: nums = [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]



*/

public class Question2 {
    public void sortColors(int[] nums) {
        int n = nums.length;
        int low = 0;
        int mid = 0;
        int high = n - 1;
        
        while (mid <= high) {
            if (nums[mid] == 0) {
                swap(nums, low, mid);
                low++;
                mid++;
            } else if (nums[mid] == 1) {
                mid++;
            } else if (nums[mid] == 2) {
                swap(nums, mid, high);
                high--;
            }
        }
    }
    
    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    
    public static void main(String[] args) {
        int[] nums = {2, 0, 2, 1, 1, 0};
        
        Question2 sorter = new Question2();
        sorter.sortColors(nums);
        
        for (int num : nums) {
            System.out.print(num + " ");
        }
    }
}
```

Q3.
```java
/*


First Bad Version Solution

You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have `n` versions `[1, 2, ..., n]` and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API `bool isBadVersion(version)` which returns whether `version` is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.


Input: n = 5, bad = 4
Output: 4
Explanation:
call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true
Then 4 is the first bad version.





*/

public class Question3 {
    public boolean isBadVersion(int version) {
        // Implementation of the isBadVersion API is not provided
        return false; // Placeholder return statement
    }

    public int firstBadVersion(int n) {
        int left = 1;
        int right = n;

        while (left < right) {
            int mid = left + (right - left) / 2;

            if (isBadVersion(mid)) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return left;
    }

    public static void main(String[] args) {
        int n = 5;
        int bad = 4;

        Question3 versionControl = new Question3();
        int firstBadVersion = versionControl.firstBadVersion(n);

        System.out.println("The first bad version is: " + firstBadVersion);
    }
}
```

Q4.
```java
/*

Given an integer array `nums`, return *the maximum difference between two successive elements in its sorted form*. If the array contains less than two elements, return `0`.

You must write an algorithm that runs in linear time and uses linear extra space.

Input: nums = [3,6,9,1]
Output: 3
Explanation: The sorted form of the array is [1,3,6,9], either (3,6) or (6,9) has the maximum difference 3.



*/

import java.util.Arrays;

public class Question4 {
    public int maximumGap(int[] nums) {
        int n = nums.length;
        
        if (n < 2) {
            return 0;
        }
        
        // Find the maximum and minimum values in the array
        int maxVal = Arrays.stream(nums).max().getAsInt();
        int minVal = Arrays.stream(nums).min().getAsInt();
        
        // Calculate the bucket size and number of buckets
        int bucketSize = Math.max(1, (maxVal - minVal) / (n - 1));
        int numBuckets = (maxVal - minVal) / bucketSize + 1;
        
        // Initialize the buckets
        int[][] buckets = new int[numBuckets][2];
        for (int i = 0; i < numBuckets; i++) {
            Arrays.fill(buckets[i], -1);
        }
        
        // Populate the buckets with values
        for (int num : nums) {
            int bucketIndex = (num - minVal) / bucketSize;
            
            if (buckets[bucketIndex][0] == -1) {
                buckets[bucketIndex][0] = num;
                buckets[bucketIndex][1] = num;
            } else {
                buckets[bucketIndex][0] = Math.min(buckets[bucketIndex][0], num);
                buckets[bucketIndex][1] = Math.max(buckets[bucketIndex][1], num);
            }
        }
        
        // Calculate the maximum gap
        int maxGap = 0;
        int prevMax = minVal;
        
        for (int[] bucket : buckets) {
            if (bucket[0] == -1) {
                continue;
            }
            
            maxGap = Math.max(maxGap, bucket[0] - prevMax);
            prevMax = bucket[1];
        }
        
        return maxGap;
    }

    public static void main(String[] args) {
        int[] nums = {3, 6, 9, 1};

        Question4 maximumGap = new Question4();
        int maxDifference = maximumGap.maximumGap(nums);

        System.out.println("The maximum difference is: " + maxDifference);
    }
}
```

Q5.
```java
/*

Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and return `false` if every element is distinct.

Input: nums = [1,2,3,1]
Output: true



*/

import java.util.HashSet;

public class Question5 {
    public boolean containsDuplicate(int[] nums) {
        HashSet<Integer> set = new HashSet<>();
        
        for (int num : nums) {
            if (set.contains(num)) {
                return true;
            }
            set.add(num);
        }
        
        return false;
    }

    public static void main(String[] args) {
        int[] nums = {1, 2, 3, 1};

        Question5 containsDuplicate = new Question5();
        boolean result = containsDuplicate.containsDuplicate(nums);

        System.out.println("Contains duplicate elements: " + result);
    }
}
```

Q6.
```java
/*

There are some spherical balloons taped onto a flat wall that represents the XY-plane. The balloons are represented as a 2D integer array `points` where `points[i] = [xstart, xend]` denotes a balloon whose **horizontal diameter** stretches between `xstart` and `xend`. You do not know the exact y-coordinates of the balloons.

Arrows can be shot up **directly vertically** (in the positive y-direction) from different points along the x-axis. A balloon with `xstart` and `xend` is **burst** by an arrow shot at `x` if `xstart <= x <= xend`. There is **no limit** to the number of arrows that can be shot. A shot arrow keeps traveling up infinitely, bursting any balloons in its path.

Given the array `points`, return *the **minimum** number of arrows that must be shot to burst all balloons*.

Input: points = [[10,16],[2,8],[1,6],[7,12]]
Output: 2
Explanation: The balloons can be burst by 2 arrows:
- Shoot an arrow at x = 6, bursting the balloons [2,8] and [1,6].
- Shoot an arrow at x = 11, bursting the balloons [10,16] and [7,12].




*/

import java.util.Arrays;

public class Question6 {
    public int findMinArrowShots(int[][] points) {
        if (points == null || points.length == 0) {
            return 0;
        }

        // Sort the balloons based on their end position
        Arrays.sort(points, (a, b) -> Integer.compare(a[1], b[1]));

        int arrows = 1; // At least one arrow is needed
        int currentEnd = points[0][1]; // Initial end position

        for (int i = 1; i < points.length; i++) {
            // If the start position is greater than the current end position,
            // we need to shoot a new arrow
            if (points[i][0] > currentEnd) {
                arrows++;
                currentEnd = points[i][1]; // Update the current end position
            }
        }

        return arrows;
    }

    public static void main(String[] args) {
        int[][] points = {{10, 16}, {2, 8}, {1, 6}, {7, 12}};

        Question6 solution = new Question6();
        int minArrows = solution.findMinArrowShots(points);

        System.out.println("Minimum number of arrows needed: " + minArrows);
    }
}
```

Q7.
```java
/*

Given an integer array nums, return the length of the longest strictly increasing

Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.




*/

public class Question7 {
    public int lengthOfLIS(int[] nums) {
        int n = nums.length;
        int[] dp = new int[n];
        Arrays.fill(dp, 1);
        
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
        }
        
        int maxLen = 0;
        for (int len : dp) {
            maxLen = Math.max(maxLen, len);
        }
        
        return maxLen;
    }
    public static void main(String[] args) {
    	int[] nums = {10, 9, 2, 5, 3, 7, 101, 18};
    	Question7 lis = new Question7();
    	int maxLength = lis.lengthOfLIS(nums);
    	System.out.println("Length of the longest increasing subsequence: " + maxLength);

	}
}
```

Q8.
```java
/*



Given an array of `n` integers `nums`, a **132 pattern** is a subsequence of three integers `nums[i]`, `nums[j]` and `nums[k]` such that `i < j < k` and `nums[i] < nums[k] < nums[j]`.

Return `true` *if there is a **132 pattern** in* `nums`*, otherwise, return* `false`*.*



Input: nums = [1,2,3,4]
Output: false
Explanation: There is no 132 pattern in the sequence.




*/


public class Question8 {
    public boolean find132pattern(int[] nums) {
        int n = nums.length;
        int[] minArray = new int[n];
        Stack<Integer> stack = new Stack<>();
        
        // Find the minimum element so far for each index
        minArray[0] = nums[0];
        for (int i = 1; i < n; i++) {
            minArray[i] = Math.min(minArray[i - 1], nums[i]);
        }
        
        // Check for the 132 pattern
        for (int j = n - 1; j >= 0; j--) {
            if (nums[j] > minArray[j]) {
                while (!stack.isEmpty() && stack.peek() <= minArray[j]) {
                    stack.pop();
                }
                if (!stack.isEmpty() && stack.peek() < nums[j]) {
                    return true;
                }
                stack.push(nums[j]);
            }
        }
        
        return false;
    }
    public static void main(String[] args) {
    	int[] nums = {3,1,4,2};
    	Question8 pattern132 = new Question8();
    	boolean hasPattern = pattern132.find132pattern(nums);
    	System.out.println("Has 132 pattern: " + hasPattern);

	}
}

```







