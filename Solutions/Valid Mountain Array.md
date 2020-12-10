<a href="https://leetcode.com/problems/valid-mountain-array/"> See the problem on leetcode </a>
<details>
   <summary>Description</summary>
<div class="content__u3I1 question-content__JfgR"><div><p>Given an array of integers&nbsp;<code>arr</code>, return <em><code>true</code> if and only if it is a valid mountain array</em>.</p>

<p>Recall that arr is a mountain array if and only if:</p>

<ul>
	<li><code>arr.length &gt;= 3</code></li>
	<li>There exists some <code>i</code> with&nbsp;<code>0 &lt; i&nbsp;&lt; arr.length - 1</code>&nbsp;such that:
	<ul>
		<li><code>arr[0] &lt; arr[1] &lt; ... &lt; arr[i - 1] &lt; A[i] </code></li>
		<li><code>arr[i] &gt; arr[i + 1] &gt; ... &gt; arr[arr.length - 1]</code></li>
	</ul>
	</li>
</ul>
<img src="https://assets.leetcode.com/uploads/2019/10/20/hint_valid_mountain_array.png" width="500">
<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> arr = [2,1]
<strong>Output:</strong> false
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> arr = [3,5,5]
<strong>Output:</strong> false
</pre><p><strong>Example 3:</strong></p>
<pre><strong>Input:</strong> arr = [0,3,2,1]
<strong>Output:</strong> true
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= arr.length &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= arr[i] &lt;= 10<sup>4</sup></code></li>
</ul>
</div></div>
</details>

<details>
<summary>Solution</summary>
	
```java
class Solution {
    public boolean validMountainArray(int[] arr) {
        if (arr.length < 3) return false;
        boolean flipped = false;
        for(int i = 1; i < arr.length; i++){
            if (!flipped){
                if (arr[i] - arr[i - 1] < 0 && i != 1)
                    flipped = true;
                else if (arr[i] - arr[i-1] > 0)
                    continue;
                else
                    return false;
            }
            else{
                if (arr[i] - arr[i-1] >= 0)
                    return false;
            }
        }
        return flipped;
    }
}
```

</details>

<details>
    <summary>A word about the solution</Summary>
Easy question. Merely simulation.
</details>
