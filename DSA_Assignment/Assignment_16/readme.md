Q1.
```java
/*
Given an array,for each element find the value of the nearest element to the right which is having a frequency greater than that of the current element.If there does not exist an answer for a position,then make the value‘-1’.
Input: a[] = [1, 1, 2, 3, 4, 2, 1]
Output : [-1, -1, 1, 2, 2, 1, -1]

*/

import java.util.*;



public class Question01 {
    public static int[] findNearestGreaterFrequency(int[] arr) {
        Map<Integer, Integer> frequencyMap = new HashMap<>();
        Stack<Integer> stack = new Stack<>();
        int[] result = new int[arr.length];

        for (int i = arr.length - 1; i >= 0; i--) {
            frequencyMap.put(arr[i], frequencyMap.getOrDefault(arr[i], 0) + 1);

            while (!stack.isEmpty() && frequencyMap.get(arr[stack.peek()]) <= frequencyMap.get(arr[i])) {
                int index = stack.pop();
                if (frequencyMap.get(arr[i]) > frequencyMap.get(arr[index])) {
                    result[index] = arr[i];
                }
            }

            stack.push(i);
        }

        return result;
    }

    public static void main(String[] args) {
        int[] arr = {1, 1, 1, 2, 2, 2, 2, 11, 3, 3};
        int[] output = findNearestGreaterFrequency(arr);

        System.out.print("Output: [");
        for (int i = 0; i < output.length; i++) {
            System.out.print(output[i]);
            if (i < output.length - 1) {
                System.out.print(", ");
            }
        }
        System.out.println("]");
    }
}
```

Q2.
```java
/*
Given a stack of integers, sort it in ascending order using another temporary stack.

Input : [34, 3, 31, 98, 92, 23]
Output : [3, 23, 31, 34, 92, 98]

Input : [3, 5, 1, 4, 2, 8]
Output : [1, 2, 3, 4, 5, 8]

*/



import java.util.Stack;

public class Question2 {
	public static Stack<Integer> sortStack(Stack<Integer> inputStack) {
	    Stack<Integer> tempStack = new Stack<>();

	    while (!inputStack.isEmpty()) {
	        int temp = inputStack.pop();

	        while (!tempStack.isEmpty() && tempStack.peek() < temp) {
	            inputStack.push(tempStack.pop());
	        }

	        tempStack.push(temp);
	    }

	    return tempStack;
	}


    public static void main(String[] args) {
        Stack<Integer> stack1 = new Stack<>();
        stack1.push(34);
        stack1.push(3);
        stack1.push(31);
        stack1.push(98);
        stack1.push(92);
        stack1.push(23);
        System.out.println("Input stack: " + stack1);
        Stack<Integer> sortedStack1 = sortStack(stack1);
        System.out.println("Sorted stack: " + sortedStack1);

        Stack<Integer> stack2 = new Stack<>();
        stack2.push(3);
        stack2.push(5);
        stack2.push(1);
        stack2.push(4);
        stack2.push(2);
        stack2.push(8);
        System.out.println("Input stack: " + stack2);
        Stack<Integer> sortedStack2 = sortStack(stack2);
        System.out.println("Sorted stack: " + sortedStack2);
    }
}
```

Q3.
```java
/*
Given a stack with **push()**, **pop()**, and **empty()** operations, The task is to delete the **middle** element ****of it without using any additional data structure.

Input  : Stack[] = [1, 2, 3, 4, 5]

Output : Stack[] = [1, 2, 4, 5]

Input  : Stack[] = [1, 2, 3, 4, 5, 6]

Output : Stack[] = [1, 2, 4, 5, 6]
Input:
push(2)
push(3)
pop()
push(4)
pop()
Output:3 4
Explanation:
push(2) the stack will be {2}
push(3) the stack will be {2 3}
pop()   poped element will be 3 the
        stack will be {2}
push(4) the stack will be {2 4}
pop()   poped element will be 4

*/

import java.util.Stack;

public class Question3 {
    private static int count = 0;

    public static Stack<Integer> deleteMiddle(Stack<Integer> stack) {
        if (stack.isEmpty() || stack.size() == 1) {
            return stack;
        }

        int mid = stack.pop();
        stack = deleteMiddle(stack);

        if (count != stack.size()) {
            stack.push(mid);
        }

        count++;
        return stack;
    }

    public static void main(String[] args) {
        Stack<Integer> stack1 = new Stack<>();
        stack1.push(1);
        stack1.push(2);
        stack1.push(3);
        stack1.push(4);
        stack1.push(5);
        System.out.println("Input stack: " + stack1);
        Stack<Integer> modifiedStack1 = deleteMiddle(stack1);
        System.out.println("Modified stack: " + modifiedStack1);

        Stack<Integer> stack2 = new Stack<>();
        stack2.push(1);
        stack2.push(2);
        stack2.push(3);
        stack2.push(4);
        stack2.push(5);
        stack2.push(6);
        System.out.println("Input stack: " + stack2);
        Stack<Integer> modifiedStack2 = deleteMiddle(stack2);
        System.out.println("Modified stack: " + modifiedStack2);
    }
}
```

Q4.
```java
/*
Given a Queue consisting of first **n** natural numbers (in random order). The task is to check whether the given Queue elements can be arranged in increasing order in another Queue using a stack. The operation allowed are:

1. Push and pop elements from the stack
2. Pop (Or Dequeue) from the given Queue.
3. Push (Or Enqueue) in the another Queue.

**Examples :**

Input : Queue[] = { 5, 1, 2, 3, 4 } 

Output : Yes 

Pop the first element of the given Queue 

i.e 5. Push 5 into the stack. 

Now, pop all the elements of the given Queue and push them to second Queue. 

Now, pop element 5 in the stack and push it to the second Queue.   

Input : Queue[] = { 5, 1, 2, 6, 3, 4 } 

Output : No 

Push 5 to stack. 

Pop 1, 2 from given Queue and push it to another Queue. 

Pop 6 from given Queue and push to stack. 

Pop 3, 4 from given Queue and push to second Queue. 

Now, from using any of above operation, we cannot push 5 into the second Queue because it is below the 6 in the stack.
*/



import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;

public class Question4 {
    public static String checkQueueArrangement(Queue<Integer> givenQueue) {
        Stack<Integer> stack = new Stack<>();
        Queue<Integer> secondQueue = new LinkedList<>();
        int expectedElement = 1;

        while (!givenQueue.isEmpty()) {
            if (givenQueue.peek() == expectedElement) {
                secondQueue.add(givenQueue.remove());
                expectedElement++;
            } else if (!stack.isEmpty() && stack.peek() == expectedElement) {
                secondQueue.add(stack.pop());
                expectedElement++;
            } else {
                stack.push(givenQueue.remove());
            }
        }

        while (!stack.isEmpty()) {
            if (stack.peek() == expectedElement) {
                secondQueue.add(stack.pop());
                expectedElement++;
            } else {
                return "No";
            }
        }

        if (secondQueue.isEmpty()) {
            return "Yes";
        } else {
            return "No";
        }
    }

    public static void main(String[] args) {
        Queue<Integer> queue1 = new LinkedList<>();
        queue1.add(5);
        queue1.add(1);
        queue1.add(2);
        queue1.add(3);
        queue1.add(4);
        System.out.println("Input queue: " + queue1);
        String result1 = checkQueueArrangement(queue1);
        System.out.println("Result: " + result1);

        Queue<Integer> queue2 = new LinkedList<>();
        queue2.add(5);
        queue2.add(1);
        queue2.add(2);
        queue2.add(6);
        queue2.add(3);
        queue2.add(4);
        System.out.println("Input queue: " + queue2);
        String result2 = checkQueueArrangement(queue2);
        System.out.println("Result: " + result2);
    }
}
```

Q5.
```java
/*


Given a number , write a program to reverse this number using stack.
Input : 365
Output : 563

Input : 6899
Output : 9986
*/

import java.util.Stack;

public class Question5 {
    public static int reverseNumber(int number) {
        String numberString = Integer.toString(number);
        Stack<Character> stack = new Stack<>();

        for (int i = 0; i < numberString.length(); i++) {
            stack.push(numberString.charAt(i));
        }

        StringBuilder reversedNumberBuilder = new StringBuilder();
        while (!stack.isEmpty()) {
            reversedNumberBuilder.append(stack.pop());
        }

        String reversedNumberString = reversedNumberBuilder.toString();
        int reversedNumber = Integer.parseInt(reversedNumberString);

        return reversedNumber;
    }

    public static void main(String[] args) {
        int number1 = 365;
        int reversedNumber1 = reverseNumber(number1);
        System.out.println("Input: " + number1);
        System.out.println("Reversed number: " + reversedNumber1);

        int number2 = 6899;
        int reversedNumber2 = reverseNumber(number2);
        System.out.println("Input: " + number2);
        System.out.println("Reversed number: " + reversedNumber2);
    }
}
```

Q6.
```java
/*

Given an integer k and a **[queue](https://www.geeksforgeeks.org/queue-data-structure/)** of integers, The task is to reverse the order of the first **k** elements of the queue, leaving the other elements in the same relative order.

Only following standard operations are allowed on queue.

- enqueue(x) :Add an item x to rear of queue
- dequeue() :Remove an item from front of queue
- size() :Returns number of elements in queue.
- front() :Finds front item.


*/

import java.util.LinkedList;
import java.util.Queue;
import java.util.Stack;

public class Question6 {
    public static Queue<Integer> reverseFirstKElements(Queue<Integer> queue, int k) {
        if (queue.isEmpty() || k <= 0 || k > queue.size()) {
            return queue;
        }

        Stack<Integer> stack = new Stack<>();

        // Dequeue the first k elements and push them onto the stack
        for (int i = 0; i < k; i++) {
            stack.push(queue.remove());
        }

        // Enqueue the elements from the stack back into the queue
        while (!stack.isEmpty()) {
            queue.add(stack.pop());
        }

        // Dequeue the remaining elements and enqueue them back into the queue
        for (int i = 0; i < queue.size() - k; i++) {
            queue.add(queue.remove());
        }

        return queue;
    }

    public static void main(String[] args) {
        Queue<Integer> queue1 = new LinkedList<>();
        queue1.add(1);
        queue1.add(2);
        queue1.add(3);
        queue1.add(4);
        queue1.add(5);
        int k1 = 3;
        System.out.println("Input queue: " + queue1);
        System.out.println("k: " + k1);
        Queue<Integer> modifiedQueue1 = reverseFirstKElements(queue1, k1);
        System.out.println("Modified queue: " + modifiedQueue1);

        Queue<Integer> queue2 = new LinkedList<>();
        queue2.add(10);
        queue2.add(20);
        queue2.add(30);
        queue2.add(40);
        queue2.add(50);
        queue2.add(60);
        int k2 = 5;
        System.out.println("Input queue: " + queue2);
        System.out.println("k: " + k2);
        Queue<Integer> modifiedQueue2 = reverseFirstKElements(queue2, k2);
        System.out.println("Modified queue: " + modifiedQueue2);
    }
}
```

Q7.
```java
/*
Given a sequence of n strings, the task is to check if any two similar words come together and then destroy each other then print the number of words left in the sequence after this pairwise destruction.
**Examples:**
Input : ab aa aa bcd ab
Output : 3
As aa, aa destroys each other so,
ab bcd ab is the new sequence.
Input :  tom jerry jerry tom
Output : 0
As first both jerry will destroy each other.
Then sequence will be tom, tom they will also destroy
each other. So, the final sequence doesn’t contain any
word.
*/



import java.util.Stack;

public class Question7 {
    public static int countRemainingWords(String[] words) {
        Stack<String> stack = new Stack<>();

        for (String word : words) {
            if (!stack.isEmpty() && stack.peek().equals(word)) {
                stack.pop();
            } else {
                stack.push(word);
            }
        }

        return stack.size();
    }

    public static void main(String[] args) {
        String[] sequence1 = {"ab", "aa", "aa", "bcd", "ab"};
        int remainingWords1 = countRemainingWords(sequence1);
        System.out.println("Input sequence: ab aa aa bcd ab");
        System.out.println("Number of words left: " + remainingWords1);

        String[] sequence2 = {"tom", "jerry", "jerry", "tom"};
        int remainingWords2 = countRemainingWords(sequence2);
        System.out.println("Input sequence: tom jerry jerry tom");
        System.out.println("Number of words left: " + remainingWords2);
    }
}

```

Q8.
```java
/*

Given an array of integers, the task is to find the maximum absolute difference between the nearest left and the right smaller element of every element in the array.

**Note:** If there is no smaller element on right side or left side of any element then we take zero as the smaller element. For example for the leftmost element, the nearest smaller element on the left side is considered as 0. Similarly, for rightmost elements, the smaller element on the right side is considered as 0.
Input : arr[] = {2, 1, 8}
Output : 1
Left smaller  LS[] {0, 0, 1}
Right smaller RS[] {1, 0, 0}
Maximum Diff of abs(LS[i] - RS[i]) = 1

Input  : arr[] = {2, 4, 8, 7, 7, 9, 3}
Output : 4
Left smaller   LS[] = {0, 2, 4, 4, 4, 7, 2}
Right smaller  RS[] = {0, 3, 7, 3, 3, 3, 0}
Maximum Diff of abs(LS[i] - RS[i]) = 7 - 3 = 4

Input : arr[] = {5, 1, 9, 2, 5, 1, 7}
Output : 1
*/


import java.util.Stack;

public class Question8 {
    public static int findMaxDifference(int[] arr) {
        int n = arr.length;

        int[] LS = new int[n]; // Nearest smaller element on the left
        int[] RS = new int[n]; // Nearest smaller element on the right

        Stack<Integer> stack = new Stack<>();

        // Calculate LS array
        for (int i = 0; i < n; i++) {
            while (!stack.isEmpty() && arr[stack.peek()] >= arr[i]) {
                stack.pop();
            }

            if (stack.isEmpty()) {
                LS[i] = 0;
            } else {
                LS[i] = arr[stack.peek()];
            }

            stack.push(i);
        }

        stack.clear();

        // Calculate RS array
        for (int i = n - 1; i >= 0; i--) {
            while (!stack.isEmpty() && arr[stack.peek()] >= arr[i]) {
                stack.pop();
            }

            if (stack.isEmpty()) {
                RS[i] = 0;
            } else {
                RS[i] = arr[stack.peek()];
            }

            stack.push(i);
        }

        int maxDiff = Integer.MIN_VALUE;

        // Calculate the maximum absolute difference
        for (int i = 0; i < n; i++) {
            int diff = Math.abs(LS[i] - RS[i]);
            if (diff > maxDiff) {
                maxDiff = diff;
            }
        }

        return maxDiff;
    }

    public static void main(String[] args) {
        int[] arr1 = {2, 1, 8};
        int maxDiff1 = findMaxDifference(arr1);
        System.out.println("Input array: [2, 1, 8]");
        System.out.println("Maximum absolute difference: " + maxDiff1);

        int[] arr2 = {2, 4, 8, 7, 7, 9, 3};
        int maxDiff2 = findMaxDifference(arr2);
        System.out.println("Input array: [2, 4, 8, 7, 7, 9, 3]");
        System.out.println("Maximum absolute difference: " + maxDiff2);

        int[] arr3 = {5, 1, 9, 2, 5, 1, 7};
        int maxDiff3 = findMaxDifference(arr3);
        System.out.println("Input array: [5, 1, 9, 2, 5, 1, 7]");
        System.out.println("Maximum absolute difference: " + maxDiff3);
    }
}


```





