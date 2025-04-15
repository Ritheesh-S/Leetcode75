# product-of-array-except-self
link to the problem [leetcode/product-of-array-except-self](https://leetcode.com/problems/product-of-array-except-self/)

## Problem Statement (What I understood)
- given int[] -> return int[] such that i is product of element in int[] other than i
- there i may be -30 to 30 -> can be 0

## Blind attempt
Own attempt at solving

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int total = 1;
        boolean isZero = false;
        boolean isMultiZero = false;
        for(int i=0;i<n;i++){
            if(!isZero && nums[i]==0) {isZero = true;}
            else if(isZero && nums[i]==0) {isMultiZero = true;break;}
            else{
                total *= nums[i];
            }
        }
        int[] soln = new int[n];
        for(int i=0;i<n;i++){
            if(isMultiZero) {soln[i]=0;}
            else if(isZero && nums[i]!=0) {soln[i]=0;}
            else if(isZero && nums[i]==0) {soln[i]=total;}
            else {soln[i] = total/nums[i];}
        }
        return soln;
    }
}
```

## Blind attempt remarks
- two blind spot in total product -> is there single/ multiple zero in int[]
- iterate once to confirm the above case and find Total of i with value
- return by total/i
- edge case MultiZero return all a Zero 
- edge case singleZero return all zero except i=0 with total

## Optimization attempt 1
no difference to above in space nor time
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        boolean isZero = false;
        boolean isMultiZero = false;
        int firstZero = 0;
        int total = 1;
        int n = nums.length;
        for (int i = 0; i < n; i++) {
            if (!isZero && nums[i] == 0) {
                isZero = true;
                firstZero = i;
            } else if (isZero && nums[i] == 0) {
                isMultiZero = true;
                break;
            } else {
                total *= nums[i];
            }
        }
        int[] soln = new int[n];
        if (isMultiZero)
            return soln;
        if (isZero) {
            soln[firstZero] = total;
            return soln;
        }
        for (int i = 0; i < n; i++) {
            soln[i] = total / nums[i];
        }
        return soln;
    }
}
```

## Optimization attempt 2
```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int soln[] = new int[n];
        soln[0] = 1;
        for (int i = 1; i < n; i++)
            soln[i] = nums[i - 1] * soln[i - 1];
        int suffix = 1;
        for (int i = n - 1; i >= 0; i--) {
            soln[i] *= suffix;
            suffix *= nums[i];
        }
        return soln;
    }
}
```

## Observations
- int[] intializes items to zero -> primitive int does not have null or invalid char, defaults to zero
- sliding window 
    - loop once to prepare soln[i] with product of items before i
    - loop back to set suffix with product of items after i 
    - Multiply back to soln[i] in the same to get product of all except i