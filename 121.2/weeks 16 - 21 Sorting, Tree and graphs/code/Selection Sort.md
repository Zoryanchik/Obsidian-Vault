![[Pasted image 20250224000051.png]]
class SelectionSort {
    static void selectionSort(int[] array) {
        for (int i = 0; i < array.length; i++) { // Outer loop
            int iMin = i; // Assume the first element is the minimum
            for (int j = i + 1; j < array.length; j++) { // Inner loop
                if (array[j] < array[iMin]) iMin = j; // Update iMin if a smaller element is found
            }
            if (iMin != i) { // Swap the elements if a new minimum is found
                int tmp = array[i];
                array[i] = array[iMin];
                array[iMin] = tmp;
            }
        }
    }
}
