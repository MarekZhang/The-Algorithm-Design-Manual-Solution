# The Algorithm Design Manual

### Chapter 1 - Introduction to Algorithms

![Untitled](The%20Algorithm%20Design%20Manual%201c24edc510e6440faff1630f3df81945/Untitled.png)

- Solution 1-32
    
    ```jsx
    /* Exercise 1-32 */
    class E1_32 {
    	private static int result = 0;
    
    	private static int divide(int dividend, int divisor) {
    		if (dividend < divisor)
    			return result;
    		result++;
    		return divide(dividend - divisor, divisor);
    	}
    
    	public static void main(String[] args) {
    		System.out.println(divide(10, 3));
    		result = 0;
    		System.out.println(divide(12, 3));
    		result = 0;
    		System.out.println(divide(1999, 13));
    	}
    }
    ```
    
- Solution 1-33
    
    Answer: Seven races.
    
    **First 5 races:** Divide 25 horses into 5 groups and that gives you 5 winners.
    
    **Sixth race:** Now race 5 of them that will give you winner and which two are the bottom-most group. Reject the bottom two group
    
    Now consider the first 3 groups, G1, G2 and G3
    
    G3 Group (the horse that came 3rd in 6th race) - can only bid for 3rd place so we take him for next level i.e. G31
    
    G2 Group (the horse that came 2nd in 6th race) - can bid for 2& 3rd spots we take top two from this group for next level i.e G21, G22
    
    G1 Group (the horse that came 1st in 6th race) - can bid for 1,2,3rd place, but we have already got our first; so we need only to take 2 from this group for next level i.e. G11, G12, G13
    
    **Seventh Race:**: G12, G13, G21, G22, G31 Race them to get 2nd and 3rd winner G11 is already won as 1st winner.
    
- **Leetcode 739. Daily Temperatures**
    
    ![Untitled](The%20Algorithm%20Design%20Manual%201c24edc510e6440faff1630f3df81945/Untitled%201.png)
    

```java
class Solution {
    //time complexity O(N) || space complexity O(N)
    public int[] dailyTemperatures(int[] T) {
       //monotonic stack
       Stack<Integer> stack = new Stack<Integer>();
       int[] res = new int[T.length];
       for(int i = 0; i < T.length; i++){
           if(stack.isEmpty() || T[i] <= T[stack.peek()])
               stack.push(i);
           else{
               while(!stack.isEmpty() && T[i] > T[stack.peek()]){
                   int idx = stack.pop();
                   res[idx] = i - idx;
               } 
               stack.push(i);
           }
       }
       return res;
    }
}
```

- **Leetcode 61. Rotate List**
    
    ![Untitled](The%20Algorithm%20Design%20Manual%201c24edc510e6440faff1630f3df81945/Untitled%202.png)
    

```java
class Solution {
	public ListNode rotateRight(ListNode head, int k) {
		if(head == null || k == 0 ) return head;
		ListNode tempt = head;
		int len = 0;
		
		while(tempt != null) {
			tempt = tempt.next;
			len++;
		}

		k %= len;
        if(k == 0) return head;

		int move = len - k;
		tempt = head;

		for(int i = 1; i < move; i++) {
			tempt = tempt.next;
		}

		ListNode newHead, pointer;
		newHead = pointer = tempt.next;
		tempt.next = null;	

		while(pointer.next != null) pointer = pointer.next;

		pointer.next = head;

		return newHead;
	}
}
```

**Leetcode 324. Wiggle Sort II**

![Untitled](The%20Algorithm%20Design%20Manual%201c24edc510e6440faff1630f3df81945/Untitled%203.png)

```java
import java.util.*;

class Solution {
    public void wiggleSort(int[] nums) {
		int len = nums.length;
		int[] axu = Arrays.copyOfRange(nums, 0, len);
		Arrays.sort(axu);
		int medianPos = (len - 1) / 2;
		int n = medianPos;
		int m = len-1;
		for(int i = 0; i < len; i++) {
			if(i % 2 == 0) {
				nums[i] = axu[n--];
			}else{
				nums[i] = axu[m--];
			}
		}

    }
}
```

- HackerRank **Left Rotation**
    
    ![Untitled](The%20Algorithm%20Design%20Manual%201c24edc510e6440faff1630f3df81945/Untitled%204.png)
    
    ```java
    
      public static List<Integer> rotateLeft(int d, List<Integer> arr) {
      // Write your code here
          List<Integer> res = new ArrayList<Integer>();
          int len = arr.size();
          for(int i = d; i < len; i++){
              res.add(arr.get(i));
          }
          
          for(int i = 0; i < d; i++) {
              res.add(arr.get(i));
          }
    
          return res;
      }
    
    ```
    
- **HackerRank Number Line Jumps**
    
    ![Untitled](The%20Algorithm%20Design%20Manual%201c24edc510e6440faff1630f3df81945/Untitled%205.png)
    
    ```java
    public static String kangaroo(int x1, int v1, int x2, int v2) {
      // Write your code here
          if(v1 <= v2) return "NO";
          return (x2 - x1) % (v1 - v2) == 0 ? "YES" : "NO";
    }
    ```

- -[Hackerland Radio Transmitters](https://www.hackerrank.com/challenges/hackerland-radio-transmitters/problem)
  //TODO
