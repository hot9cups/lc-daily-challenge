<a href="https://leetcode.com/problems/spiral-matrix-ii/"> See the problem on leetcode </a>
<details>
   <summary>Description</summary>
<div class="content__u3I1 question-content__JfgR"><div><p>Given a positive integer <code>n</code>, generate an <code>n x n</code> <code>matrix</code> filled with elements from <code>1</code> to <code>n<sup>2</sup></code> in spiral order.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg" style="width: 242px; height: 242px;">
<pre><strong>Input:</strong> n = 3
<strong>Output:</strong> [[1,2,3],[8,9,4],[7,6,5]]
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> n = 1
<strong>Output:</strong> [[1]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 20</code></li>
</ul>
</div></div>
</details>

<details>
<summary>Solution</summary>
	
```java
class Solution {
    public int[][] generateMatrix(int n) {
        int [][] matrix = new int[n][n];
        int start = 1, left = 0, right = n-1, up = 0, down = n-1;
        
        while (left <= right && up <= down){
            
            for(int i = left; i <= right; i++)
                matrix[up][i] = start++;
            
            for(int i = up+1; i <= down; i++)
                matrix[i][right] = start++;
            
            for(int i = right-1; i >= left; i--)
                matrix[down][i] = start++;
            
            for(int i = down-1; i > up; i--)
                matrix[i][left] = start++;
            
            right--;
            down--;
            left++;
            up++;           
        }
        return matrix;
    }
}
```

</details>

<details>
    <summary>A word about the solution</Summary>
    Well I explained the solution <a href = 'https://leetcode.com/problems/spiral-matrix-ii/discuss/963134/Java-solution-with-explanation-can-be-extended-to-non-square-matrices.-Beats-100'>here.</a>
    <br> There's also <a href='https://leetcode.com/problems/spiral-matrix/'>Spiral Matrix 1</a>, that needed a very slight modification and I can't be arsed at the moment to refactor beyond what I have now. Anyway, the solution for part 1 is as follows:
    
```java
class Solution {
    public List<Integer> spiralOrder(int[][] matrix) {
        ArrayList<Integer> nums = new ArrayList<Integer>();
        int left = 0, up = 0;
        int right = matrix[0].length-1, down = matrix.length-1;
        
        while(left <= right && up <= down){
            for(int i = left; i <= right;i++)
                nums.add(matrix[up][i]);
            for(int i = up + 1; i <= down;i++)
                nums.add(matrix[i][right]);
            for(int i = right - 1; i >= left;i--)
                nums.add(matrix[down][i]);
            for(int i = down - 1; i > up;i--)
                nums.add(matrix[i][left]);
            left++; down--; up++; right--;
        }
        while(nums.size() != matrix[0].length * matrix.length)
            nums.remove(nums.size()-1);
        return nums;
    }
}
```

Then there's also <a href = 'https://leetcode.com/problems/spiral-matrix-iii/'>Spiral Matrix 3</a>, maybe I'll edit this post tomorrow and post the solution for that as well.



</details>
