# greatest-common-divisor-of-strings
link to the problem [leetcode/greatest-common-divisor-of-strings](https://leetcode.com/problems/greatest-common-divisor-of-strings/)

## Problem Statement (What I understood)
Greatest String x whic on repeat can form str1 and str2
- str1 and str2 **WILL** exist and all UPPER cased

## Blind attempt
Own attempt at solving

```java
class Solution {
    public String gcdOfStrings(String str1, String str2) {
        int str1Len = str1.length();
        int str2Len = str2.length();
        int soln = str1Len <= str2Len ? str1Len : str2Len;
        while (soln > 0) {
            if (str1Len % soln == 0 && str2Len % soln == 0) {
                int aRep = str1Len / soln;
                int bRep = str2Len / soln;
                String rep = str1.substring(0, soln);
                String aComp = rep.repeat(aRep);
                String bComp = rep.repeat(bRep);
                if (str1.equals(aComp) && str2.equals(bComp)) {
                    break;
                }
            }
            soln--;
        }
        if (soln == 0)
            return "";
        else
            return str1.substring(0, soln);
    }
}
```

## Blind attempt remarks
- String.repeat(count) -> available after Java11
- String.substring(a,b) -> it will take index from a to b-1
- Too much of a Naive approach

## Optimization attempt
```java
class Solution {
    public int gcd(int a, int b) {
        return b == 0 ? a : gcd(b, a % b);
    }

    public String gcdOfStrings(String str1, String str2) {
        if ((str1 + str2).equals(str2 + str1)) {
            int gcdVal = gcd(str1.length(), str2.length());
            return str1.substring(0, gcdVal);
        } else
            return "";
    }
}
```

## Observations
- if combined in any order results in the same string.. there will be a GCD Substring
- Do a basic GCD and return that substring 