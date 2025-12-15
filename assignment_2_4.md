# Assignment No: 2.4

## Title
Write a program using Bubble sort algorithm, assign the roll nos. to the students of your class as per their previous years result. i.e. topper will be roll no. 1 and analyse the sorting algorithm pass by pass.

## Code

```cpp
#include<iostream.h>
#include<conio.h>

struct Student {
    int student_roll_no;
    int total_marks;
};

void bubble_sort(Student arr[], int n) {
    int i, j;
    for(i=0; i<n-1; i++) {
        for(j=0; j<n-i-1; j++) {
            if(arr[j].total_marks < arr[j+1].total_marks) {
                // Manual swap
                Student temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}

int main() {
    int n, i;
    Student arr[50]; // Fixed size
    
    clrscr();

    cout<<"Enter number of students: ";
    cin>>n;
    
    for(i=0; i<n; i++) {
        cout<<"Enter totalmarks for student "<<i+1<<": ";
        cin>>arr[i].total_marks;
    }
    
    bubble_sort(arr, n);
    
    // Assign roll numbers based on sorted rank
    for(i=0; i<n; i++) {
        arr[i].student_roll_no = i+1;
    }
    
    cout<<"\nStudents details: \n";
    cout<<"Roll no.     Marks\n";
    for(i=0; i<n; i++) {
        cout<<" "<<arr[i].student_roll_no<<"            "<<arr[i].total_marks<<endl;
    }
    
    getch();
    return 0;
}

```

## Output

```text
Enter number of students: 4
Enter totalmarks for student 1: 90
Enter totalmarks for student 2: 93
Enter totalmarks for student 3: 87
Enter totalmarks for student 4: 56

Students details: 
Roll no.    Marks
1           93
2           90
3           87
4           56
```
