<a href="https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/"> See the problem on leetcode </a>
<details>
   <summary>Description</summary>
<div class="content__u3I1 question-content__JfgR"><div><p>Given a sorted array <em>nums</em>, remove the duplicates <a href="https://en.wikipedia.org/wiki/In-place_algorithm" target="_blank"><strong>in-place</strong></a> such that duplicates appeared at most&nbsp;<em>twice</em> and return the new length.</p>

<p>Do not allocate extra space for another array; you must do this by <strong>modifying the input array <a href="https://en.wikipedia.org/wiki/In-place_algorithm" target="_blank">in-place</a></strong> with O(1) extra memory.</p>

<p><strong>Clarification:</strong></p>

<p>Confused why the returned value is an integer, but your answer is an array?</p>

<p>Note that the input array is passed in by <strong>reference</strong>, which means a modification to the input array will be known to the caller.</p>

<p>Internally you can think of this:</p>

<pre>// <strong>nums</strong> is passed in by reference. (i.e., without making a copy)
int len = removeDuplicates(nums);

// any modification to <strong>nums</strong> in your function would be known by the caller.
// using the length returned by your function, it prints the first <strong>len</strong> elements.
for (int i = 0; i &lt; len; i++) {
&nbsp; &nbsp; print(nums[i]);
}
</pre>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,1,1,2,2,3]
<strong>Output:</strong> 5, nums = [1,1,2,2,3]
<strong>Explanation:</strong> Your function should return length = <strong><code>5</code></strong>, with the first five elements of <em><code>nums</code></em> being <strong><code>1, 1, 2, 2</code></strong> and <strong>3</strong> respectively. It doesn't matter what you leave beyond the returned length.
</pre>

<p><strong>Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [0,0,1,1,1,1,2,3,3]
<strong>Output:</strong> 7, nums = [0,0,1,1,2,3,3]
<strong>Explanation:</strong> Your function should return length = <strong><code>7</code></strong>, with the first seven elements of <em><code>nums</code></em> being modified to&nbsp;<strong><code>0</code></strong>, <strong>0</strong>, <strong>1</strong>, <strong>1</strong>, <strong>2</strong>, <strong>3</strong> and&nbsp;<strong>3</strong> respectively. It doesn't matter what values are set beyond&nbsp;the returned length.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= nums.length &lt;= 3 * 10<sup>4</sup></code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
	<li><code>nums</code>&nbsp;is sorted in ascending order.</li>
</ul>
</div></div>
</details>

<details>
<summary>Solution</summary>
	
```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int end = 0;
        for(int i = 1; i < nums.length; i++){
            if (nums[i] == nums[i-1] && end == 0){
                end = i+1;
                while(i < nums.length - 1 && nums[i] == nums[i+1])
                    i++;
            }
            else if(nums[i] > nums[i-1] && end != 0){
                if(i < nums.length - 1 && nums[i] != nums[i+1]){
                    swap(nums, i, end);
                    end++;
                }
                else{
                    int j = i;
                    while(i < nums.length - 1 && nums[i] == nums[i+1])
                        i++;
                    swap (nums, j, end);
                    end ++;
                    if (j+1 < nums.length){
                        swap(nums, j+1, end);
                        end++;
                    }
                }
            }
        }
        return end == 0? nums.length: end;
    }
    public void swap(int []nums, int i, int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
    // oh, by reference. If you wanted by value
    // https://stackoverflow.com/questions/28003275/is-it-possible-to-pass-array-by-value-in-java-instead-of-reference
        
    //also this:
    //https://stackoverflow.com/questions/14062118/pass-array-by-reference-in-java
}
```
</details>

<details>
    <summary>A word about the solution</Summary>
There's neater solutions, for example <a href='https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/discuss/?currentPage=1&orderBy=most_relevant&query=general'> these.</a> 
Also solved <a href='https://leetcode.com/problems/remove-duplicates-from-sorted-array/submissions/'> this.</a> <br>
Then there's <a href='https://leetcode.com/problems/remove-duplicates-from-sorted-array/discuss/259484/Generalized-solution-with-explanation-in-C%2B%2B-and-Java'> this link </a> which is 
really really good. I'm actually just gonna paste the content here anyway.

```java
class Solution {
public:
    int removeDuplicates(vector<int>& nums, int k) {
        int i = 0;
        for (int num : nums) {
            if (i < k || num > nums[i - k]) {
                nums[i++] = num;
            }
        }
        return i;
    }
}
```
<p></p><p>which will work as below</p><p>
</p><pre><code>nums[] = [<span class="hljs-number">0</span>,<span class="hljs-number">0</span>,<span class="hljs-number">1</span>,<span class="hljs-number">1</span>,<span class="hljs-number">1</span>,<span class="hljs-number">2</span>]  k = <span class="hljs-number">1</span>

initialized i=<span class="hljs-number">0</span>

<span class="hljs-keyword">for</span> every element <span class="hljs-keyword">in</span> array
	nums[<span class="hljs-number">0</span>]-&gt; num=<span class="hljs-number">0</span> =&gt; <span class="hljs-number">0</span>&lt;<span class="hljs-number">1</span>   (i&lt;k) 
							nums[<span class="hljs-number">0</span>]=<span class="hljs-number">0</span>      |-------&gt;         nums[i++]=num
							i=<span class="hljs-number">1</span>            |-----------------------^
nums[] = [<span class="hljs-number">0</span>,<span class="hljs-number">0</span>,<span class="hljs-number">1</span>,<span class="hljs-number">1</span>,<span class="hljs-number">1</span>,<span class="hljs-number">2</span>]
	nums[<span class="hljs-number">1</span>]-&gt; num=<span class="hljs-number">0</span> =&gt; !(<span class="hljs-number">1</span>&lt;<span class="hljs-number">1</span>)   !(i&lt;k)   and !(<span class="hljs-number">0</span>&gt;<span class="hljs-number">0</span>)  !(num[<span class="hljs-number">1</span>] &gt; num(<span class="hljs-number">1</span>-<span class="hljs-number">1</span>)
	nums[<span class="hljs-number">2</span>]-&gt; num=<span class="hljs-number">1</span> =&gt; !(<span class="hljs-number">2</span>&lt;<span class="hljs-number">1</span>)   !(i&lt;k)   but (<span class="hljs-number">1</span>&gt;<span class="hljs-number">0</span>)  (num[<span class="hljs-number">2</span>] &gt; num(<span class="hljs-number">1</span>-<span class="hljs-number">1</span>)
							nums[<span class="hljs-number">1</span>]=<span class="hljs-number">1</span>      |-------&gt;         nums[i++]=num
							i=<span class="hljs-number">2</span>            |-----------------------^
nums[] = [<span class="hljs-number">0</span>,<span class="hljs-number">1</span>,<span class="hljs-number">1</span>,<span class="hljs-number">1</span>,<span class="hljs-number">1</span>,<span class="hljs-number">2</span>]
	nums[<span class="hljs-number">3</span>]-&gt; num=<span class="hljs-number">1</span> =&gt; !(<span class="hljs-number">3</span>&lt;<span class="hljs-number">2</span>)   !(i&lt;k)  and !(<span class="hljs-number">1</span>&gt;<span class="hljs-number">1</span>)  !(num[<span class="hljs-number">3</span>] &gt; num(<span class="hljs-number">2</span>-<span class="hljs-number">1</span>) 
	nums[<span class="hljs-number">4</span>]-&gt; num=<span class="hljs-number">1</span> =&gt; !(<span class="hljs-number">4</span>&lt;<span class="hljs-number">2</span>)   !(i&lt;k)  and !(<span class="hljs-number">1</span>&gt;<span class="hljs-number">1</span>)  !(num[<span class="hljs-number">4</span>] &gt; num(<span class="hljs-number">2</span>-<span class="hljs-number">1</span>) 
	nums[<span class="hljs-number">5</span>]-&gt; num=<span class="hljs-number">2</span> =&gt; !(<span class="hljs-number">5</span>&lt;<span class="hljs-number">2</span>)   !(i&lt;k)  but !(<span class="hljs-number">2</span>&gt;<span class="hljs-number">1</span>)  !(num[<span class="hljs-number">5</span>] &gt; num(<span class="hljs-number">2</span>-<span class="hljs-number">1</span>) 
							nums[<span class="hljs-number">2</span>]=<span class="hljs-number">2</span>      |-------&gt;         nums[i++]=num
							i=<span class="hljs-number">3</span>            |-----------------------^										
nums[] = [<span class="hljs-number">0</span>,<span class="hljs-number">1</span>,<span class="hljs-number">2</span>,<span class="hljs-number">1</span>,<span class="hljs-number">1</span>,<span class="hljs-number">2</span>]
</code></pre>
<p></p><p>so here in this problem we can use k as an static value by taking k=2 by default<br>
<strong>C++</strong></p><p>
</p><pre><code><span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">Solution</span> {</span>
<span class="hljs-keyword">public</span>:
    <span class="hljs-function"><span class="hljs-keyword">int</span> <span class="hljs-title">removeDuplicates</span><span class="hljs-params">(<span class="hljs-built_in">vector</span>&lt;<span class="hljs-keyword">int</span>&gt;&amp; nums)</span> </span>{
        <span class="hljs-keyword">int</span> i = <span class="hljs-number">0</span>;
        <span class="hljs-keyword">for</span> (<span class="hljs-keyword">int</span> num : nums) {
            <span class="hljs-keyword">if</span> (i &lt; <span class="hljs-number">1</span> || num &gt; nums[i - <span class="hljs-number">1</span>]) {
                nums[i++] = num;
            }
        }
        <span class="hljs-keyword">return</span> i;
    }
};
</code></pre>
<p></p><p><strong>JAVA</strong></p><p>
</p><pre><code><span class="hljs-class"><span class="hljs-keyword">class</span> <span class="hljs-title">Solution</span> {</span>
    <span class="hljs-function"><span class="hljs-keyword">public</span> <span class="hljs-keyword">int</span> <span class="hljs-title">removeDuplicates</span><span class="hljs-params">(<span class="hljs-keyword">int</span>[] nums)</span> </span>{
    <span class="hljs-keyword">int</span> i = <span class="hljs-number">0</span>;
    <span class="hljs-keyword">for</span> (<span class="hljs-keyword">int</span> n : nums){
        <span class="hljs-keyword">if</span> (i &lt; <span class="hljs-number">1</span> || n &gt; nums[i<span class="hljs-number">-1</span>]){
            nums[i++] = n;
        }
    }
    <span class="hljs-keyword">return</span> i;
    }
}
</code></pre><p></p></div></div><div class="tag-list-container__2cDj"><div class="css-9sdfuf"><span class="css-vh6pmz">c++</span><span class="css-vh6pmz">java</span><span class="css-vh6pmz">explaination</span></div></div></div>
</details>
