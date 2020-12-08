<a href="https://leetcode.com/problems/pairs-of-songs-with-total-durations-divisible-by-60/"> See the problem on leetcode </a>
<details>
   <summary>Description</summary>
<div class="content__u3I1 question-content__JfgR"><div><p>You are given a list of songs where the i<sup>th</sup> song has a duration of <code>time[i]</code> seconds.</p>

<p>Return <em>the number of pairs of songs for which their total duration in seconds is divisible by</em> <code>60</code>. Formally, we want the number of indices <code>i</code>, <code>j</code> such that <code>i &lt; j</code> with <code>(time[i] + time[j]) % 60 == 0</code>.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> time = [30,20,150,100,40]
<strong>Output:</strong> 3
<strong>Explanation:</strong> Three pairs have a total duration divisible by 60:
(time[0] = 30, time[2] = 150): total duration 180
(time[1] = 20, time[3] = 100): total duration 120
(time[1] = 20, time[4] = 40): total duration 60
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> time = [60,60,60]
<strong>Output:</strong> 3
<strong>Explanation:</strong> All three pairs have a total duration of 120, which is divisible by 60.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= time.length &lt;= 6 * 10<sup>4</sup></code></li>
	<li><code>1 &lt;= time[i] &lt;= 500</code></li>
</ul>
</div></div>
</details>

<details>
<summary>Solution</summary>
	
```java
class Solution {
    public int numPairsDivisibleBy60(int[] times) {
        int [] modTimes = new int[60];
        for(int songTime : times)
            modTimes[songTime%60]++;

        int totalPairs = findPairs(modTimes[0]) + findPairs(modTimes[30]);
        for(int i = 1; i < 30; i++)
            totalPairs += modTimes[i] * modTimes[60-i];
        
        return totalPairs;
    }
    
    public int findPairs(int n){
        return n * (n-1)/2;
    }
}
```

</details>

<details>
    <summary>A word about the solution</Summary>
Well I explained the solution <a href = 'https://leetcode.com/problems/pairs-of-songs-with-total-durations-divisible-by-60/discuss/964331/Java-Simple-Code-with-Explanation-beats-99.86'>here.</a>
While I was at it, I also ended up solving 
<a href = 'https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/submissions/'> this </a> and 
<a href= 'https://leetcode.com/problems/flipping-an-image/submissions/'> this </a> and 
<a href= 'https://leetcode.com/problems/maximum-product-of-three-numbers/submissions/'> this.</a>
</details>
