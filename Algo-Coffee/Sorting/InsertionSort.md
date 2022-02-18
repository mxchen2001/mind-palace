# Insertion Sort

You've probably first performed insertion sort when one of your friends asked you to put a deck of cards in the right order. The of insertion sort is to put the current element into the correct position in the array. You will do this for every element in the array.

```java
void insertionSort(int[] array) {
    for (int i = 1; i < array.length; i++) {
        for (int j = i - 1; i >= 0; j--) {
            if (array[j] < array[i]) {
                array[j + 1] = array[i];
                break;
            }
            array[j + 1] = array[j];
        }
    }
}
```