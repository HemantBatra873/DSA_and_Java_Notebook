# Quick sort 

Called quick because quickly sorts the pivot into ita right position.

How it works.

- You call qs(a,l,r) and then it calls par(a,l,r) and returns pi's idx and then qs is called recursivelt on qs(a,l,pi-1) and qs(a,pi+1,r).

- In par(a,l,r) we select pi elem which is say last a[r] and we sort it to correct pos using different partition schemes.

## Lomuto partition schemes

Pivot = last element.

Moves smaller elements to the left.

Uses a for loop.

Slightly less efficient (more swaps).

```java

public class QuickSort {

    public static void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            int pi = partition(arr, low, high);

            // Recursively sort elements before and after partition
            quickSort(arr, low, pi - 1);
            quickSort(arr, pi + 1, high);
        }
    }

    private static int partition(int[] arr, int low, int high) {
        int pivot = arr[high];  // Choose last element as pivot
        int i = low - 1;

        for (int j = low; j < high; j++) {
            if (arr[j] < pivot) {
                i++;
                // swap arr[i] and arr[j]
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }

        // Place pivot in correct position
        int temp = arr[i + 1];
        arr[i + 1] = arr[high];
        arr[high] = temp;

        return i + 1;
    }

    public static void main(String[] args) {
        int[] arr = {10, 7, 8, 9, 1, 5};
        quickSort(arr, 0, arr.length - 1);

        System.out.print("Sorted array: ");
        for (int num : arr)
            System.out.print(num + " ");
    }
}

```

## Hoare Partition Scheme

```java

public class QuickSortHoare {

    public static void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            int pi = partition(arr, low, high);
            quickSort(arr, low, pi);
            quickSort(arr, pi + 1, high);
        }
    }

    private static int partition(int[] arr, int low, int high) {
        int pivot = arr[(low + high) / 2];
        int i = low;
        int j = high;

        while (true) {
            while (arr[i] < pivot) i++;
            while (arr[j] > pivot) j--;

            if (i >= j)
                return j;

            // Swap arr[i] and arr[j]
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;

            i++;
            j--;
        }
    }

    public static void main(String[] args) {
        int[] arr = {10, 7, 8, 9, 1, 5};
        quickSort(arr, 0, arr.length - 1);

        System.out.print("Sorted array: ");
        for (int num : arr)
            System.out.print(num + " ");
    }
}

```