Q1.
```java
/*

Given a linked list of **N** nodes such that it may contain a loop.

A loop here means that the last node of the link list is connected to the node at position X(1-based index). If the link list does not have any loop, X=0.

Remove the loop from the linked list, if it is present, i.e. unlink the last node which is forming the loop.

Input:
N = 3
value[] = {1,3,4}
X = 2
Output:1
Explanation:The link list looks like
1 -> 3 -> 4
     ^    |
     |____|
A loop is present. If you remove it
successfully, the answer will be 1.

*/

class Node {
    int data;
    Node next;

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}

public class Question01 {
    public static Node detectAndRemoveLoop(Node head) {
        Node slow = head;
        Node fast = head;

        // Detect the loop using Floyd's cycle-finding algorithm
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;

            if (slow == fast)
                break;
        }

        // If no loop exists, return the head as is
        if (fast == null || fast.next == null)
            return head;

        // Reset one of the pointers to the head and move both pointers until they meet again
        slow = head;
        while (slow.next != fast.next) {
            slow = slow.next;
            fast = fast.next;
        }

        // Remove the loop by making the next pointer of the node just before the start of the loop null
        fast.next = null;

        return head;
    }

    public static void printLinkedList(Node head) {
        Node current = head;
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Node head = new Node(1);
        head.next = new Node(3);
        head.next.next = new Node(4);
        head.next.next.next = head.next;

        System.out.print("Original Linked List: ");
        printLinkedList(head);

        head = detectAndRemoveLoop(head);

        System.out.print("Linked List after removing the loop: ");
        printLinkedList(head);
    }
}
```

Q2.
```java
/*
A number N is represented in Linked List such that each digit corresponds to a node in linked list. You need to add 1 to it.
Input:
LinkedList: 4->5->6
Output:457

*/

class Node {
    int data;
    Node next;

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}

public class Question2 {
    public static Node reverseLinkedList(Node head) {
        Node prev = null;
        Node current = head;
        Node next;

        while (current != null) {
            next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }

        return prev;
    }

    public static Node addOne(Node head) {
        if (head == null)
            return null;

        Node reversedHead = reverseLinkedList(head);
        Node current = reversedHead;
        Node prev = null;
        boolean carry = true;

        while (current != null && carry) {
            int sum = current.data + 1;
            carry = sum > 9;
            current.data = sum % 10;
            prev = current;
            current = current.next;
        }

        if (carry) {
            prev.next = new Node(1);
        }

        return reverseLinkedList(reversedHead);
    }

    public static void printLinkedList(Node head) {
        Node current = head;
        while (current != null) {
            System.out.print(current.data);
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        // Example 1: LinkedList: 4->5->6
        Node head1 = new Node(4);
        head1.next = new Node(5);
        head1.next.next = new Node(6);

        System.out.print("Input: ");
        printLinkedList(head1);

        Node result1 = addOne(head1);

        System.out.print("Output: ");
        printLinkedList(result1);

        // Example 2: LinkedList: 1->2->3
        Node head2 = new Node(1);
        head2.next = new Node(2);
        head2.next.next = new Node(3);

        System.out.print("Input: ");
        printLinkedList(head2);

        Node result2 = addOne(head2);

        System.out.print("Output: ");
        printLinkedList(result2);
    }
}
```

Q3.
```java
/*

Given a Linked List of size N, where every node represents a sub-linked-list and contains two pointers:(i) a next pointer to the next node,(ii) a bottom pointer to a linked list where this node is head.Each of the sub-linked-list is in sorted order.Flatten the Link List such that all the nodes appear in a single level while maintaining the sorted order. Note: The flattened list will be printed using the bottom pointer instead of next pointer.
Input:
5 -> 10 -> 19 -> 28
|     |     |     |
7     20    22   35
|           |     |
8          50    40
|                 |
30               45
Output: 5-> 7-> 8- > 10 -> 19-> 20->
22-> 28-> 30-> 35-> 40-> 45-> 50.
Explanation:
The resultant linked lists has every
node in a single level.(Note:| represents the bottom pointer.)

*/
class Node {
    int data;
    Node next;
    Node bottom;

    public Node(int data) {
        this.data = data;
        this.next = null;
        this.bottom = null;
    }
}

public class Question3 {
    public static Node flatten(Node head) {
        if (head == null || head.next == null)
            return head;

        // Merge function to merge two sorted lists
        Node merge(Node a, Node b) {
            if (a == null)
                return b;
            if (b == null)
                return a;

            Node result;
            if (a.data < b.data) {
                result = a;
                result.bottom = merge(a.bottom, b);
            } else {
                result = b;
                result.bottom = merge(a, b.bottom);
            }

            return result;
        }

        Node dummy = new Node(0);
        Node tail = dummy;
        Node curr = head;

        while (curr != null) {
            tail.bottom = curr;
            tail = tail.bottom;
            curr = curr.next;
        }

        Node result = dummy.bottom;

        while (dummy.next != null) {
            result = merge(result, dummy.next.bottom);
            dummy.next = dummy.next.next;
        }

        return result;
    }

    public static void printFlattenedList(Node head) {
        Node current = head;
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.bottom;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Node head = new Node(5);
        head.next = new Node(10);
        head.next.next = new Node(19);
        head.next.next.next = new Node(28);

        head.bottom = new Node(7);
        head.next.bottom = new Node(20);
        head.next.next.bottom = new Node(22);
        head.next.next.next.bottom = new Node(35);

        head.bottom.bottom = new Node(8);
        head.next.bottom.bottom = new Node(50);
        head.next.next.bottom.bottom = new Node(40);

        head.bottom.bottom.bottom = new Node(30);
        head.next.bottom.bottom.bottom = new Node(45);

        System.out.print("Flattened List: ");
        Node flattened = flatten(head);
        printFlattenedList(flattened);
    }
}
```

Q4.
```java
/*
You are given a special linked list with **N** nodes where each node has a next pointer pointing to its next node. You are also given **M** random pointers, where you will be given **M** number of pairs denoting two nodes **a** and **b**  **i.e. a->arb = b** (arb is pointer to random node)**.**

Construct a copy of the given list. The copy should consist of exactly **N** new nodes, where each new node has its value set to the value of its corresponding original node. Both the next and random pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. None of the pointers in the new list should point to nodes in the original list.

For example, if there are two nodes **X** and **Y** in the original list, where **X.arb** **-->** **Y**, then for the corresponding two nodes **x** and **y** in the copied list, **x.arb --> y.**

Return the head of the copied linked list.

Input:
N = 4, M = 2
value = {1,2,3,4}
pairs = {{1,2},{2,4}}
Output:1
Explanation:In this test case, there
are 4 nodes in linked list.  Among these
4 nodes,  2 nodes have arbitrary pointer
set, rest two nodes have arbitrary pointer
as NULL. Second line tells us the value
of four nodes. The third line gives the
information about arbitrary pointers.
The first node arbitrary pointer is set to
node 2.  The second node arbitrary pointer
is set to node 4.

>
*/


class Node {
    int data;
    Node next;
    Node random;

    public Node(int data) {
        this.data = data;
        this.next = null;
        this.random = null;
    }
}

public class Question4 {
    public static Node copyRandomList(Node head) {
        if (head == null)
            return null;

        // HashMap to store the mapping between original and copied nodes
        Map<Node, Node> nodeMap = new HashMap<>();

        // Create a new node for each original node and store the mapping
        Node current = head;
        while (current != null) {
            nodeMap.put(current, new Node(current.data));
            current = current.next;
        }

        // Update the next and random pointers of the copied nodes
        current = head;
        while (current != null) {
            Node copiedNode = nodeMap.get(current);
            copiedNode.next = nodeMap.get(current.next);
            copiedNode.random = nodeMap.get(current.random);
            current = current.next;
        }

        // Return the head of the copied linked list
        return nodeMap.get(head);
    }

    public static void printLinkedList(Node head) {
        Node current = head;
        while (current != null) {
            System.out.print("[" + current.data + ", " +
                    (current.random != null ? current.random.data : "null") + "] ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Node head = new Node(1);
        head.next = new Node(2);
        head.next.next = new Node(3);
        head.next.next.next = new Node(4);

        head.random = head.next;
        head.next.random = head.next.next.next;

        System.out.print("Original Linked List: ");
        printLinkedList(head);

        Node copiedHead = copyRandomList(head);

        System.out.print("Copied Linked List: ");
        printLinkedList(copiedHead);
    }
}

```

Q5.
```java
/*

Given the `head` of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return *the reordered list*.

The **first** node is considered **odd**, and the **second** node is **even**, and so on.

Note that the relative order inside both the even and odd groups should remain as it was in the input.

You must solve the problem in `O(1)` extra space complexity and `O(n)` time complexity.

Input: head = [1,2,3,4,5]
Output: [1,3,5,2,4]

*/

class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}

public class Question5 {
    public static ListNode reorderList(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode oddHead = head;
        ListNode evenHead = head.next;
        ListNode evenNode = evenHead;

        while (evenNode != null && evenNode.next != null) {
            oddHead.next = evenNode.next;
            oddHead = oddHead.next;
            evenNode.next = oddHead.next;
            evenNode = evenNode.next;
        }

        oddHead.next = evenHead;
        return head;
    }

    public static void printLinkedList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(3);
        head.next.next.next = new ListNode(4);
        head.next.next.next.next = new ListNode(5);

        System.out.print("Original Linked List: ");
        printLinkedList(head);

        ListNode reorderedList = reorderList(head);

        System.out.print("Reordered Linked List: ");
        printLinkedList(reorderedList);
    }
}
```

Q6.
```java
/*

Given a singly linked list of size N. The task is to left-shift the linked list by k nodes, where k is a given positive integer smaller than or equal to length of the linked list.
Input:
N = 5
value[] = {2, 4, 7, 8, 9}
k = 3
Output:8 9 2 4 7
Explanation:Rotate 1:4 -> 7 -> 8 -> 9 -> 2
Rotate 2: 7 -> 8 -> 9 -> 2 -> 4
Rotate 3: 8 -> 9 -> 2 -> 4 -> 7

*/

class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}

public class Question6 {
    public static ListNode leftShiftLinkedList(ListNode head, int k) {
        if (head == null || k <= 0) {
            return head;
        }

        int length = getLength(head);
        int shift = k % length;

        if (shift == 0) {
            return head;
        }

        ListNode newHead = null;
        ListNode newTail = null;

        ListNode current = head;
        int count = 0;
        while (current != null) {
            if (count == length - shift - 1) {
                newTail = current;
            }
            if (count == length - shift) {
                newHead = current;
            }
            current = current.next;
            count++;
        }

        newTail.next = null;
        current = newHead;
        while (current.next != null) {
            current = current.next;
        }
        current.next = head;

        return newHead;
    }

    public static int getLength(ListNode head) {
        int length = 0;
        ListNode current = head;
        while (current != null) {
            length++;
            current = current.next;
        }
        return length;
    }

    public static void printLinkedList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(2);
        head.next = new ListNode(4);
        head.next.next = new ListNode(7);
        head.next.next.next = new ListNode(8);
        head.next.next.next.next = new ListNode(9);

        System.out.print("Original Linked List: ");
        printLinkedList(head);

        int k = 3;
        ListNode shiftedList = leftShiftLinkedList(head, k);

        System.out.print("Left-shifted Linked List: ");
        printLinkedList(shiftedList);
    }
}
```

Q7.
```java
/*
You are given the `head` of a linked list with `n` nodes.

For each node in the list, find the value of the **next greater node**. That is, for each node, find the value of the first node that is next to it and has a **strictly larger** value than it.

Return an integer array `answer` where `answer[i]` is the value of the next greater node of the `ith` node (**1-indexed**). If the `ith` node does not have a next greater node, set `answer[i] = 0`.
Input: head = [2,1,5]
Output: [5,5,0]
*/
import java.util.*;

class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
    }
}

public class Question7 {

    public static int[] nextLargerNodes(ListNode head) {
        if (head == null) {
            return new int[0];
        }

        // Convert linked list to array
        List<Integer> list = new ArrayList<>();
        ListNode curr = head;
        while (curr != null) {
            list.add(curr.val);
            curr = curr.next;
        }

        int n = list.size();
        int[] answer = new int[n];
        Stack<Integer> stack = new Stack<>();

        // Traverse the array from right to left
        for (int i = n - 1; i >= 0; i--) {
            int num = list.get(i);

            while (!stack.isEmpty() && num >= list.get(stack.peek())) {
                stack.pop();
            }

            if (!stack.isEmpty()) {
                answer[i] = list.get(stack.peek());
            }

            stack.push(i);
        }

        return answer;
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(2);
        head.next = new ListNode(1);
        head.next.next = new ListNode(5);

        int[] result = nextLargerNodes(head);
        System.out.println(Arrays.toString(result));
    }
}


```

Q8.
```java
/*
Given the `head` of a linked list, we repeatedly delete consecutive sequences of nodes that sum to `0` until there are no such sequences.

After doing so, return the head of the final linked list.  You may return any such answer.

(Note that in the examples below, all sequences are serializations of `ListNode` objects.)
Input: head = [1,2,-3,3,1]
Output: [3,1]
Note: The answer [1,2,1] would also be accepted.

*/

class ListNode {
    int val;
    ListNode next;

    ListNode(int val) {
        this.val = val;
    }
}

public class Question8 {
    public ListNode removeZeroSumSublists(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;

        ListNode slow = dummy;
        ListNode fast = dummy;
        int cumulativeSum = 0;

        while (fast != null) {
            cumulativeSum += fast.val;

            if (cumulativeSum == 0) {
                slow.next = fast.next;
            }

            fast = fast.next;

            if (cumulativeSum != 0) {
                slow = slow.next;
            }
        }

        return dummy.next;
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(1);
        head.next = new ListNode(2);
        head.next.next = new ListNode(-3);
        head.next.next.next = new ListNode(3);
        head.next.next.next.next = new ListNode(1);

        Question8 solution = new Question8();
        ListNode result = solution.removeZeroSumSublists(head);

        while (result != null) {
            System.out.print(result.val + " ");
            result = result.next;
        }
    }
}
```



