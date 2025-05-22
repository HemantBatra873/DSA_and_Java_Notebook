# Bubble Sort
Simple sorting technique   
2 loops are used   
First loop will go from i = 0 to i = n - 1 representing the max number of repetitions of the passes.  
Second loop will go from j = 0 to j = n - 1 - i because the elements after that must already be at their positions from previous passes.  
Compare arr[j] to arr[j + 1] and if arr[j] is bigger than arr[j+1] then swap them.  
This will lead to the max element being swapped to the end of the array.  
The name is inspired from how bubbles come to the top of the bucket similarly bubble is the max element and it comes to the last position at the end.  
We also use the isSwapped variable so that if no swapping is done(All elements are already swapped we can return directly.  

## Time Complexity :
Best : O(n) Already sorted  
Average : O(n^2)  
Worst : O(n^2)

## Code 
```
private static void bubbleSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            boolean swapped = false;
            for (int j = 0; j < n - 1 - i; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    swapped = true;
                }
            }

            if (!swapped)
                break;
        }
    }
```


## Complete code with i/o

```
import java.util.Scanner;

public class Practice {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter the size of the array");
        int n = sc.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; i++) {
            System.out.println("Enter the value at index " + i);
            arr[i] = sc.nextInt();
        }
        for (int i = 0; i < n; i++) {
            System.out.println("index " + i + " -> " + arr[i]);
        }

        bubbleSort(arr);

        for (int i = 0; i < n; i++) {
            System.out.println("index " + i + " -> " + arr[i]);
        }
        sc.close();
    }

    private static void bubbleSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            boolean swapped = false;
            for (int j = 0; j < n - 1 - i; j++) {
                if (arr[j] > arr[j + 1]) {
                    int temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    swapped = true;
                }
            }

            if (!swapped)
                break;
        }
    }
}
```
