<a href="https://leetcode.com/problems/the-kth-factor-of-n/"> See the problem on leetcode </a>
<details>
   <summary>Description</summary>
   <div class="content__u3I1 question-content__JfgR"><div><p>Given two positive integers <code>n</code> and <code>k</code>.</p>

<p>A factor of an integer <code>n</code> is defined as an integer <code>i</code> where <code>n % i == 0</code>.</p>

<p>Consider a list of all factors of <code>n</code>&nbsp;sorted in <strong>ascending order</strong>, return <em>the </em><code>kth</code><em> factor</em> in this list or return <strong>-1</strong> if <code>n</code> has less than&nbsp;<code>k</code> factors.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> n = 12, k = 3
<strong>Output:</strong> 3
<strong>Explanation:</strong> Factors list is [1, 2, 3, 4, 6, 12], the 3rd factor is 3.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> n = 7, k = 2
<strong>Output:</strong> 7
<strong>Explanation:</strong> Factors list is [1, 7], the 2nd factor is 7.
</pre>

<p><strong>Example 3:</strong></p>

<pre><strong>Input:</strong> n = 4, k = 4
<strong>Output:</strong> -1
<strong>Explanation:</strong> Factors list is [1, 2, 4], there is only 3 factors. We should return -1.
</pre>

<p><strong>Example 4:</strong></p>

<pre><strong>Input:</strong> n = 1, k = 1
<strong>Output:</strong> 1
<strong>Explanation:</strong> Factors list is [1], the 1st factor is 1.
</pre>

<p><strong>Example 5:</strong></p>

<pre><strong>Input:</strong> n = 1000, k = 3
<strong>Output:</strong> 4
<strong>Explanation:</strong> Factors list is [1, 2, 4, 5, 8, 10, 20, 25, 40, 50, 100, 125, 200, 250, 500, 1000].
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= k &lt;= n &lt;= 1000</code></li>
</ul></div></div>
</details>

<details>
<summary>Solution</summary>
	
```java
class Solution {
    public int kthFactor(int n, int k){
        ArrayList<Integer> factors_low = new ArrayList<>();
        ArrayList<Integer> factors_high = new ArrayList<>();
        
        for(int i = 1; i <= (int)Math.sqrt(n); i++){
            if(n%i == 0) {
                factors_low.add(i); // sorted asc
                factors_high.add(n/i); // sorted desc
            }
        }
        int low_size = factors_low.size();
        int high_size = factors_high.size();
        
        if(factors_low.get(low_size - 1) == factors_high.get(high_size - 1)){
            factors_high.remove(high_size - 1);
            high_size--;
        }

        if(k <= low_size) 
            return factors_low.get(k-1);
        if((k-low_size) <= high_size) 
            return factors_high.get(high_size-(k-low_size)); //cuz desc
        return -1;
    }
}
```

</details>

<details>
    <summary>A word about the solution</Summary>
    The solution above is O(sqrt(N)). Apparently the O(N) trivial solution gives a better runtime on leetcode, which I suppose could be because of the small inputs, 
    but also because there's no arraylists being created, no new objects. So I'll post the O(N) solution here too

```java
class Solution {
    public int kthFactor(int n, int k) {
        int kth = 0;
        for(int i = 1 ; i <= n; i++){
            if(n%i == 0)
                kth++;
            if(kth == k)
                return i;
        }
        return -1;
    }
}
```
<a href='https://leetcode.com/problems/the-kth-factor-of-n/discuss/959365/Python-O(sqrt(n))-solution-explained'>This post</a> also has a good explanation about the O(sqrt(N)) idea, so might as well link it here.
</details>
