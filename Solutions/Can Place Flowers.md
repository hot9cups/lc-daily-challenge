<a href="https://leetcode.com/problems/can-place-flowers/"> See the problem on leetcode </a>
<details>
   <summary>Description</summary>
   <div class="content__u3I1 question-content__JfgR"><div><p>You have a long flowerbed in which some of the plots are planted, and some are not. However, flowers cannot be planted in <strong>adjacent</strong> plots.</p>

<p>Given an integer array&nbsp;<code>flowerbed</code>&nbsp;containing <code>0</code>'s and <code>1</code>'s, where <code>0</code> means empty and <code>1</code> means not empty,&nbsp;and an integer <code>n</code>, return <em>if</em> <code>n</code> new flowers can be planted in the <code>flowerbed</code>&nbsp;without violating the no-adjacent-flowers rule.</p>

<p>&nbsp;</p>
<p><strong>Example 1:</strong></p>
<pre><strong>Input:</strong> flowerbed = [1,0,0,0,1], n = 1
<strong>Output:</strong> true
</pre><p><strong>Example 2:</strong></p>
<pre><strong>Input:</strong> flowerbed = [1,0,0,0,1], n = 2
<strong>Output:</strong> false
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= flowerbed.length &lt;= 2 * 10<sup>4</sup></code></li>
	<li><code>flowerbed[i]</code> is <code>0</code> or <code>1</code>.</li>
	<li>There are no two adjacent flowers in <code>flowerbed</code>.</li>
	<li><code>0 &lt;= n &lt;= flowerbed.length</code></li>
</ul>
</div></div>
</details>

<details>
<summary>Solution</summary>
	
```java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        if (flowerbed.length == 1 && n <= 1)
            return flowerbed[0] == 0 || n == 0;
        
        if (flowerbed[0] + flowerbed[1] == 0){
            flowerbed[0] = 1;
            n--;
        }
        
        if (flowerbed[flowerbed.length-1] + flowerbed[flowerbed.length-2] == 0){
                    flowerbed[flowerbed.length-1] = 1;
                    n--;
                }
        
        int idx = 1;
        while(n > 0 && idx < flowerbed.length - 1){
            if(flowerbed[idx-1] + flowerbed[idx] + flowerbed[idx+1] == 0){
                flowerbed[idx] = 1;
                n--;
            }
            idx++;
        }
        return n <= 0;
    }
}
```

</details>

<details>
    <summary>A word about the solution</Summary>
    Well the solution works out, greedy is indeed the way to go here. The official solution had a neater if, I suppose:
	
```java
if (flowerbed[i] == 0 && (i == 0 || flowerbed[i - 1] == 0) && (i == flowerbed.length - 1 || flowerbed[i + 1] == 0)) {
  flowerbed[i++] = 1;
  count++;
}
```
The comments had a clearner version imo:
```java
public boolean canPlaceFlowers(int[] flowerbed, int n) {
  for(int i=0; i<flowerbed.length; i++){
    if(flowerbed[i]==0){
      int previousIndex = i-1>=0? i-1 : 0;
      int nextIndex = i+1<flowerbed.length? i+1: flowerbed.length-1;
      if(flowerbed[previousIndex]==0&&flowerbed[nextIndex]==0){
        n--;
        if(n==0)
          return true;
        flowerbed[i] = 1;
      }
    }
  }
  return n<=0;
}
```
There's an additional optimisation that can be done here, incrementing i by two whenever you can place flower.
Also solutions above modify the original array, it's possible to solve the question without doing so, combined with the optimisation.
IE., everytime you can place a flower, reduce num_flowers_required by 1, and increment idx by 2. Return as soon as num_flowers_required is 0.
</details>
