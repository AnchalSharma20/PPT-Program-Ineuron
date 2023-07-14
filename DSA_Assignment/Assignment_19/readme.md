Q1.
```java
/*You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

*Merge all the linked-lists into one sorted linked-list and return it.
Input: lists = [[1,4,5],[1,3,4],[2,6]]
Output: [1,1,2,3,4,4,5,6]
Explanation: The linked-lists are:
[
  1->4->5,
  1->3->4,
  2->6
]
merging them into one sorted list:
1->1->2->3->4->4->5->6


**/

import java.util.PriorityQueue;

public class Question1 {
    public ListNode mergeKLists(ListNode[] lists) {
        // Create a priority queue to store the nodes of the linked lists
        PriorityQueue<ListNode> pq = new PriorityQueue<>((a, b) -> a.val - b.val);

        // Add the head nodes of all the linked lists to the priority queue
        for (ListNode head : lists) {
            if (head != null) {
                pq.offer(head);
            }
        }

        // Create a dummy node to build the merged list
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;

        // Process the nodes in the priority queue until it is empty
        while (!pq.isEmpty()) {
            // Remove the node with the smallest value from the priority queue
            ListNode node = pq.poll();
            current.next = node;
            current = current.next;

            // Add the next node from the same linked list to the priority queue
            if (node.next != null) {
                pq.offer(node.next);
            }
        }

        return dummy.next;
    }

    public static void main(String[] args) {
        // Create the example linked lists
        ListNode l1 = new ListNode(1);
        l1.next = new ListNode(4);
        l1.next.next = new ListNode(5);

        ListNode l2 = new ListNode(1);
        l2.next = new ListNode(3);
        l2.next.next = new ListNode(4);

        ListNode l3 = new ListNode(2);
        l3.next = new ListNode(6);

        // Create the array of linked lists
        ListNode[] lists = {l1, l2, l3};

        // Merge the linked lists
        Question1 merger = new Question1();
        ListNode mergedList = merger.mergeKLists(lists);

        // Print the merged list
        while (mergedList != null) {
            System.out.print(mergedList.val + " ");
            mergedList = mergedList.next;
        }
        System.out.println();
    }
}
```

Q2.
```java
/*

Given an integer array nums, return an integer array counts where counts[i] is the number of smaller elements to the right of nums[i].

Input: nums = [5,2,6,1]
Output: [2,1,1,0]
Explanation:
To the right of 5 there are2 smaller elements (2 and 1).
To the right of 2 there is only1 smaller element (1).
To the right of 6 there is1 smaller element (1).
To the right of 1 there is0 smaller element.




*/

import java.util.ArrayList;
import java.util.List;

public class Question2 {
    public List<Integer> countSmaller(int[] nums) {
        List<Integer> result = new ArrayList<>();
        int n = nums.length;

        // Create a sorted list to store the elements encountered so far
        List<Integer> sortedList = new ArrayList<>();

        // Traverse the array from right to left
        for (int i = n - 1; i >= 0; i--) {
            int num = nums[i];

            // Find the insertion position of the current element in the sorted list
            int insertionPos = findInsertionPosition(sortedList, num);

            // Add the insertion position to the result (number of smaller elements to the right)
            result.add(0, insertionPos);

            // Insert the current element at the correct position in the sorted list
            sortedList.add(insertionPos, num);
        }

        return result;
    }

    // Binary search to find the insertion position in the sorted list
    private int findInsertionPosition(List<Integer> sortedList, int target) {
        int left = 0;
        int right = sortedList.size();

        while (left < right) {
            int mid = left + (right - left) / 2;
            int midNum = sortedList.get(mid);

            if (midNum < target) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }

        return left;
    }

    public static void main(String[] args) {
        int[] nums = {5, 2, 6, 1};
        Question2 counter = new Question2();
        List<Integer> result = counter.countSmaller(nums);
        System.out.println(result);
    }
}
```

Q3.
```java
/*

Given an array of integers `nums`, sort the array in ascending order and return it.

You must solve the problem **without using any built-in** functions in `O(nlog(n))` time complexity and with the smallest space complexity possible.

Input: nums = [5,2,3,1]
Output: [1,2,3,5]
Explanation: After sorting the array, the positions of some numbers are not changed (for example, 2 and 3), while the positions of other numbers are changed (for example, 1 and 5).





*/

public class Question3 {
    public void sortArray(int[] nums) {
        int n = nums.length;
        int[] temp = new int[n];
        mergeSort(nums, temp, 0, n - 1);
    }

    private void mergeSort(int[] nums, int[] temp, int left, int right) {
        if (left >= right) {
            return;
        }

        int mid = left + (right - left) / 2;

        mergeSort(nums, temp, left, mid);
        mergeSort(nums, temp, mid + 1, right);

        merge(nums, temp, left, mid, right);
    }

    private void merge(int[] nums, int[] temp, int left, int mid, int right) {
        for (int i = left; i <= right; i++) {
            temp[i] = nums[i];
        }

        int i = left;
        int j = mid + 1;
        int k = left;

        while (i <= mid && j <= right) {
            if (temp[i] <= temp[j]) {
                nums[k] = temp[i];
                i++;
            } else {
                nums[k] = temp[j];
                j++;
            }
            k++;
        }

        while (i <= mid) {
            nums[k] = temp[i];
            i++;
            k++;
        }
    }

    public static void main(String[] args) {
        int[] nums = {5, 2, 3, 1};
        Question3 sorter = new Question3();
        sorter.sortArray(nums);

        for (int num : nums) {
            System.out.print(num + " ");
        }
    }
}
```

Q4.
```java
/*

Given an array of random numbers, Push all the zero’s of a given array to the end of the array. For example, if the given arrays is {1, 9, 8, 4, 0, 0, 2, 7, 0, 6, 0}, it should be changed to {1, 9, 8, 4, 2, 7, 6, 0, 0, 0, 0}. The order of all other elements should be same. Expected time complexity is O(n) and extra space is O(1).

Input :  arr[] = {1, 2, 0, 4, 3, 0, 5, 0};
Output : arr[] = {1, 2, 4, 3, 5, 0, 0, 0};

Input : arr[]  = {1, 2, 0, 0, 0, 3, 6};
Output : arr[] = {1, 2, 3, 6, 0, 0, 0};


*/

public class Question4 {
    public static void pushZeros(int[] arr) {
        int n = arr.length;
        int left = 0; // Pointer for non-zero elements

        // Traverse the array
        for (int i = 0; i < n; i++) {
            // If the current element is non-zero, swap it with the left pointer element
            if (arr[i] != 0) {
                int temp = arr[i];
                arr[i] = arr[left];
                arr[left] = temp;
                left++;
            }
        }
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 0, 4, 3, 0, 5, 0};
        pushZeros(arr);

        // Print the modified array
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}
```

Q5.
```java
/*

Given an array of positive and negative numbers, arrange them in an alternate fashion such that every positive number is followed by a negative and vice-versa maintaining the order of appearance. The number of positive and negative numbers need not be equal. If there are more positive numbers they appear at the end of the array. If there are more negative numbers, they too appear at the end of the array.

Input:  arr[] = {1, 2, 3, -4, -1, 4}
Output: arr[] = {-4, 1, -1, 2, 3, 4}

Input:  arr[] = {-5, -2, 5, 2, 4, 7, 1, 8, 0, -8}
Output: arr[] = {-5, 5, -2, 2, -8, 4, 7, 1, 8, 0}

*/

public class Question5 {
    public static void alternateArrange(int[] arr) {
        int n = arr.length;
        int positive = 0; // Pointer for positive numbers

        // Find the index of the first negative number
        while (positive < n && arr[positive] >= 0) {
            positive++;
        }

        // Rearrange the array in an alternate fashion
        int negative = 1; // Pointer for negative numbers

        while (positive < n && negative < n) {
            // Swap the positive and negative numbers
            int temp = arr[positive];
            arr[positive] = arr[negative];
            arr[negative] = temp;

            positive += 2;
            negative += 2;

            // Find the next positive number
            while (positive < n && arr[positive] >= 0) {
                positive += 2;
            }

            // Find the next negative number
            while (negative < n && arr[negative] < 0) {
                negative += 2;
            }
        }
    }

    public static void main(String[] args) {
        int[] arr = {1, 2, 3, -4, -1, 4};
        alternateArrange(arr);

        // Print the modified array
        for (int num : arr) {
            System.out.print(num + " ");
        }
    }
}
```

Q6.
```java
/*

Given two sorted arrays, the task is to merge them in a sorted manner.

Input: arr1[] = { 1, 3, 4, 5}, arr2[] = {2, 4, 6, 8} 
Output: arr3[] = {1, 2, 3, 4, 4, 5, 6, 8}

Input: arr1[] = { 5, 8, 9}, arr2[] = {4, 7, 8}
Output: arr3[] = {4, 5, 7, 8, 8, 9}



*/

public class Question6 {
    public static int[] mergeArrays(int[] arr1, int[] arr2) {
        int n1 = arr1.length;
        int n2 = arr2.length;
        int[] merged = new int[n1 + n2];

        int i = 0; // Pointer for arr1
        int j = 0; // Pointer for arr2
        int k = 0; // Pointer for merged array

        // Compare elements from arr1 and arr2 and add the smaller element to the merged array
        while (i < n1 && j < n2) {
            if (arr1[i] <= arr2[j]) {
                merged[k++] = arr1[i++];
            } else {
                merged[k++] = arr2[j++];
            }
        }

        // Add remaining elements from arr1, if any
        while (i < n1) {
            merged[k++] = arr1[i++];
        }

        // Add remaining elements from arr2, if any
        while (j < n2) {
            merged[k++] = arr2[j++];
        }

        return merged;
    }

    public static void main(String[] args) {
        int[] arr1 = {1, 3, 4, 5};
        int[] arr2 = {2, 4, 6, 8};
        int[] merged = mergeArrays(arr1, arr2);

        // Print the merged array
        for (int num : merged) {
            System.out.print(num + " ");
        }
    }
}
```

Q7.
```java
/*

Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must be unique and you may return the result in any order.

Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]





*/

import java.util.*;

public class Question7 {
    public static int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet<>();
        Set<Integer> intersect = new HashSet<>();

        // Add elements of nums1 to the set
        for (int num : nums1) {
            set.add(num);
        }

        // Check if each element in nums2 exists in the set
        for (int num : nums2) {
            if (set.contains(num)) {
                intersect.add(num);
            }
        }

        // Convert the set to an array
        int[] result = new int[intersect.size()];
        int i = 0;
        for (int num : intersect) {
            result[i++] = num;
        }

        return result;
    }

    public static void main(String[] args) {
        int[] nums1 = {1, 2, 2, 1};
        int[] nums2 = {2, 2};
        int[] intersection = intersection(nums1, nums2);

        // Print the intersection array
        for (int num : intersection) {
            System.out.print(num + " ");
        }
    }
}
```

Q8.
```java
/*

Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must appear as many times as it shows in both arrays and you may return the result in any order.

Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]




*/
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Question8 {
    public static int[] intersect(int[] nums1, int[] nums2) {
        Map<Integer, Integer> frequencyMap = new HashMap<>();
        List<Integer> intersection = new ArrayList<>();

        // Build frequency map for nums1
        for (int num : nums1) {
            frequencyMap.put(num, frequencyMap.getOrDefault(num, 0) + 1);
        }

        // Check frequency and build intersection list for nums2
        for (int num : nums2) {
            if (frequencyMap.containsKey(num) && frequencyMap.get(num) > 0) {
                intersection.add(num);
                frequencyMap.put(num, frequencyMap.get(num) - 1);
            }
        }

        // Convert the intersection list to an array
        int[] result = new int[intersection.size()];
        int i = 0;
        for (int num : intersection) {
            result[i++] = num;
        }

        return result;
    }

    public static void main(String[] args) {
        int[] nums1 = {1, 2, 2, 1};
        int[] nums2 = {2, 2};
        int[] intersection = intersect(nums1, nums2);

        // Print the intersection array
        for (int num : intersection) {
            System.out.print(num + " ");
        }
    }
}
```








