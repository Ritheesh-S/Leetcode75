# reverse-words-in-a-string
link to the problem [leetcode/reverse-words-in-a-string](https://leetcode.com/problems/reverse-words-in-a-string/)

## Problem Statement (What I understood)
- ~~Thought we had to reverse chars in individual words and not the whole sentance at first~~
- the just wanted the words in reverse order

## Blind attempt
Own attempt at solving

```java
class Solution {
    public String reverseWords(String s) {
        String strm = s.trim().replaceAll(" +", " ");
        StringBuilder soln = new StringBuilder();
        String[] star = strm.split(" ");
        for (int i = star.length - 1; i > 0; i--) {
            soln.append(star[i]).append(" ");
        }
        soln.append(star[0]);
        return soln.toString();
    }
}
```

## Blind attempt remarks
- trim trailing and leading space -> replace multiple spaces with single space
- split with space and reverse iterate to build the string in reverse word order

## Optimization attempt 1
```java
class Solution {
    public String reverseWords(String s) {
        String[] star = s.trim().split("\\s+");
        StringBuilder soln = new StringBuilder();
        for (int i = star.length - 1; i > 0; i--)
            soln.append(star[i]).append(" ");
        return soln.append(star[0]).toString();
    }
}
```
## Optimization attempt 2
```java
class Solution {
    public String reverseWords(String s) {
        int i = s.length() - 1;
        int j = 0;
        StringBuilder soln = new StringBuilder("");
        while (i >= 0) {
            while (i >= 0 && s.charAt(i) == ' ') {
                i--;
            }
            if (i < 0) {
                break;
            }
            j = i;
            while (i >= 0 && s.charAt(i) != ' ') {
                i--;
            }
            if (soln.length() == 0) {
                soln.append(s.substring(i + 1, j + 1));
            } else {
                soln.append(" ").append(s.substring(i + 1, j + 1));
            }
        }
        return soln.toString();
    }
}
```

## Observations
- split directly sith \\s+ 
- String substring with two pointer seems O(N) we iterate once 
- iterate once on Substring? still total is less time than -> Trim() and Split()
