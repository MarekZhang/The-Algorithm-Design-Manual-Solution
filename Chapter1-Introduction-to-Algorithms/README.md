# The Algorithm Design Manual

### Chapter 1 - Introduction to Algorithms

![Untitled](The%20Algorithm%20Design%20Manual%205903c47b617d424db98495d092cbd95f/Untitled.png)

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
    
- Leetcode **739. Daily Temperatures**
    
    ![Untitled](The%20Algorithm%20Design%20Manual%205903c47b617d424db98495d092cbd95f/Untitled%201.png)
    

```jsx
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