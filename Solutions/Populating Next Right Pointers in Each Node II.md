<a href="https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/"> See the problem on leetcode </a>
<details>
   <summary>Description</summary>
   <div class="content__u3I1 question-content__JfgR"><div><p>Given a binary tree</p>

<pre>struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
</pre>

<p>Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to <code>NULL</code>.</p>

<p>Initially, all next pointers are set to <code>NULL</code>.</p>

<p>&nbsp;</p>

<p><strong>Follow up:</strong></p>

<ul>
	<li>You may only use constant extra space.</li>
	<li>Recursive approach is fine, you may assume implicit stack space does not count as extra space for this problem.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<p><img alt="" src="https://assets.leetcode.com/uploads/2019/02/15/117_sample.png" style="width: 640px; height: 218px;"></p>

<pre><strong>Input:</strong> root = [1,2,3,4,5,null,7]
<strong>Output:</strong> [1,#,2,3,#,4,5,7,#]
<strong>Explanation: </strong>Given the above binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the given tree is less than <code>6000</code>.</li>
	<li><code>-100&nbsp;&lt;= node.val &lt;= 100</code></li>
</ul>
</div></div>
</details>

<details>
<summary>Solution</summary>
	
```java
/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node next;   

    public Node() {}
    
    public Node(int _val) {
        val = _val;
    }

    public Node(int _val, Node _left, Node _right, Node _next) {
        val = _val;
        left = _left;
        right = _right;
        next = _next;
    }
};
*/

class Solution {
    public Node connect(Node root) {
        formNext(root);
        return root;
    }
    
    public void formNext(Node root){
        if(root == null) return;
        
        if (root.left != null)
            root.left.next = getNext(root, true);
            
        if (root.right != null)
            root.right.next = getNext(root, false);
        
        formNext(root.right);
        formNext(root.left);
    }
    
    public Node getNext(Node root, boolean forLeft){
        if(forLeft && root.right != null)
            return root.right;
        
        Node temp = root.next;
        while(temp != null){
            if (temp.left != null)
                return temp.left;
            else if  (temp.right != null)
                return temp.right;
            temp = temp.next;
        }
        return null;
    }
    
}
```

</details>

<details>
<summary>A word about the solution</Summary>
First off, here's a few test cases which helped while writing the code:

```
[1,2,3,4,5,null,7]
[1,2,3,4,null,null,5]
[1,2,3,4,5,null,6,7,null,null,null,null,8]
[1,2]
[2,1,3,0,7,9,1,2,null,1,0,null,null,8,8,null,null,null,null,7]
[5,2,-2,4,-4,-9,2,7,2,null,-9,-9,null,null,3,null,7,null,null,null,null,null,null,null,3]
```

and their outputs:

```
[1,#,2,3,#,4,5,7,#]
[1,#,2,3,#,4,5,#]
[1,#,2,3,#,4,5,6,#,7,8,#]
[1,#,2,#]
[2,#,1,3,#,0,7,9,1,#,2,1,0,8,8,#,7,#]
[5,#,2,-2,#,4,-4,-9,2,#,7,2,-9,-9,3,#,7,3,#]
```

Their tree visualisations can be checked out from leetcode's 'Run Code - Console section'.<br>
So what the code does is assign the left child of a parent to the right child of the parent if it exists, or to the left/right child of parent's next node, 
or to the left/right child of parent's next's next node, so on.<br>
Then assign the right child to parent's next's left/right child, or to parent's next's next's left/right child, you get the idea.<br>
That's what getNode() does. The additional parameter forLeft is to check if the node we're finding is for the left child; If it is we'd first need to check if
the parent's right node exists, if it does we don't need to look further and can directly assign this to be the next node of the left child.<br>
(Notice this is not required for the right child, it can only have a next node amongst the parent's next's children, or its parent's next's next's children, so on. That part is common
to both left and right childs.)<br><br>
So we start at the root and move down, recursively. There's one more thing to take care of, that we'd need to move down the right subtree first, and then through the left subtree.
This is because when you're in the left subtree and you're trying to find next pointer for a certain node, you might end up searching in the right subtree of the main tree,
but the right subtree wouldn't have been touched yet if we had travelled down the left subtree first, so essentially right subtree's next pointers for every node would still be null
and we wouldn't be able to find the solution. The last 2 inputs I wrote above really helped realise that, would be worth to visualise those 2 inputs on the visualiser and understand it.<br>
Hence the way to recurse through this would be
```
formNext(root.right);
formNext(root.left);
```

Also, interestingly there was an earlier part to the question,<a href = 'https://leetcode.com/problems/populating-next-right-pointers-in-each-node/'>Here.</a>
This one's far easier, it's a perfect binary tree. Since the second part that I solved above was a generalisation of part 1, it turns out pasting in the same code is
Accepted for the question(Beats 100% too just like it did for part 2). That was nice. 
</details>
