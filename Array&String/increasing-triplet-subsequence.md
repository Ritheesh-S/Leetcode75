# increasing-triplet-subsequence
link to the problem [leetcode/increasing-triplet-subsequence](https://leetcode.com/problems/increasing-triplet-subsequence)

## Problem Statement (What I understood)
- index i,j,k in nums[] where ` i < j < k ` and ` nums[i] < nums[j] < nums[k] ` 

## Blind attempt
Own attempt at solving

```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        int n = nums.length;
        if (n < 3)
            return false;

        for (int i = 0; i < n - 2; i++) {
            for (int j = i + 1; j < n - 1; j++) {
                for (int k = j + 1; k < n; k++) {
                    if (nums[i] < nums[j] && nums[j] < nums[k])
                        return true;
                }
            }
        }
        return false;
    }
}
```

## Blind attempt remarks
- could only think of a naive solution -> timelimit exceeded

## Optimization attempt
```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        int low = Integer.MAX_VALUE;
        int mid = Integer.MAX_VALUE;
        for(int i:nums){
            if(i<=low) low=i;
            else if(i<=mid) mid=i;
            else return true;
        }
        return false;
    }
}
```

## Observations
- iterate and find lowest and second lowest if any greater there exist a triplet
- even if lowest update second lowest will hold meaning there was a lower value previously hence any value higher than both will return true