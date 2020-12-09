<a href="https://leetcode.com/problems/binary-search-tree-iterator/"> See the problem on leetcode </a>
<details>
   <summary>Description</summary>
<div class="content__u3I1 question-content__JfgR"><div><p>Implement the <code>BSTIterator</code> class that represents an iterator over&nbsp;the <strong><a href="https://en.wikipedia.org/wiki/Tree_traversal#In-order_(LNR)">in-order traversal</a></strong>&nbsp;of&nbsp;a binary search tree (BST):</p>

<ul>
	<li><code>BSTIterator(TreeNode root)</code> Initializes an object of the <code>BSTIterator</code> class. The <code>root</code> of the BST is given as part of the constructor. The pointer should be initialized to a non-existent number smaller than any element in the BST.</li>
	<li><code>boolean hasNext()</code> Returns <code>true</code> if there exists a number in the traversal to the right of the pointer, otherwise returns <code>false</code>.</li>
	<li><code>int next()</code> Moves the pointer to the right, then returns the number at the pointer.</li>
</ul>

<p>Notice that by initializing the pointer to a non-existent smallest number, the first call to <code>next()</code> will return the smallest element in the BST.</p>

<p>You may assume that <code>next()</code>&nbsp;calls will always be valid. That is, there will be at least a next number in the in-order traversal&nbsp;when <code>next()</code>&nbsp;is called.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2018/12/25/bst-tree.png" style="width: 189px; height: 178px;">
<pre><strong>Input</strong>
["BSTIterator", "next", "next", "hasNext", "next", "hasNext", "next", "hasNext", "next", "hasNext"]
[[[7, 3, 15, null, null, 9, 20]], [], [], [], [], [], [], [], [], []]
<strong>Output</strong>
[null, 3, 7, true, 9, true, 15, true, 20, false]

<strong>Explanation</strong>
BSTIterator bSTIterator = new BSTIterator([7, 3, 15, null, null, 9, 20]);
bSTIterator.next();    // return 3
bSTIterator.next();    // return 7
bSTIterator.hasNext(); // return True
bSTIterator.next();    // return 9
bSTIterator.hasNext(); // return True
bSTIterator.next();    // return 15
bSTIterator.hasNext(); // return True
bSTIterator.next();    // return 20
bSTIterator.hasNext(); // return False
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[1, 10<sup>5</sup>]</code>.</li>
	<li><code>0 &lt;= Node.val &lt;= 10<sup>6</sup></code></li>
	<li>At most <code>10<sup>5</sup></code> calls will be made to <code>hasNext</code>, and <code>next</code>.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong></p>

<ul>
	<li>Could you implement <code>next()</code> and <code>hasNext()</code> to run in average <code>O(1)</code> time and use&nbsp;<code>O(h)</code> memory, where <code>h</code> is the height of the tree?</li>
</ul>
</div></div>
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
class BSTIterator {
    static Queue<Integer> queue = new LinkedList<>();

    public BSTIterator(TreeNode root) {
        inorder(root);
    }
    
    private void inorder(TreeNode root){
        if (root == null) return;
        inorder(root.left);
        queue.offer(root.val);
        inorder(root.right);
    }
    
    public int next() {
        return queue.poll();
    }
    
    public boolean hasNext() {
        return !queue.isEmpty();
    }
}

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator obj = new BSTIterator(root);
 * int param_1 = obj.next();
 * boolean param_2 = obj.hasNext();
 */
```

</details>

<details>
    <summary>A word about the solution</Summary>
My solution isn't quite O(h) memory yet, it's only O(N) where N is number of nodes in the tree. There were talks about Controlled Morris Traversal, gotta read up on that.
There was another nice solution, this:
	
```java
You can modify a non-recursive inorder traversal algo to solve the problem. Just separate the loop condition:

LinkedList<TreeNode> stack = new LinkedList<>();
TreeNode node;
public BSTIterator(TreeNode root) {
    node = root;
}
public boolean hasNext() {
    return node != null || !stack.isEmpty();
}
public int next() {
    while (node != null) {
        stack.add(node);
        node = node.left;
    }
    node = stack.removeLast();
    int res = node.val;
    node = node.right;
    return res;
}
And inorder tree traversal now looks like:

while (hasNext()) {
    print(next())
}
```
The solution to the question itself is quite good, will have to give it a good thorough read tomorrow, but essentially what I picked up from a quick skim through was that 
you need to convert the recursive solution to an iterative one, the whys and hows are still a bit fuzzy in my headso will have to read up soon.
</details>
