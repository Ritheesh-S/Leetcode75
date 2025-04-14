# can-place-flowers
link to the problem [leetcode/can-place-flowers](https://leetcode.com/problems/can-place-flowers/)

## Problem Statement (What I understood)
- Flower bed with X pots and N new flower
- N can be 0 but X will have value 
- new flower cannot have adjacent flowers
- edge case when X=1 and at corners

## Blind attempt
Own attempt at solving

```java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        if (n == 0)
            return true;
        int len = flowerbed.length;
        if (len == 1) {
            if (flowerbed[0] == 0 && n == 1)
                return true;
            else
                return false;
        }
        if (flowerbed[0] == 0 && flowerbed[1] == 0 && n > 0) {
            flowerbed[0] = 1;
            n--;
        }
        if (flowerbed[len - 1] == 0 && flowerbed[len - 2] == 0 && n > 0) {
            flowerbed[len - 1] = 1;
            n--;
        }
        int count = 0;
        for (int i = 1; i < len - 1 && n > 0; i++) {
            if (flowerbed[i] == 0)
                count++;
            else
                count = 0;
            if (count == 3) {
                count = 1;
                n--;
            }
        }
        if (n == 0)
            return true;
        else
            return false;
    }
}
```

## Blind attempt remarks
- Naive attempt just loop handle inner row of 3 Zeros
- edge case failed on X=1 with conditions N=0 and other atttemps
- 0 and X-1 edge case handling failed -> handle it separately 
- N=0 needs to be handled first
- Total 4 attempts to get all clear

## Optimization attempt
```java
class Solution {
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        if (n == 0)
            return true;
        int len = flowerbed.length;
        for (int i = 0; i < len; i++) {
            if (flowerbed[i] == 0 && ((i == 0 || flowerbed[i - 1] == 0) && (i == len - 1 || flowerbed[i + 1] == 0))) {
                flowerbed[i] = 1;
                n--;
            }
            if (n == 0)
                return true;
        }
        return false;
    }
}
```

## Observations
- we can do a OR check for the edge cases and handle it simple
- if first OR condition satisfes 2nd is not checked if First AND fails the second is not checked