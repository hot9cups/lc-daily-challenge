<a href="https://leetcode.com/problems/maximum-depth-of-binary-tree/"> See the problem on leetcode </a>
<details>
   <summary>Description</summary>
   <div class="content__u3I1 question-content__JfgR">
      <div>
         <p>Given the <code>root</code> of a binary tree, return <em>its maximum depth</em>.</p>
         <p>A binary tree's <strong>maximum depth</strong>&nbsp;is the number of nodes along the longest path from the root node down to the farthest leaf node.</p>
         <p>&nbsp;</p>
         <p><strong>Example 1:</strong></p>
         <img alt="" src="https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg" style="width: 400px; height: 277px;">
         <pre><strong>Input:</strong> root = [3,9,20,null,null,15,7]
<strong>Output:</strong> 3
</pre>
         <p><strong>Example 2:</strong></p>
         <pre><strong>Input:</strong> root = [1,null,2]
<strong>Output:</strong> 2
</pre>
         <p><strong>Example 3:</strong></p>
         <pre><strong>Input:</strong> root = []
<strong>Output:</strong> 0
</pre>
         <p><strong>Example 4:</strong></p>
         <pre><strong>Input:</strong> root = [0]
<strong>Output:</strong> 1
</pre>
         <p>&nbsp;</p>
         <p><strong>Constraints:</strong></p>
         <ul>
            <li>The number of nodes in the tree is in the range <code>[0, 10<sup>4</sup>]</code>.</li>
            <li><code>-100 &lt;= Node.val &lt;= 100</code></li>
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
    int depth = 0;
    public int maxDepth(TreeNode root) {
        calcDepth(root, 1);
        return depth;
    }
    
    public void calcDepth(TreeNode root, int curDepth){
        if(root == null)
            return;
        calcDepth(root.left, curDepth + 1);
        calcDepth(root.right, curDepth + 1);
        depth = Math.max(curDepth, depth);
    }
}
```

</details>

<details>
    <summary>A word about the solution</Summary>
    Recursively calculate left subtree's depth, right subtree's depth and update depth accordingly.
</details>













