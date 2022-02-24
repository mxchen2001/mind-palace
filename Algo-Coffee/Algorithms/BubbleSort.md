# Bubble Sort

Probably the first "algorithm" that you will every write. The idea is to compare two adjacent elements and swap them if they are in the wrong order. Locally, this just fixes the position of a single elements, but do this for the every element in the array will produce a sorted array.

You can image a "bubble" propagating up the array, where the largest element will bubble to the top in each iteration. This

```java
void bubbleSort(int[] array) {
    for (int i = 0; i < array.length - 1; i++) {
        for (int j = 0; j < array.length - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }  
        }
    }
}
```

Time Complexity: O(n^2)
Space Complexity: O(1)