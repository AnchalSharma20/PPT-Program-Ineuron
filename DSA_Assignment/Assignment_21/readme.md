Q1.
```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;

    public TreeNode(int val) {
        this.val = val;
        this.left = null;
        this.right = null;
    }
}

public class BinaryTreeToBST {
    private static void storeNodeValues(TreeNode root, List<Integer> values) {
        if (root == null)
            return;

        storeNodeValues(root.left, values);
        values.add(root.val);
        storeNodeValues(root.right, values);
    }

    private static void convertToBST(TreeNode root, Iterator<Integer> iterator) {
        if (root == null)
            return;

        convertToBST(root.left, iterator);
        root.val = iterator.next();
        convertToBST(root.right, iterator);
    }

    public static void main(String[] args) {
        // Construct the binary tree
        TreeNode root = new TreeNode(10);
        root.left = new TreeNode(2);
        root.right = new TreeNode(7);
        root.left.left = new TreeNode(8);
        root.left.right = new TreeNode(4);

        // Step 1: Store node values
        List<Integer> values = new ArrayList<>();
        storeNodeValues(root, values);

        // Step 2: Sort the values
        Collections.sort(values);

        // Step 3: Convert the binary tree to a binary search tree
        Iterator<Integer> iterator = values.iterator();
        convertToBST(root, iterator);

        // Print the converted binary search tree
        printInorder(root);
    }

    private static void printInorder(TreeNode root) {
        if (root == null)
            return;

        printInorder(root.left);
        System.out.print(root.val + " ");
        printInorder(root.right);
    }
}
```

Q2.
```java
class TreeNode {
    int val;
    TreeNode left, right;

    public TreeNode(int val) {
        this.val = val;
        this.left = null;
        this.right = null;
    }
}

class DoublyLinkedListNode {
    int val;
    DoublyLinkedListNode prev, next;

    public DoublyLinkedListNode(int val) {
        this.val = val;
        this.prev = null;
        this.next = null;
    }
}

public class BinaryTreeToDoublyLinkedList {
    private static TreeNode prevNode;

    private static void convertToDLL(TreeNode root, DoublyLinkedListNode prev) {
        if (root == null)
            return;

        convertToDLL(root.left, prev);

        DoublyLinkedListNode curr = new DoublyLinkedListNode(root.val);

        if (prev != null) {
            prev.next = curr;
            curr.prev = prev;
        } else {
            prevNode = curr;
        }

        prevNode = curr;

        convertToDLL(root.right, prevNode);
    }

    public static DoublyLinkedListNode convertBinaryTreeToDLL(TreeNode root) {
        if (root == null)
            return null;

        convertToDLL(root, null);

        return prevNode;
    }

    public static void printDLL(DoublyLinkedListNode head) {
        DoublyLinkedListNode curr = head;

        while (curr != null) {
            System.out.print(curr.val + " ");
            curr = curr.next;
        }
    }

    public static void main(String[] args) {
        // Construct the binary tree
        TreeNode root = new TreeNode(10);
        root.left = new TreeNode(5);
        root.right = new TreeNode(20);
        root.right.left = new TreeNode(30);
        root.right.right = new TreeNode(35);

        // Convert binary tree to doubly linked list
        DoublyLinkedListNode head = convertBinaryTreeToDLL(root);

        // Print the doubly linked list
        printDLL(head);
    }
}
```

Q3.
```java
import java.util.LinkedList;
import java.util.Queue;

class TreeNode {
    int val;
    TreeNode left, right, next;

    public TreeNode(int val) {
        this.val = val;
        this.left = null;
        this.right = null;
        this.next = null;
    }
}

public class ConnectNodesAtSameLevel {
    public static void connect(TreeNode root) {
        if (root == null)
            return;

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);

        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            TreeNode prev = null;

            for (int i = 0; i < levelSize; i++) {
                TreeNode curr = queue.poll();

                if (prev != null)
                    prev.next = curr;

                prev = curr;

                if (curr.left != null)
                    queue.offer(curr.left);

                if (curr.right != null)
                    queue.offer(curr.right);
            }

            prev.next = null; // Set the next pointer of the last node to null
        }
    }

    public static void printLevelOrderTraversal(TreeNode root) {
        TreeNode currLevel = root;

        while (currLevel != null) {
            TreeNode currNode = currLevel;

            while (currNode != null) {
                System.out.print(currNode.val + " → ");
                currNode = currNode.next;
            }

            System.out.println("-1");
            currLevel = currLevel.left;
        }
    }

    public static void main(String[] args) {
        // Construct the binary tree
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);
        root.right.left = new TreeNode(6);
        root.right.right = new TreeNode(7);

        // Connect nodes at the same level
        connect(root);

        // Print the level order traversal with next pointers
        printLevelOrderTraversal(root);
    }
}
```

Q4.
```java
class TreeNode {
    int val;
    TreeNode left, right;

    public TreeNode(int val) {
        this.val = val;
        this.left = null;
        this.right = null;
    }
}

public class DistanceBetweenNodesBST {
    private static TreeNode findLCA(TreeNode root, int node1, int node2) {
        if (root == null)
            return null;

        if (root.val > node1 && root.val > node2)
            return findLCA(root.left, node1, node2);

        if (root.val < node1 && root.val < node2)
            return findLCA(root.right, node1, node2);

        return root;
    }

    private static int findDistance(TreeNode root, int node, int distance) {
        if (root == null)
            return -1;

        if (root.val == node)
            return distance;

        if (root.val > node)
            return findDistance(root.left, node, distance + 1);

        return findDistance(root.right, node, distance + 1);
    }

    public static int findDistanceBetweenNodes(TreeNode root, int node1, int node2) {
        TreeNode lca = findLCA(root, node1, node2);

        int distance1 = findDistance(lca, node1, 0);
        int distance2 = findDistance(lca, node2, 0);

        return distance1 + distance2;
    }

    public static void main(String[] args) {
        // Construct the binary search tree
        TreeNode root = new TreeNode(8);
        root.left = new TreeNode(3);
        root.right = new TreeNode(10);
        root.left.left = new TreeNode(1);
        root.left.right = new TreeNode(6);
        root.left.right.left = new TreeNode(4);
        root.left.right.right = new TreeNode(7);
        root.right.right = new TreeNode(14);
        root.right.right.left = new TreeNode(13);

        int node1 = 6;
        int node2 = 14;

        int distance = findDistanceBetweenNodes(root, node1, node2);

        System.out.println("The distance between the two keys = " + distance);
    }
}
```
