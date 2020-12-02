<a href="https://leetcode.com/problems/linked-list-random-node/"> See the problem on leetcode </a>
<details>
   <summary>Description</summary>
   <div class="content__u3I1 question-content__JfgR">
      <div>
         <p>Given a singly linked list, return a random node's value from the linked list. Each node must have the <b>same probability</b> of being chosen.</p>
         <p><b>Follow up:</b><br>
            What if the linked list is extremely large and its length is unknown to you? Could you solve this efficiently without using extra space?
         </p>
         <p><b>Example:</b></p>
         <pre>// Init a singly linked list [1,2,3].
ListNode head = new ListNode(1);
head.next = new ListNode(2);
head.next.next = new ListNode(3);
Solution solution = new Solution(head);


// getRandom() should return either 1, 2, or 3 randomly. Each element should have equal probability of returning.
solution.getRandom();
</pre>
         <p></p>
      </div>
   </div>
</details>

<details>
<summary>Solution</summary>
	
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    ArrayList<Integer> nums = new ArrayList<>();

    /** @param head The linked list's head.
        Note that the head is guaranteed to be not null, so it contains at least one node. */
    public Solution(ListNode head) {
        while(head!=null){
            nums.add(head.val);
            head = head.next;
        }
    }
    
    /** Returns a random node's value. */
    public int getRandom() {
        int idx = new Random().nextInt(nums.size());
        return nums.get(idx);
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(head);
 * int param_1 = obj.getRandom();
 */
```

</details>

<details>
    <summary>A word about the solution</Summary>
    The O(n) time and space solution is trivial. O(1) space solution for infinite stream of numbers is obtained via Reservoir sampling, explained <a href = 'https://leetcode.com/problems/linked-list-random-node/solution/' here </a>.
    Might as well implement it and update the solution here soon(Tomorrow).
   
</details>













