# Assignment No: 2.5

## Title
Write a program to arrange the list of employees as per the average of their height and weight by using Merge and Selection sorting method. Analyse their time complexities and conclude which algorithm will take less time to sort the list.

## Code

```cpp
#include<iostream.h>
#include<conio.h>

struct Employee {
    float height;
    float weight;
    float avg;
};

// Function to calculate average of height and weight
void calculate_avg(Employee arr[], int n) {
    int i;
    for(i=0; i<n; i++) {
        arr[i].avg = (arr[i].height + arr[i].weight) / 2.0;
    } 
}

// Selection Sort
void selection_sort(Employee arr[], int n) {
    int i, j, min;
    for(i=0; i<n-1; i++) {
        min = i;
        for(j=i+1; j<n; j++) {
            if(arr[j].avg < arr[min].avg) {
                min = j;
            }
        }
        // Manual swap of entire struct (essential for data integrity)
        Employee temp = arr[min];
        arr[min] = arr[i];
        arr[i] = temp;
    }
}

// Merge function for Merge Sort
void merge(Employee arr[], int low, int mid, int high) {
    Employee temp[100];  
    int left = low;
    int right = mid + 1;
    int k = 0;
    int i;

    while(left <= mid && right <= high) {
        if(arr[left].avg <= arr[right].avg) {
            temp[k++] = arr[left++];
        } else {
            temp[k++] = arr[right++];
        }
    }

    while(left <= mid) temp[k++] = arr[left++];
    while(right <= high) temp[k++] = arr[right++];
 
    for(i = low; i <= high; i++) {
        arr[i] = temp[i - low];
    }
}

// Merge Sort
void merge_sort(Employee arr[], int low, int high) {
    int mid;
    if(low >= high) return;

    mid = (low + high) / 2;
    merge_sort(arr, low, mid);
    merge_sort(arr, mid + 1, high);
    merge(arr, low, mid, high);
}

int main() {
    int n, i, choice;
    Employee emp[50]; // Fixed size
    clrscr();

    cout << "Enter the number of employees: ";
    cin >> n;

    for(i=0; i<n; i++) {
        cout << "Enter height and weight of employee " << i+1 << ": ";
        cin >> emp[i].height >> emp[i].weight;
    }

    calculate_avg(emp, n);

    cout << "\nChoose sorting method:\n1. Selection Sort\n2. Merge Sort\nEnter choice: ";
    cin >> choice;

    switch(choice) {
        case 1:
            selection_sort(emp, n);
            cout << "\nSorted using Selection Sort.\n";
            break;
        case 2:
            merge_sort(emp, 0, n-1);
            cout << "\nSorted using Merge Sort.\n";
            break;
        default:
            cout << "Invalid choice! Showing unsorted list.\n";
    }

    cout << "\nEmployee details:\n";
    cout << "Height     Weight     Average\n";
    for(i=0; i<n; i++) {
        cout << emp[i].height << "          " << emp[i].weight << "         " << emp[i].avg << endl;
    }

    getch();
    return 0;
}

```

## Output

```text
Enter the number of employees: 3
Enter height and weight of employee 1: 167 53
Enter height and weight of employee 2: 170 75
Enter height and weight of employee 3: 162 60

Choose sorting method:
1. Selection Sort
2. Merge Sort
Enter choice: 1

Sorted using Selection Sort.

Employee details:
Height    Weight    Average
167       53        110
170       75        111
162       60        122.5
```
