Q1.
```java
class Node {
    int data;
    Node left, right;

    public Node(int item) {
        data = item;
        left = right = null;
    }
}

class BinaryTree {
    Node root;

    int maxSumSubtree(Node node, Sum maxSum) {
        if (node == null)
            return 0;

        int currentSum = node.data + maxSumSubtree(node.left, maxSum) + maxSumSubtree(node.right, maxSum);

        if (currentSum > maxSum.max)
            maxSum.max = currentSum;

        return currentSum;
    }

    int findMaxSumSubtree(Node node) {
        if (node == null)
            return 0;

        Sum maxSum = new Sum();
        maxSum.max = Integer.MIN_VALUE;

        maxSumSubtree(node, maxSum);

        return maxSum.max;
    }

    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        tree.root = new Node(1);
        tree.root.left = new Node(2);
        tree.root.right = new Node(3);
        tree.root.left.left = new Node(4);
        tree.root.left.right = new Node(5);
        tree.root.right.left = new Node(6);
        tree.root.right.right = new Node(7);

        int maxSum = tree.findMaxSumSubtree(tree.root);
        System.out.println("Maximum sum of a subtree in the binary tree: " + maxSum);
    }
}

class Sum {
    int max;
}
```

Q2.
```java
class Node {
    int data;
    Node left, right;

    public Node(int item) {
        data = item;
        left = right = null;
    }
}

class BinaryTree {
    Node root;

    void insertLevelOrder(int[] arr) {
        root = insertLevelOrder(arr, root, 0);
    }

    Node insertLevelOrder(int[] arr, Node root, int index) {
        if (index < arr.length) {
            Node newNode = new Node(arr[index]);
            root = newNode;

            root.left = insertLevelOrder(arr, root.left, 2 * index + 1);
            root.right = insertLevelOrder(arr, root.right, 2 * index + 2);
        }
        return root;
    }

    void inOrderTraversal(Node root) {
        if (root != null) {
            inOrderTraversal(root.left);
            System.out.print(root.data + " ");
            inOrderTraversal(root.right);
        }
    }

    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        int[] arr = {7, 4, 12, 3, 6, 8, 1, 5, 10};

        tree.insertLevelOrder(arr);

        System.out.println("BST:");
        tree.inOrderTraversal(tree.root);
    }
}
```

Q3.
```java
class BinaryTree {
    boolean isLevelOrderBST(int[] arr, int n) {
        if (n == 0)
            return true;

        return isLevelOrderBSTUtil(arr, n, 0, Integer.MIN_VALUE, Integer.MAX_VALUE);
    }

    boolean isLevelOrderBSTUtil(int[] arr, int n, int index, int min, int max) {
        if (index >= n)
            return true;

        if (arr[index] < min || arr[index] > max)
            return false;

        int i;
        for (i = index + 1; i < n; i++) {
            if (arr[i] > arr[index])
                break;
        }

        return isLevelOrderBSTUtil(arr, n, index + 1, min, arr[index] - 1)
                && isLevelOrderBSTUtil(arr, n, i, arr[index] + 1, max);
    }

    public static void main(String[] args) {
        BinaryTree tree = new BinaryTree();
        int[] arr1 = {7, 4, 12, 3, 6, 8, 1, 5, 10};
        int[] arr2 = {11, 6, 13, 5, 12, 10};

        if (tree.isLevelOrderBST(arr1, arr1.length))
            System.out.println("Output1: Yes");
        else
            System.out.println("Output1: No");

        if (tree.isLevelOrderBST(arr2, arr2.length))
            System.out.println("Output2: Yes");
        else
            System.out.println("Output2: No");
    }
}
```











