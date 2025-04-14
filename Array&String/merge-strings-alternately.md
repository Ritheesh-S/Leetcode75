# merge-strings-alternately
link to the problem [leetcode/merge-strings-alternately](https://leetcode.com/problems/merge-strings-alternately)

## Problem Statement (What I understood)
merge two Strings alternating chars
- both **WILL** contain data
- one may be long -> just append remaining

## Blind attempt
Own attempt at solving

```java
class Solution {
    public String mergeAlternately(String word1, String word2) {
        int a = word1.length();
        int b = word2.length();

        StringBuilder soln = new StringBuilder(a + b);
        int i = 0;
        int j = 0;
        while (i < a || j < b) {
            if (i < a) {
                soln.append(word1.charAt(i));
                i++;
            }
            if (j < b) {
                soln.append(word2.charAt(j));
                j++;
            }
        }
        return soln.toString();
    }
}
```

## Blind attempt remarks

- ~~.length~~ -> .length() for String
- StringBuilder can be initialized to a Size
- ~~String.getCharAt(int)~~ -> String.charAt(int)

## Optimization attempt

```java
class Solution {
    public String mergeAlternately(String word1, String word2) {
        StringBuilder soln = new StringBuilder(word1.length() + word2.length());
        int i = 0;
        while (i < word1.length() || i < word2.length()) {
            if (i < word1.length()) {
                soln.append(word1.charAt(i));
            }
            if (i < word2.length()) {
                soln.append(word2.charAt(i));
            }
            i++;
        }
        return soln.toString();
    }
}
```

## Observations
- since its single iteration no need for index j
- Optional -> No need to assign length to variable a,b (but doing so with better variable name is more readable)