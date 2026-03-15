#include <stdio.h>

// Helper function to print the array
void printArray(int A[], int n) {
    for (int i = 0; i < n; i++) {
        printf("%d ", A[i]);
    }
    printf("\n");
}

int partition(int A[], int low, int high) {
    int pivot = A[low]; // Choosing the first element as pivot
    int i = low + 1;
    int j = high;
    int temp;

    do {
        // Move i to the right while elements are smaller than pivot
        while (A[i] <= pivot && i <= high) {
            i++;
        }

        // Move j to the left while elements are larger than pivot
        while (A[j] > pivot) {
            j--;
        }

        // If i and j haven't crossed, swap their elements
        if (i < j) {
            temp = A[i];
            A[i] = A[j];
            A[j] = temp;
        }
    } while (i < j);

    // Finally, swap pivot (A[low]) with A[j]
    temp = A[low];
    A[low] = A[j];
    A[j] = temp;

    return j; // Return the partition index
}

void quickSort(int A[], int low, int high) {
    int partitionIndex; 

    if (low < high) {
        partitionIndex = partition(A, low, high);
        quickSort(A, low, partitionIndex - 1);  // Sort left subarray
        quickSort(A, partitionIndex + 1, high); // Sort right subarray
    }
}

int main() {
    int A[] = {3, 5, 2, 13, 12};
    int n = 5;

    printf("Before Sorting: ");
    printArray(A, n);

    quickSort(A, 0, n - 1);

    printf("After Sorting: ");
    printArray(A, n);

    return 0;
}      
