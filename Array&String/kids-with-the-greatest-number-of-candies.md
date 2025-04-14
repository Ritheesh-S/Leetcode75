# kids-with-the-greatest-number-of-candies
link to the problem [leetcode/kids-with-the-greatest-number-of-candies](https://leetcode.com/problems/kids-with-the-greatest-number-of-candies/)

## Problem Statement (What I understood)
N kids with some candies if given the extracandies will he become the one with the greatest amount of candies
- return list of Boolean if the i'th kid will

## Blind attempt
Own attempt at solving

```java
class Solution {
    public List<Boolean> kidsWithCandies(int[] candies, int extraCandies) {
        int n = candies.length;
        int max = candies[0];
        for (int i = 1; i < n; i++)
            if (candies[i] > max)
                max = candies[i];
        List<Boolean> ans = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            if (candies[i] + extraCandies >= max)
                ans.add(true);
            else
                ans.add(false);
        }
        return ans;
    }
}
```

## Blind attempt remarks
- find max
- check if satisfies condition and add to list

## Optimization attempt
```java
class Solution {
    public List<Boolean> kidsWithCandies(int[] candies, int extraCandies) {
        int n = candies.length;
        List<Boolean> ans = new ArrayList<Boolean>(n);
        int max = candies[0];
        for (int i = 1; i < n; i++) {
            if (candies[i] > max) {
                max = candies[i];
            }
        }
        for (int i = 0; i < n; i++) {
            int total = candies[i] + extraCandies;
            ans.add(total >= max);
        }
        return ans;
    }
}
```

## Observations
- Instead of checking condition while returning Boolean just return the condition
- Blind attempt seems to be the optimal approach for this 