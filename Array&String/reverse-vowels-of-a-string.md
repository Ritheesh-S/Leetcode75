# reverse-vowels-of-a-string
link to the problem [leetcode/reverse-vowels-of-a-string](https://leetcode.com/problems/reverse-vowels-of-a-string/)

## Problem Statement (What I understood)
reverse just the vowel in a string as simple as it sounds

## Blind attempt
Own attempt at solving

```java
class Solution {
    public String reverseVowels(String s) {
        List<Character> vowels = Arrays.asList('a', 'i', 'u', 'e', 'o', 'A', 'I', 'U', 'E', 'O');
        StringBuilder strb = new StringBuilder(s);
        int i = 0, j = strb.length() - 1;
        boolean ichk = false, jchk = false;
        while (i < j) {
            Character ichar = strb.charAt(i);
            Character jchar = strb.charAt(j);
            if (ichk || vowels.contains(ichar))
                ichk = true;
            else
                i++;
            if (jchk || vowels.contains(jchar))
                jchk = true;
            else
                j--;
            if (ichk && jchk) {
                ichk = false;
                jchk = false;
                strb.setCharAt(j, ichar);
                strb.setCharAt(i, jchar);
                i++;
                j--;
            }
        }
        return strb.toString();
    }
}
```

## Blind attempt remarks
- too much time in comparing vowels ig
- initialize check list of vowels and two pointer swap the String 
- StringBuilder has method to replace char at index

## Optimization attempt
```java
class Solution {
    public String reverseVowels(String s) {
        char[] strb = s.toCharArray();
        int i = 0, j = strb.length - 1;
        while (i < j) {
            while (i < j && !isVowel(strb[i]))
                i++;
            while (i < j && !isVowel(strb[j]))
                j--;
            if (i < j) {
                Character temp = strb[j];
                strb[j] = strb[i];
                strb[i] = temp;
                i++;
                j--;
            }
        }
        return String.valueOf(strb);
    }
    
    private boolean isVowel(char c) {
        return c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u'
                || c == 'A' || c == 'E' || c == 'I' || c == 'O' || c == 'U';
    }
}
```

## Observations
- simple char check is faster than Hashset or a List lookup
- instead of iterating main loop for each increment, loop till vowel hit