Q1.
```java
public class BinaryTreeDepth {
    public static int calculateDepth(String preorder) {
        int depth = 0;
        int maxDepth = 0;

        for (char c : preorder.toCharArray()) {
            if (c == 'n') {
                depth++;
                maxDepth = Math.max(maxDepth, depth);
            } else if (c == 'l') {
                depth--;
            }
        }

        return maxDepth;
    }

    public static void main(String[] args) {
        String preorder = "nlnll";
        int depth = calculateDepth(preorder);
        System.out.println("Depth: " + depth);
    }
}
```

Q2.
```java
import java.util.*;

class TreeNode {
    int val;
    int hd; // horizontal distance
    TreeNode left, right;

    public TreeNode(int val) {
        this.val = val;
        this.hd = Integer.MAX_VALUE;
        this.left = null;
        this.right = null;
    }
}

public class BottomViewBinaryTree {
    public static void printBottomView(TreeNode root) {
        if (root == null)
            return;

        TreeMap<Integer, Integer> map = new TreeMap<>();
        Queue<TreeNode> queue = new LinkedList<>();
        root.hd = 0;
        queue.add(root);

        while (!queue.isEmpty()) {
            TreeNode current = queue.poll();
            int hd = current.hd;

            // Update the value for the current horizontal distance
            map.put(hd, current.val);

            if (current.left != null) {
                current.left.hd = hd - 1;
                queue.add(current.left);
            }

            if (current.right != null) {
                current.right.hd = hd + 1;
                queue.add(current.right);
            }
        }

        // Print the nodes from left to right
        for (int value : map.values()) {
            System.out.print(value + " ");
        }
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(20);
        root.left = new TreeNode(8);
        root.right = new TreeNode(22);
        root.left.left = new TreeNode(5);
        root.left.right = new TreeNode(3);
        root.right.right = new TreeNode(25);
        root.left.right.left = new TreeNode(10);
        root.left.right.right = new TreeNode(14);

        printBottomView(root);
    }
}
```

Q3.
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

public class LeftViewBinaryTree {
    public static void printLeftView(TreeNode root) {
        if (root == null)
            return;

        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);

        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            boolean isFirstNode = true;

            for (int i = 0; i < levelSize; i++) {
                TreeNode current = queue.poll();

                if (isFirstNode) {
                    System.out.print(current.val + " ");
                    isFirstNode = false;
                }

                if (current.left != null)
                    queue.add(current.left);

                if (current.right != null)
                    queue.add(current.right);
            }
        }
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(4);
        root.left = new TreeNode(5);
        root.right = new TreeNode(2);
        root.right.left = new TreeNode(3);
        root.right.right = new TreeNode(1);
        root.right.left.left = new TreeNode(6);
        root.right.left.right = new TreeNode(7);

        printLeftView(root);
    }
}
```

Q4.
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

public class RightViewBinaryTree {
    public static void printRightView(TreeNode root) {
        if (root == null)
            return;

        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);

        while (!queue.isEmpty()) {
            int levelSize = queue.size();

            for (int i = 0; i < levelSize; i++) {
                TreeNode current = queue.poll();

                if (i == levelSize - 1) {
                    System.out.print(current.val + " ");
                }

                if (current.left != null)
                    queue.add(current.left);

                if (current.right != null)
                    queue.add(current.right);
            }
        }
    }

    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.left = new TreeNode(2);
        root.right = new TreeNode(3);
        root.left.left = new TreeNode(4);
        root.left.right = new TreeNode(5);
        root.right.left = new TreeNode(6);
        root.right.right = new TreeNode(7);
        root.right.right.right = new TreeNode(8);

        printRightView(root);
    }
}
```

