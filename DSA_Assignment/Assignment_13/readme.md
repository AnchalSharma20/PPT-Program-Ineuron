Q1.
```Java
/*

Given two linked list of the same size, the task is to create a new linked list using those linked lists. The condition is that the greater node among both linked list will be added to the new linked list.
Input: list1 = 5->2->3->8
list2 = 1->7->4->5
Output: New list = 5->7->4->8

Input:list1 = 2->8->9->3
list2 = 5->3->6->4
Output: New list = 5->8->9->4
*/

class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}

public class Question01 {
    public static ListNode createNewList(ListNode list1, ListNode list2) {
        ListNode head = null;
        ListNode tail = null;

        while (list1 != null && list2 != null) {
            int val1 = list1.val;
            int val2 = list2.val;

            int greaterVal = Math.max(val1, val2);
            ListNode newNode = new ListNode(greaterVal);

            if (head == null) {
                head = newNode;
                tail = newNode;
            } else {
                tail.next = newNode;
                tail = tail.next;
            }

            list1 = list1.next;
            list2 = list2.next;
        }

        return head;
    }

    public static void printList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        // Example 1
        ListNode list1 = new ListNode(5);
        list1.next = new ListNode(2);
        list1.next.next = new ListNode(3);
        list1.next.next.next = new ListNode(8);

        ListNode list2 = new ListNode(1);
        list2.next = new ListNode(7);
        list2.next.next = new ListNode(4);
        list2.next.next.next = new ListNode(5);

        ListNode newList = createNewList(list1, list2);
        System.out.print("New list: ");
        printList(newList);

        // Example 2
        ListNode list3 = new ListNode(2);
        list3.next = new ListNode(8);
        list3.next.next = new ListNode(9);
        list3.next.next.next = new ListNode(3);

        ListNode list4 = new ListNode(5);
        list4.next = new ListNode(3);
        list4.next.next = new ListNode(6);
        list4.next.next.next = new ListNode(4);

        ListNode newList2 = createNewList(list3, list4);
        System.out.print("New list: ");
        printList(newList2);
    }
}
```

Q2.
```Java
/*
Write a function that takes a list sorted in non-decreasing order and deletes any duplicate nodes from the list. The list should only be traversed once.

For example if the linked list is 11->11->11->21->43->43->60 then removeDuplicates() should convert the list to 11->21->43->60.
Input:
LinkedList: 
11->11->11->21->43->43->60
Output:
11->21->43->60
*/

class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}

public class Question2 {
    public static ListNode removeDuplicates(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }

        ListNode current = head;

        while (current != null && current.next != null) {
            if (current.val == current.next.val) {
                current.next = current.next.next;
            } else {
                current = current.next;
            }
        }

        return head;
    }

    public static void printList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        ListNode head = new ListNode(11);
        head.next = new ListNode(11);
        head.next.next = new ListNode(11);
        head.next.next.next = new ListNode(21);
        head.next.next.next.next = new ListNode(43);
        head.next.next.next.next.next = new ListNode(43);
        head.next.next.next.next.next.next = new ListNode(60);

        System.out.print("Original list: ");
        printList(head);

        ListNode newList = removeDuplicates(head);
        System.out.print("List after removing duplicates: ");
        printList(newList);
    }
}

```


Q3.
```Java
/*

Given a linked list of size N. The task is to reverse every k nodes (where k is an input to the function) in the linked list. If the number of nodes is not a multiple of k then left-out nodes, in the end, should be considered as a group and must be reversed (See Example 2 for clarification).
Input:
LinkedList: 1->2->2->4->5->6->7->8
K = 4
Output:4 2 2 1 8 7 6 5
Explanation:
The first 4 elements 1,2,2,4 are reversed first
and then the next 4 elements 5,6,7,8. Hence, the
resultant linked list is 4->2->2->1->8->7->6->5.

*/
class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
        this.next = null;
    }
}

public class Question3 {
    public static ListNode reverseKGroup(ListNode head, int k) {
        if (head == null || head.next == null || k == 1) {
            return head;
        }

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prevGroupTail = dummy;
        ListNode current = head;
        int count = 0;

        while (current != null) {
            count++;
            if (count % k == 0) {
                prevGroupTail = reverseGroup(prevGroupTail, current.next);
                current = prevGroupTail.next;
            } else {
                current = current.next;
            }
        }

        return dummy.next;
    }

    public static ListNode reverseGroup(ListNode prevGroupTail, ListNode nextGroupHead) {
        ListNode prev = prevGroupTail.next;
        ListNode current = prev.next;

        while (current != nextGroupHead) {
            ListNode next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }

        ListNode groupHead = prevGroupTail.next;
        groupHead.next = nextGroupHead;
        prevGroupTail.next = prev;

        return groupHead;
    }

    public static void printList(ListNode head) {
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

        int k = 3;

        System.out.print("Original list: ");
        printList(head);

        ListNode reversed = reverseKGroup(head, k);

        System.out.print("Reversed list: ");
        printList(reversed);
    }
}
```

Q4.
```Java
/*
Given a linked list, write a function to reverse every alternate k nodes (where k is an input to the function) in an efficient way. Give the complexity of your algorithm.
Inputs:   1->2->3->4->5->6->7->8->9->NULL and k = 3
Output:   3->2->1->4->5->6->9->8->7->NULL.
*/



class ListNode {
    int val;
    ListNode next;
    
    public ListNode(int val) {
        this.val = val;
    }
}

public class Question4 {
    public static ListNode reverseAlternateKNodes(ListNode head, int k) {
        if (head == null || k <= 1) {
            return head;
        }

        ListNode current = head;
        ListNode previous = null;

        // Reverse k nodes
        int count = 0;
        while (current != null && count < k) {
            ListNode nextNode = current.next;
            current.next = previous;
            previous = current;
            current = nextNode;
            count++;
        }

        // Skip the next k nodes
        count = 0;
        while (current != null && count < k) {
            current = current.next;
            count++;
        }

        // Recursively reverse the remaining alternate k nodes
        if (current != null) {
            head.next = reverseAlternateKNodes(current, k);
        }

        return previous;
    }

    public static void printList(ListNode head) {
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
        head.next.next.next = new ListNode(5);
        head.next.next.next.next = new ListNode(2);
        head.next.next.next.next.next = new ListNode(10);

        int k = 2;

        System.out.println("Original list:");
        printList(head);

        head = reverseAlternateKNodes(head, k);

        System.out.println("Reversed list:");
        printList(head);
    }
}
```

Q5.
```Java
/*

Given a linked list and a key to be deleted. Delete last occurrence of key from linked. The list may have duplicates.
Input:   1->2->3->5->2->10, key = 2
Output:  1->2->3->5->10

*/

class ListNode {
    int val;
    ListNode next;
    
    public ListNode(int val) {
        this.val = val;
    }
}

public class Question5 {
    public static ListNode deleteLastOccurrence(ListNode head, int key) {
        if (head == null)
            return null;

        ListNode prev = null;
        ListNode lastOccurrence = null;
        ListNode current = head;
        ListNode nextNode = null;

        // Find the last occurrence of the key
        while (current != null) {
            if (current.val == key)
                lastOccurrence = prev;
            prev = current;
            current = current.next;
        }

        // If last occurrence is found, delete the node
        if (lastOccurrence != null) {
            nextNode = lastOccurrence.next;
            lastOccurrence.next = nextNode.next;
        } else {
            // If last occurrence is the head node, update the head
            nextNode = head;
            head = head.next;
        }

        // Clean up memory
        nextNode.next = null;

        return head;
    }

    public static void printList(ListNode head) {
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
        head.next.next.next = new ListNode(5);
        head.next.next.next.next = new ListNode(2);
        head.next.next.next.next.next = new ListNode(10);

        int key = 2;

        System.out.println("Original list:");
        printList(head);

        head = deleteLastOccurrence(head, key);

        System.out.println("Modified list:");
        printList(head);
    }
}
```

Q6.
```Java
/*

Given two sorted linked lists consisting of **N** and **M** nodes respectively. The task is to merge both of the lists (in place) and return the head of the merged list.

**Examples:**

Input: a: 5->10->15, b: 2->3->20

Output: 2->3->5->10->15->20

Input: a: 1->1, b: 2->4

Output: 1->1->2->4

*/

class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
    }
}

public class Question6 {
    public static ListNode mergeSortedLists(ListNode a, ListNode b) {
        // Create a dummy node as the head of the merged list
        ListNode dummyNode = new ListNode(0);
        ListNode current = dummyNode;

        // Traverse both lists and compare the nodes
        while (a != null && b != null) {
            if (a.val <= b.val) {
                current.next = a;
                a = a.next;
            } else {
                current.next = b;
                b = b.next;
            }
            current = current.next;
        }

        // Attach the remaining nodes of the non-empty list
        if (a != null) {
            current.next = a;
        } else if (b != null) {
            current.next = b;
        }

        // Return the head of the merged list
        return dummyNode.next;
    }

    public static void printList(ListNode head) {
        ListNode current = head;
        while (current != null) {
            System.out.print(current.val + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        ListNode a = new ListNode(5);
        a.next = new ListNode(10);
        a.next.next = new ListNode(15);

        ListNode b = new ListNode(2);
        b.next = new ListNode(3);
        b.next.next = new ListNode(20);

        System.out.println("List a:");
        printList(a);

        System.out.println("List b:");
        printList(b);

        ListNode merged = mergeSortedLists(a, b);

        System.out.println("Merged list:");
        printList(merged);
    }
}
```

Q7.
```Java
/*
Given a Doubly Linked List, the task is to reverse the given Doubly Linked List.
Original Linked list 10 8 4 2
Reversed Linked list 2 4 8 10
*/


class Node {
    int data;
    Node prev;
    Node next;

    public Node(int data) {
        this.data = data;
    }
}

public class Question7 {
    public static Node reverseDoublyLinkedList(Node head) {
        if (head == null || head.next == null) {
            return head;
        }

        Node current = head;
        Node previous = null;

        while (current != null) {
            // Swap previous and next pointers
            Node temp = current.next;
            current.next = previous;
            current.prev = temp;

            // Move to the next nodes
            previous = current;
            current = temp;
        }

        // Update the head to the last node
        head = previous;

        return head;
    }

    public static void printList(Node head) {
        Node current = head;
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        // Create the original doubly linked list
        Node head = new Node(10);
        Node node1 = new Node(8);
        Node node2 = new Node(4);
        Node node3 = new Node(2);

        head.next = node1;
        node1.prev = head;
        node1.next = node2;
        node2.prev = node1;
        node2.next = node3;
        node3.prev = node2;

        System.out.println("Original Linked List:");
        printList(head);

        // Reverse the doubly linked list
        head = reverseDoublyLinkedList(head);

        System.out.println("Reversed Linked List:");
        printList(head);
    }
}
```

Q8.
```Java
/*

Given a doubly linked list and a position. The task is to delete a node from given position in a doubly linked list.
Input:
LinkedList = 1 <--> 3 <--> 4
x = 3
Output:1 3
Explanation:After deleting the node at
position 3 (position starts from 1),
the linked list will be now as 1->3.


*/

class Node {
    int data;
    Node prev;
    Node next;

    public Node(int data) {
        this.data = data;
    }
}

public class Question8 {
    public static Node deleteNode(Node head, int position) {
        if (head == null)
            return null;

        // Case 1: Deleting the head node
        if (position == 1) {
            Node newHead = head.next;
            if (newHead != null)
                newHead.prev = null;
            head.next = null;
            return newHead;
        }

        Node current = head;
        int count = 1;

        // Traverse to the position to be deleted
        while (current != null && count < position) {
            current = current.next;
            count++;
        }

        // Case 2: Deleting a node
        if (current != null) {
            // Update the previous node's next pointer
            if (current.prev != null)
                current.prev.next = current.next;

            // Update the next node's previous pointer
            if (current.next != null)
                current.next.prev = current.prev;

            // Disconnect the current node
            current.prev = null;
            current.next = null;
        }

        return head;
    }

    public static void printList(Node head) {
        Node current = head;
        while (current != null) {
            System.out.print(current.data + " ");
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        // Create the doubly linked list
        Node head = new Node(1);
        Node node1 = new Node(3);
        Node node2 = new Node(4);

        head.next = node1;
        node1.prev = head;
        node1.next = node2;
        node2.prev = node1;

        System.out.println("Original Doubly Linked List:");
        printList(head);

        int positionToDelete = 3;
        head = deleteNode(head, positionToDelete);

        System.out.println("Doubly Linked List after deleting node at position " + positionToDelete + ":");
        printList(head);
    }
}
```

