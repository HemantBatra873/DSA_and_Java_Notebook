# Insertion sort
What we do is we pick an element and we insert it into its correct position without doing many swaps.  
So we start this algorithm with index 2 as we need to compare with the previous indexes.  
When we pick an index we set the element at that index as the key.  
Now we make a pointer j and set it to the previous index.  
Now while j >= 0 and arr[j] will be more than key we will move element at j ahead to make space for key and set j to j - 1.  
If you observe in doing so we have craeted an empty space because element at j goes to j + 1 and j goes to j - 1.  
This position which is j + 1 is where our key is supposed to be inserted.  
Hence the name insertion sort.

## Time complexity
Best - O(n)  
Average - O(n^2)  
Worst - O(n^2)

## Code
```
private static void insertionSort(int[] arr) {
        int n = arr.length;
        for (int i = 1; i < n; i++) {
            int key = arr[i];
            int j = i - 1;
            while (j >= 0 && arr[j] > key) {
                arr[j + 1] = arr[j];
                j = j - 1;
            }
            arr[j + 1] = key;
        }
    }
```
