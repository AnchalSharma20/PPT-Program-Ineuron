Q1.
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

public class BinaryTreeToDLL {
    private static TreeNode prevNode;

    private static void convertToDLL(TreeNode root) {
        if (root == null)
            return;

        convertToDLL(root.left);

        DoublyLinkedListNode curr = new DoublyLinkedListNode(root.val);

        if (prevNode != null) {
            prevNode.next = curr;
            curr.prev = prevNode;
        } else {
            prevNode = curr;
        }

        prevNode = curr;

        convertToDLL(root.right);
    }

    public static DoublyLinkedListNode convertBinaryTreeToDLL(TreeNode root) {
        if (root == null)
            return null;

        prevNode = null;

        convertToDLL(root);

        DoublyLinkedListNode head = prevNode;

        while (head != null && head.prev != null) {
            head = head.prev;
        }

        return head;
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
        root.left = new TreeNode(12);
        root.right = new TreeNode(15);
        root.left.left = new TreeNode(25);
        root.left.right = new TreeNode(30);
        root.right.left = new TreeNode(36);

        // Convert binary tree to DLL
        DoublyLinkedListNode head = convertBinaryTreeToDLL(root);

        // Print the doubly linked list
        printDLL(head);
    }
}
```

Q2.
```java
import java.util.Arrays;

public class CheckSameTree {
    public static boolean isSameTree(int[] inorder, int[] preorder, int[] postorder) {
        if (inorder.length == 0)
            return true;

        if (inorder.length == 1)
            return (preorder[0] == inorder[0] && postorder[0] == inorder[0]);

        int root = preorder[0];
        int rootIndex = -1;

        for (int i = 0; i < inorder.length; i++) {
            if (inorder[i] == root) {
                rootIndex = i;
                break;
            }
        }

        if (rootIndex == -1)
            return false;

        int[] leftInorder = Arrays.copyOfRange(inorder, 0, rootIndex);
        int[] rightInorder = Arrays.copyOfRange(inorder, rootIndex + 1, inorder.length);

        int[] leftPreorder = Arrays.copyOfRange(preorder, 1, rootIndex + 1);
        int[] rightPreorder = Arrays.copyOfRange(preorder, rootIndex + 1, preorder.length);

        int[] leftPostorder = Arrays.copyOfRange(postorder, 0, rootIndex);
        int[] rightPostorder = Arrays.copyOfRange(postorder, rootIndex, postorder.length - 1);

        boolean isLeftSame = isSameTree(leftInorder, leftPreorder, leftPostorder);
        boolean isRightSame = isSameTree(rightInorder, rightPreorder, rightPostorder);

        return isLeftSame && isRightSame;
    }

    public static void main(String[] args) {
        int[] inorder = { 4, 2, 5, 1, 3 };
        int[] preorder = { 1, 2, 4, 5, 3 };
        int[] postorder = { 4, 5, 2, 3, 1 };

        boolean result = isSameTree(inorder, preorder, postorder);

        System.out.println(result ? "Yes" : "No");
    }
}
```

Q3.
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

public class FlipBinaryTree {
    public static TreeNode flipBinaryTree(TreeNode root) {
        if (root == null || (root.left == null && root.right == null))
            return root;

        TreeNode flippedRoot = flipBinaryTree(root.left);

        root.left.left = root.right;
        root.left.right = root;
        root.left = null;
        root.right = null;

        return flippedRoot;
    }

    public static void printInorder(TreeNode root) {
        if (root != null) {
            printInorder(root.left);
            System.out.print(root.val + " ");
            printInorder(root.right);
        }
    }

    public static void main(String[] args) {
        // Construct the binary tree
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.right.left = new TreeNode(4);
        root.right.right = new TreeNode(5);

        // Flip the binary tree
        TreeNode flippedRoot = flipBinaryTree(root);

        // Print the inorder traversal of the flipped tree
        printInorder(flippedRoot);
    }
}
```

Q4.
```java
import java.util.Stack;

class TreeNode {
    int val;
    TreeNode left, right;

    public TreeNode(int val) {
        this.val = val;
        this.left = null;
        this.right = null;
    }
}

public class RootToLeafPaths {
    public static void printRootToLeafPaths(TreeNode root) {
        if (root == null)
            return;

        Stack<TreeNode> nodeStack = new Stack<>();
        Stack<String> pathStack = new Stack<>();

        nodeStack.push(root);
        pathStack.push(Integer.toString(root.val));

        while (!nodeStack.isEmpty()) {
            TreeNode currNode = nodeStack.pop();
            String currPath = pathStack.pop();

            if (currNode.left == null && currNode.right == null) {
                System.out.println(currPath);
            }

            if (currNode.right != null) {
                nodeStack.push(currNode.right);
                pathStack.push(currPath + "->" + currNode.right.val);
            }

            if (currNode.left != null) {
                nodeStack.push(currNode.left);
                pathStack.push(currPath + "->" + currNode.left.val);
            }
        }
    }

    public static void main(String[] args) {
        // Construct the binary tree
        TreeNode root = new TreeNode(6);
        root.left = new TreeNode(3);
        root.right = new TreeNode(5);
        root.left.left = new TreeNode(2);
        root.left.right = new TreeNode(5);
        root.right.right = new TreeNode(4);
        root.left.right.left = new TreeNode(7);
        root.left.right.right = new TreeNode(4);

        // Print the root-to-leaf paths
        printRootToLeafPaths(root);
    }
}
```













