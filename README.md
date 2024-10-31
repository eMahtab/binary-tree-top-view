# Binary Tree Top View
### https://www.hackerrank.com/challenges/tree-top-view/problem

Given a pointer to the root of a binary tree, print the top view of the binary tree.

The tree as seen from the top the nodes, is called the top view of the tree.

```
For example :

   1
    \
     2
      \
       5
      /  \
     3    6
      \
       4
```
Top View : 1, 2, 5, 6

Complete the function  and print the resulting values on a single line separated by space.

## Implementation :
```java
class Solution {

	/* 
    
    class Node 
    	int data;
    	Node left;
    	Node right;
	*/
    class TreeNode {
        Node node;
        int col;
        TreeNode(Node node, int col){
            this.node = node;
            this.col = col;
        }
    }

   public static void topView(Node root) {
      Map<Integer,Node> map = new HashMap<>();
      Queue<TreeNode> queue = new LinkedList<>();
      int leftmostCol = Integer.MAX_VALUE;
      int rightmostCol = Integer.MIN_VALUE;
      queue.add(new TreeNode(root, 0));
      while(!queue.isEmpty()) {
          int size = queue.size();
          for(int i = 1; i <= size; i++) {
              TreeNode treeNode = queue.remove();
              int column = treeNode.col;
              leftmostCol = Math.min(leftmostCol, column);
              rightmostCol = Math.max(rightmostCol, column);
              map.putIfAbsent(column, treeNode.node);
              if(treeNode.node.left != null)
                  queue.add(new TreeNode(treeNode.node.left, column -1 ));
              if(treeNode.node.right != null)
                  queue.add(new TreeNode(treeNode.node.right, column +1));    
          }
      }
      for(int column = leftmostCol; column <= rightmostCol; column++) {
          System.out.print(map.get(column).data + " ");
      }
   }
}
```
