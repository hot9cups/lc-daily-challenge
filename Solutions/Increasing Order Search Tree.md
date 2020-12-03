<a href="https://leetcode.com/problems/increasing-order-search-tree/"> See the problem on leetcode </a>
<details>
   <summary>Description</summary>
   <div class="content__u3I1 question-content__JfgR">
      <div>
         <p>Given the <code>root</code> of a binary search tree, rearrange the tree in <strong>in-order</strong> so that the leftmost node in the tree is now the root of the tree, and every node has no left child and only one right child.</p>
         <p>&nbsp;</p>
         <p><strong>Example 1:</strong></p>
         <img alt="" src="https://assets.leetcode.com/uploads/2020/11/17/ex1.jpg" style="width: 600px; height: 350px;">
         <pre><strong>Input:</strong> root = [5,3,6,2,4,null,8,1,null,null,null,7,9]
<strong>Output:</strong> [1,null,2,null,3,null,4,null,5,null,6,null,7,null,8,null,9]
</pre>
         <p><strong>Example 2:</strong></p>
         <img alt="" src="https://assets.leetcode.com/uploads/2020/11/17/ex2.jpg" style="width: 300px; height: 114px;">
         <pre><strong>Input:</strong> root = [5,1,7]
<strong>Output:</strong> [1,null,5,null,7]
</pre>
         <p>&nbsp;</p>
         <p><strong>Constraints:</strong></p>
         <ul>
            <li>The number of nodes in the given tree will be in the range <code>[1, 100]</code>.</li>
            <li><code>0 &lt;= Node.val &lt;= 1000</code></li>
         </ul>
      </div>
   </div>
</details>

<details>
<summary>Solution</summary>
	
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    TreeNode head, temp;
    public TreeNode increasingBST(TreeNode root) {
        reArrange(root);
        return temp;
    }
    public void reArrange(TreeNode root){
        if(root == null)
            return;
        reArrange(root.left);
        if(head == null){
            head = root;
            temp = root;
        }
        else{
            head.right = new TreeNode(root.val);
            head = head.right;
        }
        reArrange(root.right);
    }
}
```

</details>

<details>
    <summary>A word about the solution</Summary>
    The part where I tripped up was realising I needed to do <code>head.right = new TreeNode(root.val)</code> instead of <code>head.right = root</code> since root(root refers to a general node here) would still have its left and right subtrees. The official solution though does take that route(no pun intended) by cutting off the left links of the node. Check <a href = 'https://leetcode.com/problems/increasing-order-search-tree/solution/'>this</a>
</details>
