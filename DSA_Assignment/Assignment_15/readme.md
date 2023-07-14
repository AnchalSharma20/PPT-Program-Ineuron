Q1.
```java
/*

Given an array arr[ ] of size N having elements, the task is to find the next greater element for each element of the array in order of their appearance in the array.Next greater element of an element in the array is the nearest element on the right which is greater than the current element.If there does not exist next greater of current element, then next greater element for current element is -1. For example, next greater of the last element is always -1.


*/

import java.util.*;

public class Question01 {
    public static int[] findNextGreaterElement(int[] arr) {
        int n = arr.length;
        int[] result = new int[n];
        Stack<Integer> stack = new Stack<>();

        // Iterate the array from right to left
        for (int i = n - 1; i >= 0; i--) {
            // Remove elements from stack that are smaller than current element
            while (!stack.isEmpty() && stack.peek() <= arr[i]) {
                stack.pop();
            }

            // If stack is empty, there is no next greater element
            if (stack.isEmpty()) {
                result[i] = -1;
            } else {
                result[i] = stack.peek();
            }

            // Push the current element onto the stack
            stack.push(arr[i]);
        }

        return result;
    }

    public static void main(String[] args) {
        int[] arr = {1, 3, 2, 4};
        int[] nextGreater = findNextGreaterElement(arr);

        for (int i = 0; i < nextGreater.length; i++) {
            System.out.print(nextGreater[i] + " ");
        }
    }
}
```

Q2.
```java
/*
Given an array a of integers of length n, find the nearest smaller number for every element such that the smaller element is on left side.If no small element present on the left print -1.
Input: n = 3
a = {1, 6, 2}
Output: -1 1 1

EXPLAINATION: There is no number at the
left of 1. Smaller number than 6 and 2 is 1.
*/

import java.util.*;

public class Question2 {
    public static int[] findNearestSmallerNumber(int[] arr) {
        int n = arr.length;
        int[] result = new int[n];
        Stack<Integer> stack = new Stack<>();

        // Iterate the array from left to right
        for (int i = 0; i < n; i++) {
            // Remove elements from stack that are greater than or equal to current element
            while (!stack.isEmpty() && stack.peek() >= arr[i]) {
                stack.pop();
            }

            // If stack is empty, there is no smaller element on the left
            if (stack.isEmpty()) {
                result[i] = -1;
            } else {
                result[i] = stack.peek();
            }

            // Push the current element onto the stack
            stack.push(arr[i]);
        }

        return result;
    }

    public static void main(String[] args) {
        int[] arr = {1, 6, 2};
        int[] nearestSmaller = findNearestSmallerNumber(arr);

        for (int i = 0; i < nearestSmaller.length; i++) {
            System.out.print(nearestSmaller[i] + " ");
        }
    }
}



```

Q3.
```java
/*

Implement a Stack using two queues q1 and q2.
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

import java.util.*;

public class Question3 {
    Queue<Integer> q1;
    Queue<Integer> q2;

    public Question3() {
        q1 = new LinkedList<>();
        q2 = new LinkedList<>();
    }

    public void push(int value) {
        // Add the new element to the empty queue
        q2.add(value);

        // Move all elements from the main queue (q1) to the temporary queue (q2)
        while (!q1.isEmpty()) {
            q2.add(q1.poll());
        }

        // Swap the references of q1 and q2
        Queue<Integer> temp = q1;
        q1 = q2;
        q2 = temp;
    }

    public int pop() {
        if (q1.isEmpty()) {
            throw new NoSuchElementException("Stack is empty");
        }

        // Remove and return the top element from the main queue (q1)
        return q1.poll();
    }

    public static void main(String[] args) {
        Question3 stack = new Question3();

        stack.push(2);
        stack.push(3);
        System.out.print(stack.pop() + " ");
        stack.push(4);
        System.out.print(stack.pop());
    }
}



```

Q4.
```java
/*
You are given a stack St. You have to reverse the stack using recursion.
Input:St = {3,2,1,7,6}
Output:{6,7,1,2,3}
*/



import java.util.*;

public class Question4 {
    public static void reverseStack(Stack<Integer> stack) {
        if (stack.isEmpty()) {
            return;
        }

        int element = stack.pop();
        reverseStack(stack);
        insertAtBottom(stack, element);
    }

    public static void insertAtBottom(Stack<Integer> stack, int element) {
        if (stack.isEmpty()) {
            stack.push(element);
            return;
        }

        int top = stack.pop();
        insertAtBottom(stack, element);
        stack.push(top);
    }

    public static void main(String[] args) {
        Stack<Integer> stack = new Stack<>();
        stack.push(3);
        stack.push(2);
        stack.push(1);
        stack.push(7);
        stack.push(6);

        System.out.println("Original Stack: " + stack);
        reverseStack(stack);
        System.out.println("Reversed Stack: " + stack);
    }
}

```

Q5.
```java
/*


You are given a string S, the task is to reverse the string using stack.
Input: S="GeeksforGeeks"
Output: skeeGrofskeeG
*/

import java.util.*;

public class Question5 {
    public static String reverseString(String str) {
        Stack<Character> stack = new Stack<>();

        // Push each character of the string onto the stack
        for (int i = 0; i < str.length(); i++) {
            stack.push(str.charAt(i));
        }

        StringBuilder reversed = new StringBuilder();

        // Pop each character from the stack and append it to the reversed string
        while (!stack.isEmpty()) {
            reversed.append(stack.pop());
        }

        return reversed.toString();
    }

    public static void main(String[] args) {
        String str = "GeeksforGeeks";
        String reversedString = reverseString(str);
        System.out.println("Original String: " + str);
        System.out.println("Reversed String: " + reversedString);
    }
}
```

Q6.
```java
/*

Given string S representing a postfix expression, the task is to evaluate the expression and find the final value. Operators will only include the basic arithmetic operators like *, /, + and -.
Input: S = "231*+9-"
Output: -4
Explanation:
After solving the given expression,
we have -4 as result.


*/

import java.util.*;

public class Question6 {
    public static int evaluatePostfix(String expression) {
        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < expression.length(); i++) {
            char ch = expression.charAt(i);

            if (Character.isDigit(ch)) {
                stack.push(ch - '0');
            } else {
                int operand2 = stack.pop();
                int operand1 = stack.pop();
                int result = performOperation(ch, operand1, operand2);
                stack.push(result);
            }
        }

        return stack.pop();
    }

    public static int performOperation(char operator, int operand1, int operand2) {
        switch (operator) {
            case '+':
                return operand1 + operand2;
            case '-':
                return operand1 - operand2;
            case '*':
                return operand1 * operand2;
            case '/':
                return operand1 / operand2;
            default:
                throw new IllegalArgumentException("Invalid operator: " + operator);
        }
    }

    public static void main(String[] args) {
        String expression = "123+*8-";
        int result = evaluatePostfix(expression);
        System.out.println("Expression: " + expression);
        System.out.println("Result: " + result);
    }
}


```

Q7.
```java
/*
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

Implement the `MinStack` class:

- `MinStack()` initializes the stack object.
- `void push(int val)` pushes the element `val` onto the stack.
- `void pop()` removes the element on the top of the stack.
- `int top()` gets the top element of the stack.
- `int getMin()` retrieves the minimum element in the stack.

You must implement a solution with `O(1)` time complexity for each function.
Input
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

Output
[null,null,null,null,-3,null,0,-2]

Explanation
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
*/


import java.util.*;

class MinStack {
    private Stack<Integer> stack;
    private Stack<Integer> minStack;

    public MinStack() {
        stack = new Stack<>();
        minStack = new Stack<>();
    }

    public void push(int val) {
        stack.push(val);
        
        if (minStack.isEmpty() || val <= minStack.peek()) {
            minStack.push(val);
        }
    }

    public void pop() {
        if (stack.isEmpty()) {
            throw new EmptyStackException();
        }
        
        int popped = stack.pop();
        
        if (popped == minStack.peek()) {
            minStack.pop();
        }
    }

    public int top() {
        if (stack.isEmpty()) {
            throw new EmptyStackException();
        }
        
        return stack.peek();
    }

    public int getMin() {
        if (minStack.isEmpty()) {
            throw new EmptyStackException();
        }
        
        return minStack.peek();
    }
}

public class Question7 {
    public static void main(String[] args) {
        MinStack minStack = new MinStack();
        minStack.push(-2);
        minStack.push(0);
        minStack.push(-3);
        System.out.println("getMin(): " + minStack.getMin()); // return -3
        minStack.pop();
        System.out.println("top(): " + minStack.top());       // return 0
        System.out.println("getMin(): " + minStack.getMin()); // return -2
    }
}
```

Q8.
```java
/*

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.
Input: height = [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
Explanation: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.

*/


public class Question8 {
    public static int trap(int[] height) {
        int left = 0;
        int right = height.length - 1;
        int leftMax = 0;
        int rightMax = 0;
        int trappedWater = 0;

        while (left < right) {
            if (height[left] <= height[right]) {
                if (height[left] >= leftMax) {
                    leftMax = height[left];
                } else {
                    trappedWater += leftMax - height[left];
                }
                left++;
            } else {
                if (height[right] >= rightMax) {
                    rightMax = height[right];
                } else {
                    trappedWater += rightMax - height[right];
                }
                right--;
            }
        }

        return trappedWater;
    }

    public static void main(String[] args) {
        int[] height = {0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1};
        int trappedWater = trap(height);
        System.out.println("Trapped Water: " + trappedWater);
    }
}


```




