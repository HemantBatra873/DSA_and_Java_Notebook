# Leaders in the array 

Given an array, print all the elements which are leaders. 
 
A Leader is an element that is greater than all of the elements on its right side in the array.

```
import java.util.*;

public class FindLeaders {
    public static void main(String[] args) {
        int[] arr = {16, 17, 4, 3, 5, 2};
        printLeaders(arr);
    }

    public static void printLeaders(int[] arr) {
        int n = arr.length;
        List<Integer> leaders = new ArrayList<>();

        int maxFromRight = arr[n - 1];
        leaders.add(maxFromRight);  // Last element is always a leader

        // Traverse the array from right to left
        for (int i = n - 2; i >= 0; i--) {
            if (arr[i] > maxFromRight) {
                maxFromRight = arr[i];
                leaders.add(maxFromRight);
            }
        }

        // Since we traversed from right to left, reverse the list
        Collections.reverse(leaders);
        System.out.println("Leaders in the array: " + leaders);
    }
}
```