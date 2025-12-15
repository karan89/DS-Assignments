# Assignment No: 2.3

## Title
Write a program to input marks of n students. Sort the marks in ascending order using the Quick Sort algorithm without using built-in library functions and analyse the sorting algorithm pass by pass. Find the minimum and maximum marks using Divide and Conquer (recursively).

## Code

```cpp
#include<iostream.h>
#include<conio.h>

void swapInt(int &a, int &b) {
    int temp = a;
    a = b;
    b = temp;
}

// Partition function for Quick Sort
int partition(int arr[], int low, int high) {
    int pivot = arr[low];
    int i = low;
    int j = high;
    while(i<j) {
        while(arr[i]<=pivot && i<=high-1) {
            i++;
        }
        while(arr[j]>pivot && j>=low+1) {
            j--;
        }
        if(i<j) swapInt(arr[i], arr[j]);
    }
    swapInt(arr[low], arr[j]);
    return j;
}

// Quick Sort
void quick_sort(int arr[], int low, int high) {
    if(low<high) {
        int parIndex = partition(arr, low, high);
        quick_sort(arr, low, parIndex-1);
        quick_sort(arr, parIndex+1, high);
    }
}

// Function to find min and max using Divide and Conquer
void minmax(int arr[], int low, int high, int &minVal, int &maxVal) {
    int mid;
    
    if(low==high) {
        if(arr[low]<minVal) minVal=arr[low];
        if(arr[high]>maxVal) maxVal=arr[high];
        return;
    }

    if(high==low+1) {
        if(arr[low]<arr[high]) {
            if(arr[low]<minVal) minVal=arr[low];
            if(arr[high]>maxVal) maxVal=arr[high];
        }
        else {
            if(arr[high]<minVal) minVal=arr[high];
            if(arr[low]>maxVal) maxVal=arr[low];
        }
        return;
    }

    mid=(low+high)/2;
    minmax(arr, low, mid, minVal, maxVal);
    minmax(arr, mid+1, high, minVal, maxVal);
}

int main() {
    int n, i;
    int arr[50]; // Fixed size for Turbo C
    int minVal, maxVal;

    clrscr();

    cout<<"Enter number of students: ";
    cin>>n;

    for (i = 0; i < n; i++) {
        cout<<"Enter marks: ";
        cin>>arr[i];
    }

    quick_sort(arr, 0, n - 1);

    cout<<"\nStudents sorted by Marks: \n";
    for (i = 0; i < n; i++) {
        cout << arr[i]<<endl;
    }

    minVal = arr[0];
    maxVal = arr[0];

    minmax(arr, 0, n-1, minVal, maxVal);

    cout<<"\nMinimum marks: "<<minVal<<endl;
    cout<<"Maximum marks: "<<maxVal<<endl;

    getch();
    return 0;
}

```

## Output

```text
Enter number of students: 4
Enter marks: 98
Enter marks: 45
Enter marks: 99
Enter marks: 78

Students sorted by Marks: 
45
78
98
99

Minimum marks: 45
Maximum marks: 99
```
