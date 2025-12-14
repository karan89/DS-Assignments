# Assignment No: 12.3

## Title
WAP to simulate employee databases as a hash table. Search a particular faculty by using Mid square method as a hash function for linear probing method of collision handling technique. Assume suitable data for faculty record.

## Code

```cpp
#include <iostream.h>
#include <conio.h>
#include <string.h>

#define SIZE 10

struct Employee
{
    int id;
    char name[20];
    char dept[20];
};

Employee table[SIZE];

/* Mid-Square Hash Function */
int midSquareHash(int key)
{
    long sq = (long)key * key;
    return (sq / 10) % SIZE;
}

/* Insert using Linear Probing */
void insertEmployee(int id, char name[], char dept[])
{
    int index = midSquareHash(id);
    int start = index;

    while (table[index].id != -1)
    {
        index = (index + 1) % SIZE;
        if (index == start)
        {
            cout << "Hash table is full\n";
            return;
        }
    }

    table[index].id = id;
    strcpy(table[index].name, name);
    strcpy(table[index].dept, dept);

    cout << "Employee inserted at index " << index << endl;
}

/* Search Employee */
void searchEmployee(int id)
{
    int index = midSquareHash(id);
    int start = index;

    while (table[index].id != -1)
    {
        if (table[index].id == id)
        {
            cout << "\nEmployee Found\n";
            cout << "ID   : " << table[index].id << endl;
            cout << "Name : " << table[index].name << endl;
            cout << "Dept : " << table[index].dept << endl;
            return;
        }

        index = (index + 1) % SIZE;
        if (index == start)
            break;
    }

    cout << "Employee not found\n";
}

/* Display Hash Table */
void display()
{
    int i;
    cout << "\nEmployee Hash Table:\n";
    for (i = 0; i < SIZE; i++)
    {
        if (table[i].id == -1)
            cout << i << " : EMPTY\n";
        else
            cout << i << " : " << table[i].id << " | "
                 << table[i].name << " | "
                 << table[i].dept << endl;
    }
}

/* MAIN */
void main()
{
    int i, ch, id;
    char name[20], dept[20];
    clrscr();

    for (i = 0; i < SIZE; i++)
        table[i].id = -1;

    do
    {
        cout << "\n--- EMPLOYEE MENU ---\n";
        cout << "1. Insert Employee\n";
        cout << "2. Search Employee\n";
        cout << "3. Display Hash Table\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch (ch)
        {
        case 1:
            cout << "Enter Employee ID: ";
            cin >> id;
            cout << "Enter Name: ";
            cin >> name;
            cout << "Enter Department: ";
            cin >> dept;
            insertEmployee(id, name, dept);
            break;

        case 2:
            cout << "Enter Employee ID to search: ";
            cin >> id;
            searchEmployee(id);
            break;

        case 3:
            display();
            break;
        }
    } while (ch != 4);

    getch();
}

```

## Output

```text
--- Employee Database Menu ---
1. Insert Employee
2. Search Employee
3. Display Hash Table
4. Exit
Enter choice: 1
Enter Employee ID: 1
Enter Name: Ram
Enter Department: CO

Enter choice: 1
Enter Employee ID: 2
Enter Name: Shyam
Enter Department: CM

Enter choice: 3
Hash Table: 
0 -> 1 | Ram | CO
1 -> 2 | Shyam | CM
2 -> 
3 -> 
4 -> 
5 -> 
6 -> 
7 -> 
8 -> 
9 -> 
```
