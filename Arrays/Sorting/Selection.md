# Selection sort
Why is it called selection?  
Because it selects the minimum element from the unsorted part(The entire array at the beginning) and places the selected element at its correct position.

So it uses 2 loops
The iteration of the first loop gives the position where the current min element from the unsorted part must come to.  
And the second iteration finds this element by using a minIndex int.
Then the minIndex element is places at index i of the first loop current iteration.

## Time complexkity
Best - O(n^2)   
Average - O(n^2)  
Worst - O(n^2)

## code

```
private static void selectionSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            int minIndex = i;
            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIndex]) {
                    minIndex = j;
                }
            }
            int temp = arr[i];
            arr[i] = arr[minIndex];
            arr[minIndex] = temp;
        }
    }
```
