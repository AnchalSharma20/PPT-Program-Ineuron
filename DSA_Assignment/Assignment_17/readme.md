Q1.
```java
/*
Given a string s, find the first non-repeating character in it and return its index. If it does not exist, return -1.
Input: s = "leetcode"
Output: 0

*/

public class Question01 {
    public static int firstUniqChar(String s) {
        // Create an array to store the count of each character
        int[] count = new int[26];

        // Iterate through the string and count the occurrence of each character
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            count[c - 'a']++;
        }

        // Iterate through the string again to find the first non-repeating character
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (count[c - 'a'] == 1) {
                return i;
            }
        }

        // No non-repeating character found
        return -1;
    }

    public static void main(String[] args) {
        String s = "loveleetcode";
        int index = firstUniqChar(s);
        System.out.println("Index of the first non-repeating character: " + index);
    }
}
```

Q2.
```java
/*
Given a **circular integer array** `nums` of length `n`, return *the maximum possible sum of a non-empty **subarray** of* `nums`.

A **circular array** means the end of the array connects to the beginning of the array. Formally, the next element of `nums[i]` is `nums[(i + 1) % n]` and the previous element of `nums[i]` is `nums[(i - 1 + n) % n]`.

A **subarray** may only include each element of the fixed buffer `nums` at most once. Formally, for a subarray `nums[i], nums[i + 1], ..., nums[j]`, there does not exist `i <= k1`, `k2 <= j` with `k1 % n == k2 % n`. 

Input: nums = [1,-2,3,-2]
Output: 3
Explanation: Subarray [3] has maximum sum 3.

*/

public class Question2 {
    public static int maxSubarraySum(int[] nums) {
        int maxSum = nums[0];
        int currentMax = nums[0];
        int n = nums.length;

        // Find the maximum subarray sum without circular wrapping
        for (int i = 1; i < n; i++) {
            currentMax = Math.max(nums[i], currentMax + nums[i]);
            maxSum = Math.max(maxSum, currentMax);
        }

        int totalSum = 0;
        int minSum = nums[0];
        int currentMin = nums[0];

        // Find the total sum and the minimum subarray sum with circular wrapping
        for (int i = 0; i < n; i++) {
            totalSum += nums[i];
            currentMin = Math.min(nums[i], currentMin + nums[i]);
            minSum = Math.min(minSum, currentMin);
        }

        // If the total sum is equal to the minimum subarray sum (all negative elements), return the maximum subarray sum without circular wrapping
        if (totalSum == minSum) {
            return maxSum;
        }

        // Otherwise, return the maximum of the maximum subarray sum without circular wrapping and the (total sum - minimum subarray sum) with circular wrapping
        return Math.max(maxSum, totalSum - minSum);
    }

    public static void main(String[] args) {
        int[] nums = {5,-3,5};
        int maxSum = maxSubarraySum(nums);
        System.out.println("Maximum circular subarray sum: " + maxSum);
    }
}


```

Q3.
```java
/*

The school cafeteria offers circular and square sandwiches at lunch break, referred to by numbers `0` and `1` respectively. All students stand in a queue. Each student either prefers square or circular sandwiches.

The number of sandwiches in the cafeteria is equal to the number of students. The sandwiches are placed in a **stack**. At each step:

- If the student at the front of the queue **prefers** the sandwich on the top of the stack, they will **take it** and leave the queue.
- Otherwise, they will **leave it** and go to the queue's end.

This continues until none of the queue students want to take the top sandwich and are thus unable to eat.

You are given two integer arrays `students` and `sandwiches` where `sandwiches[i]` is the type of the `ith` sandwich in the stack (`i = 0` is the top of the stack) and `students[j]` is the preference of the `jth` student in the initial queue (`j = 0` is the front of the queue). Return *the number of students that are unable to eat*

Input: students = [1,1,0,0], sandwiches = [0,1,0,1]
Output: 0
*/

import java.util.*;

public class Question3 {
    public static int countStudents(int[] students, int[] sandwiches) {
        Queue<Integer> queue = new LinkedList<>();

        // Add all students to the queue
        for (int student : students) {
            queue.offer(student);
        }

        int notEaten = 0; // Count of students who are unable to eat

        for (int sandwich : sandwiches) {
            if (queue.isEmpty()) {
                break;
            }

            if (queue.peek() == sandwich) {
                queue.poll(); // The student takes the sandwich
                notEaten = 0; // Reset the count
            } else {
                queue.offer(queue.poll()); // The student goes to the queue's end
                notEaten++; // Increment the count of students unable to eat

                // If all students have been considered but no one can eat, break the loop
                if (notEaten == queue.size()) {
                    break;
                }
            }
        }

        return queue.size(); // Remaining students in the queue are unable to eat
    }

    public static void main(String[] args) {
        int[] students = {1,1,1,0,0,1};
        int[] sandwiches = {1,0,0,0,1,1};
        int notEaten = countStudents(students, sandwiches);
        System.out.println("Number of students unable to eat: " + notEaten);
    }
}
```

Q4.
```java
/*
You have a `RecentCounter` class which counts the number of recent requests within a certain time frame.

Implement the `RecentCounter` class:

- `RecentCounter()` Initializes the counter with zero recent requests.
- `int ping(int t)` Adds a new request at time `t`, where `t` represents some time in milliseconds, and returns the number of requests that has happened in the past `3000` milliseconds (including the new request). Specifically, return the number of requests that have happened in the inclusive range `[t - 3000, t]`.

It is **guaranteed** that every call to `ping` uses a strictly larger value of `t` than the previous call.

Input
["RecentCounter", "ping", "ping", "ping", "ping"]
[[], [1], [100], [3001], [3002]]
Output
[null, 1, 2, 3, 3]
*/



import java.util.LinkedList;
import java.util.Queue;

public class Question4 {
    private Queue<Integer> requests;

    public Question4() {
        requests = new LinkedList<>();
    }

    public int ping(int t) {
        // Add the current request time to the queue
        requests.offer(t);

        // Remove outdated requests from the queue
        while (!requests.isEmpty() && requests.peek() < t - 3000) {
            requests.poll();
        }

        // Return the number of requests within the time frame
        return requests.size();
    }

    public static void main(String[] args) {
        Question4 counter = new Question4();
        System.out.println(counter.ping(1));     // Output: 1
        System.out.println(counter.ping(100));   // Output: 2
        System.out.println(counter.ping(3001));  // Output: 3
        System.out.println(counter.ping(3002));  // Output: 3
    }
}
```

Q5.
```java
/*

There are `n` friends that are playing a game. The friends are sitting in a circle and are numbered from `1` to `n` in **clockwise order**. More formally, moving clockwise from the `ith` friend brings you to the `(i+1)th` friend for `1 <= i < n`, and moving clockwise from the `nth` friend brings you to the `1st` friend.

The rules of the game are as follows:

1. **Start** at the `1st` friend.
2. Count the next `k` friends in the clockwise direction **including** the friend you started at. The counting wraps around the circle and may count some friends more than once.
3. The last friend you counted leaves the circle and loses the game.
4. If there is still more than one friend in the circle, go back to step `2` **starting** from the friend **immediately clockwise** of the friend who just lost and repeat.
5. Else, the last friend in the circle wins the game.

Given the number of friends, `n`, and an integer `k`, return *the winner of the game*.

Input: n = 5, k = 2
Output: 3
Explanation: Here are the steps of the game:
1) Start at friend 1.
2) Count 2 friends clockwise, which are friends 1 and 2.
3) Friend 2 leaves the circle. Next start is friend 3.
4) Count 2 friends clockwise, which are friends 3 and 4.
5) Friend 4 leaves the circle. Next start is friend 5.
6) Count 2 friends clockwise, which are friends 5 and 1.
7) Friend 1 leaves the circle. Next start is friend 3.
8) Count 2 friends clockwise, which are friends 3 and 5.
9) Friend 5 leaves the circle. Only friend 3 is left, so they are the winner

*/

public class Question5 {
    static class ListNode {
        int val;
        ListNode next;

        ListNode(int val) {
            this.val = val;
        }
    }

    public static int findTheWinner(int n, int k) {
        ListNode head = buildCircularLinkedList(n);

        // Start at friend 1
        ListNode current = head;
        ListNode prev = null;

        while (current.next != current) {
            // Count k-1 friends
            for (int i = 0; i < k - 1; i++) {
                prev = current;
                current = current.next;
            }

            // Remove the friend
            prev.next = current.next;
            current = prev.next;
        }

        // The last friend remaining is the winner
        return current.val;
    }

    private static ListNode buildCircularLinkedList(int n) {
        ListNode head = new ListNode(1);
        ListNode current = head;

        for (int i = 2; i <= n; i++) {
            current.next = new ListNode(i);
            current = current.next;
        }

        current.next = head; // Make the linked list circular

        return head;
    }

    public static void main(String[] args) {
        int n = 6;
        int k = 5;
        int winner = findTheWinner(n, k);
        System.out.println("The winner of the game: " + winner);
    }
}
```

Q6.
```java
/*

You are given an integer array `deck`. There is a deck of cards where every card has a unique integer. The integer on the `ith` card is `deck[i]`.

You can order the deck in any order you want. Initially, all the cards start face down (unrevealed) in one deck.

You will do the following steps repeatedly until all cards are revealed:

1. Take the top card of the deck, reveal it, and take it out of the deck.
2. If there are still cards in the deck then put the next top card of the deck at the bottom of the deck.
3. If there are still unrevealed cards, go back to step 1. Otherwise, stop.

Return *an ordering of the deck that would reveal the cards in increasing order*.

**Note** that the first entry in the answer is considered to be the top of the deck.

Input: deck = [17,13,11,2,3,5,7]
Output: [2,13,3,11,5,17,7]
Explanation:
We get the deck in the order [17,13,11,2,3,5,7] (this order does not matter), and reorder it.
After reordering, the deck starts as [2,13,3,11,5,17,7], where 2 is the top of the deck.
We reveal 2, and move 13 to the bottom.  The deck is now [3,11,5,17,7,13].
We reveal 3, and move 11 to the bottom.  The deck is now [5,17,7,13,11].
We reveal 5, and move 17 to the bottom.  The deck is now [7,13,11,17].
We reveal 7, and move 13 to the bottom.  The deck is now [11,17,13].
We reveal 11, and move 17 to the bottom.  The deck is now [13,17].
We reveal 13, and move 17 to the bottom.  The deck is now [17].
We reveal 17.
Since all the cards revealed are in increasing order, the answer is correct.

*/

import java.util.Arrays;
import java.util.LinkedList;

public class Question6 {
    public static int[] deckRevealedIncreasing(int[] deck) {
        int n = deck.length;
        Arrays.sort(deck);

        LinkedList<Integer> revealed = new LinkedList<>();
        for (int i = n - 1; i >= 0; i--) {
            if (i == n - 1) {
                revealed.addFirst(deck[i]);
            } else {
                revealed.addFirst(revealed.removeLast());
                revealed.addFirst(deck[i]);
            }
        }

        int[] result = new int[n];
        for (int i = 0; i < n; i++) {
            result[i] = revealed.removeFirst();
        }

        return result;
    }

    public static void main(String[] args) {
        int[] deck = {1,1000};
        int[] result = deckRevealedIncreasing(deck);
        System.out.println("Revealed card order: " + Arrays.toString(result));
    }
}



```

Q7.
```java
/*
Design a queue that supports `push` and `pop` operations in the front, middle, and back.

Implement the `FrontMiddleBack` class:

- `FrontMiddleBack()` Initializes the queue.
- `void pushFront(int val)` Adds `val` to the **front** of the queue.
- `void pushMiddle(int val)` Adds `val` to the **middle** of the queue.
- `void pushBack(int val)` Adds `val` to the **back** of the queue.
- `int popFront()` Removes the **front** element of the queue and returns it. If the queue is empty, return `1`.
- `int popMiddle()` Removes the **middle** element of the queue and returns it. If the queue is empty, return `1`.
- `int popBack()` Removes the **back** element of the queue and returns it. If the queue is empty, return `1`.

**Notice** that when there are **two** middle position choices, the operation is performed on the **frontmost** middle position choice. For example:

- Pushing `6` into the middle of `[1, 2, 3, 4, 5]` results in `[1, 2, 6, 3, 4, 5]`.
- Popping the middle from `[1, 2, 3, 4, 5, 6]` returns `3` and results in `[1, 2, 4, 5, 6]`.

*/
import java.util.ArrayDeque;
import java.util.Deque;

public class Question7 {
    private Deque<Integer> frontDeque;
    private Deque<Integer> backDeque;

    public Question7() {
        frontDeque = new ArrayDeque<>();
        backDeque = new ArrayDeque<>();
    }

    public void pushFront(int val) {
        frontDeque.offerFirst(val);
        balanceQueues();
    }

    public void pushMiddle(int val) {
        if (frontDeque.size() > backDeque.size()) {
            backDeque.offerFirst(frontDeque.pollLast());
        }
        frontDeque.offerLast(val);
    }

    public void pushBack(int val) {
        backDeque.offerLast(val);
        balanceQueues();
    }

    public int popFront() {
        if (isEmpty()) {
            return -1;
        }
        int val = frontDeque.isEmpty() ? backDeque.pollFirst() : frontDeque.pollFirst();
        balanceQueues();
        return val;
    }

    public int popMiddle() {
        if (isEmpty()) {
            return -1;
        }
        int val;
        if (frontDeque.size() >= backDeque.size()) {
            val = frontDeque.pollLast();
        } else {
            val = backDeque.pollFirst();
        }
        balanceQueues();
        return val;
    }

    public int popBack() {
        if (isEmpty()) {
            return -1;
        }
        int val = backDeque.isEmpty() ? frontDeque.pollLast() : backDeque.pollLast();
        balanceQueues();
        return val;
    }

    private boolean isEmpty() {
        return frontDeque.isEmpty() && backDeque.isEmpty();
    }

    private void balanceQueues() {
        if (frontDeque.size() > backDeque.size() + 1) {
            backDeque.offerFirst(frontDeque.pollLast());
        } else if (backDeque.size() > frontDeque.size()) {
            frontDeque.offerLast(backDeque.pollFirst());
        }
    }

    public static void main(String[] args) {
        Question7 queue = new Question7();
        queue.pushFront(1);
        queue.pushBack(2);
        queue.pushMiddle(3);
        System.out.println(queue.popFront()); // Output: 1
        System.out.println(queue.popMiddle()); // Output: 3
        System.out.println(queue.popBack()); // Output: 2
    }
}


```

Q8.
```java
/*
For a stream of integers, implement a data structure that checks if the last `k` integers parsed in the stream are **equal** to `value`.

Implement the **DataStream** class:

- `DataStream(int value, int k)` Initializes the object with an empty integer stream and the two integers `value` and `k`.
- `boolean consec(int num)` Adds `num` to the stream of integers. Returns `true` if the last `k` integers are equal to `value`, and `false` otherwise. If there are less than `k` integers, the condition does not hold true, so returns `false`.

Input
["DataStream", "consec", "consec", "consec", "consec"]
[[4, 3], [4], [4], [4], [3]]
Output
[null, false, false, true, false]

Explanation
DataStream dataStream = new DataStream(4, 3); //value = 4, k = 3
dataStream.consec(4); // Only 1 integer is parsed, so returns False.
dataStream.consec(4); // Only 2 integers are parsed.
                      // Since 2 is less than k, returns False.
dataStream.consec(4); // The 3 integers parsed are all equal to value, so returns True.
dataStream.consec(3); // The last k integers parsed in the stream are [4,4,3].
                      // Since 3 is not equal to value, it returns False.
*/
import java.util.LinkedList;
import java.util.Queue;

public class Question8 {
    private int value;
    private int k;
    private Queue<Integer> queue;

    public Question8(int value, int k) {
        this.value = value;
        this.k = k;
        this.queue = new LinkedList<>();
    }

    public boolean consec(int num) {
        queue.offer(num);
        if (queue.size() < k) {
            return false;
        }
        if (queue.size() > k) {
            queue.poll();
        }
        return allEqual(value);
    }

    private boolean allEqual(int num) {
        for (int n : queue) {
            if (n != num) {
                return false;
            }
        }
        return true;
    }

    public static void main(String[] args) {
        Question8 dataStream = new Question8(4, 3);
        System.out.println(dataStream.consec(4)); // Output: false
        System.out.println(dataStream.consec(4)); // Output: false
        System.out.println(dataStream.consec(4)); // Output: true
        System.out.println(dataStream.consec(3)); // Output: false
    }
}


```






