# String to Integer (atoi)

Implement the myAtoi(string s) function, which converts a string to a 32-bit signed integer.

The algorithm for myAtoi(string s) is as follows:

Whitespace: Ignore any leading whitespace (" ").

Signedness: Determine the sign by checking if the next character is '-' or '+', assuming positivity if neither present.

Conversion: Read the integer by skipping leading zeros until a non-digit character is encountered or the end of the string is reached. If no digits were read, then the result is 0.

Rounding: If the integer is out of the 32-bit signed integer range [-2^31, 2^31 - 1], then round the integer to remain in the range. Specifically, integers less than -2^31 should be rounded to -2^31, and integers greater than 2^31 - 1 should be rounded to 2^31 - 1.

Return the integer as the final result.

## Methods
Character.isDigit() - Tells if the character is a digit or not.
Character.isLetter() - Tells if the character is a letter or not.

## Code
1. s.trim() to remove white spaces.
2. If string is empty return 0.
3. Check if the first element is + or - if yes set the sign accordingly. Default is +.
4. Then for each digit if it is digit then add it to the result by multiplying previous number by 10 and adding this number.
5. But before this check if the number overflows from integer limit by checking if max (Integer.MAX_VALUE) - number / 10 is not less than current number.
6. If that is the case just return the integer max or min according to the sign.
```
class Solution {
    public int myAtoi(String s) {
        int max = Integer.MAX_VALUE;
        int min = Integer.MIN_VALUE;
        s = s.trim();
        if (s.length() == 0) {
            return 0; 
        }
        int sign = 1;  
        int idx = 0; 
        if (s.charAt(0) == '-') {
            sign = -1;
            idx++;
        } else if (s.charAt(0) == '+') {
            idx++; 
        }
        long res = 0;
        while (idx < s.length() && Character.isDigit(s.charAt(idx))) {
            int d = s.charAt(idx) - '0'; 
            if (res > (max - d) / 10) {
                return sign == 1 ? max : min;
            }

            res = res * 10 + d;
            idx++;
        }
        return (int) res * sign;
    }
}
```
