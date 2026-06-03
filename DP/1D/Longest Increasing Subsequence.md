# Longest Increasing Subsequence (LIS)
The Longest Increasing Subsequence (LIS) problem is a classic algorithmic problem. The goal is to find the length of the longest subsequence of a given sequence such that all elements of the subsequence are sorted in increasing order.
Below are two common approaches to solve this problem in Java: the Dynamic Programming approach (which allows us to easily reconstruct and print the actual subsequence) and the Binary Search approach (which is highly optimized for finding just the length).
## 1. Dynamic Programming Approach (Printing the LIS)
This approach computes the LIS by building up an array dp where dp[i] stores the length of the LIS ending at index i. To print the actual sequence, we maintain an additional parent array that keeps track of the previous index in the LIS sequence.
 * **Time Complexity:** O(N^2)
 * **Space Complexity:** O(N)
### Java Code
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class LIS_DP {
    public static void printLIS(int[] arr) {
        int n = arr.length;
        if (n == 0) {
            System.out.println("Array is empty.");
            return;
        }

        // dp[i] stores the length of LIS ending at arr[i]
        int[] dp = new int[n];
        // parent[i] stores the index of the previous element in the LIS ending at arr[i]
        int[] parent = new int[n];

        // Initialize DP and parent arrays
        for (int i = 0; i < n; i++) {
            dp[i] = 1;
            parent[i] = i; // Initially, every element is its own parent
        }

        // Compute DP and parent arrays
        for (int i = 0; i < n; i++) {
            for (int prev = 0; prev < i; prev++) {
                if (arr[prev] < arr[i] && 1 + dp[prev] > dp[i]) {
                    dp[i] = 1 + dp[prev];
                    parent[i] = prev;
                }
            }
        }

        // Find the index of the maximum LIS length
        int maxLen = -1;
        int lastIndex = -1;
        for (int i = 0; i < n; i++) {
            if (dp[i] > maxLen) {
                maxLen = dp[i];
                lastIndex = i;
            }
        }

        // Backtrack using the parent array to reconstruct the sequence
        List<Integer> lis = new ArrayList<>();
        lis.add(arr[lastIndex]);
        while (parent[lastIndex] != lastIndex) {
            lastIndex = parent[lastIndex];
            lis.add(arr[lastIndex]);
        }

        // The sequence is constructed backwards, so reverse it
        Collections.reverse(lis);

        System.out.println("DP Approach -> Length: " + maxLen);
        System.out.println("DP Approach -> Sequence: " + lis);
    }

    public static void main(String[] args) {
        int[] arr = {10, 9, 2, 5, 3, 7, 101, 18};
        printLIS(arr);
    }
}

```
## 2. Binary Search Approach (Optimal Length Calculation)
This approach maintains a temporary array representing an increasing subsequence. We iterate through the original array. If the current element is larger than the last element of the temporary array, we append it. Otherwise, we use binary search to find the smallest element in the temporary array that is greater than or equal to the current element, and we replace it.
*Note: The temporary array does **not** always store the actual LIS at the end, but its final length will perfectly match the length of the correct LIS.*
 * **Time Complexity:** O(N \log N)
 * **Space Complexity:** O(N)
### Java Code
```java
import java.util.Arrays;

public class LIS_BinarySearch {
    public static int lengthOfLIS(int[] arr) {
        if (arr == null || arr.length == 0) {
            return 0;
        }

        int n = arr.length;
        // temp array to store the increasing subsequence elements
        int[] temp = new int[n];
        int len = 0; // Current length of the temp array

        temp[0] = arr[0];
        len = 1;

        for (int i = 1; i < n; i++) {
            // If arr[i] is greater than the last element of temp, it extends the LIS
            if (arr[i] > temp[len - 1]) {
                temp[len] = arr[i];
                len++;
            } else {
                // Find the index of the first element in temp that is >= arr[i]
                int idx = Arrays.binarySearch(temp, 0, len, arr[i]);
                
                // If Arrays.binarySearch doesn't find the exact key, 
                // it returns -(insertion_point) - 1. We extract the insertion point.
                if (idx < 0) {
                    idx = -(idx + 1);
                }
                
                // Replace it with arr[i] to keep the elements in temp as small as possible
                temp[idx] = arr[i];
            }
        }

        return len;
    }

    public static void main(String[] args) {
        int[] arr = {10, 9, 2, 5, 3, 7, 101, 18};
        int length = lengthOfLIS(arr);
        System.out.println("Binary Search Approach -> Length: " + length);
    }
}

```
