# Assignment No: 2.1

## Title
In Computer Engg. Dept. of VIT there are S.Y., T.Y., and B.Tech. students. Assume that all these students are on ground for a function. We need to identify a student of S.Y. div. (X) whose name is "XYZ" and roll no. is "17". Apply appropriate Searching method to identify the required student.

## Code

```cpp
#include<iostream.h>
#include<conio.h>
#include<string.h>
#include<stdlib.h>

struct Student
{
    char name[20];
    int roll;
    char year[5];
    char div[5];
};

/* Linear Search */
int linearSearch(Student s[], int n, int roll)
{
    int i;
    for(i = 0; i < n; i++)
    {
        if(s[i].roll == roll)
            return i;
    }
    return -1;
}

/* Binary Search (array must be sorted by roll no) */
int binarySearch(Student s[], int n, int roll)
{
    int low = 0, high = n - 1, mid;

    while(low <= high)
    {
        mid = (low + high) / 2;

        if(s[mid].roll == roll)
            return mid;
        else if(s[mid].roll < roll)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return -1;
}

void main()
{
    Student s[20];
    int n, i, ch, pos, roll;

    clrscr();

    cout << "Enter number of students: ";
    cin >> n;

    for(i = 0; i < n; i++)
    {
        cout << "\nEnter details of student " << i+1 << endl;
        cout << "Name: ";
        cin >> s[i].name;
        cout << "Roll No: ";
        cin >> s[i].roll;
        cout << "Year: ";
        cin >> s[i].year;
        cout << "Division: ";
        cin >> s[i].div;
    }

    cout << "\nEnter Roll Number to Search: ";
    cin >> roll;

    do
    {
        cout << "\n1. Linear Search";
        cout << "\n2. Binary Search";
        cout << "\n3. Exit";
        cout << "\nEnter Choice: ";
        cin >> ch;

        switch(ch)
        {
            case 1:
                pos = linearSearch(s, n, roll);
                break;

            case 2:
                pos = binarySearch(s, n, roll);
                break;

            case 3:
                exit(0);
        }

        if(pos != -1)
        {
            cout << "\nStudent Found";
            cout << "\nName: " << s[pos].name;
            cout << "\nRoll: " << s[pos].roll;
            cout << "\nYear: " << s[pos].year;
            cout << "\nDivision: " << s[pos].div << endl;
        }
        else
        {
            cout << "\nStudent Not Found\n";
        }

    } while(ch != 3);

    getch();
}

```

## Output

```text
Enter student details to search:
Name: Karan
Roll No: 27
Year: SY
Division: A

1. Linear Search
2. Binary Search
3. Exit
Enter the choice: 1

Student Data not found using Linear Search.

1. Linear Search
2. Binary Search
3. Exit
Enter the choice: 2

Student Data not found using Binary Search.

1. Linear Search
2. Binary Search
3. Exit
Enter the choice: 3
```
