# Assignment No: 11.5

## Title
WAP to simulate a faculty database as a hash table. Search a particular faculty by using MOD as a hash function for linear probing method of collision handling technique. Assume suitable data for faculty record.

## Code

```cpp
#include <iostream.h>
#include <conio.h>
#include <string.h>

#define MAX 20

struct Faculty
{
    int id;
    char name[20];
};

Faculty table[MAX];
int SIZE;

/* Hash Function (MOD) */
int hashFunction(int id)
{
    return id % SIZE;
}

/* Insert using Linear Probing */
void insertFaculty(int id, char name[])
{
    int index = hashFunction(id);
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

    cout << "Faculty record inserted.\n";
}

/* Search using Linear Probing */
void searchFaculty(int id)
{
    int index = hashFunction(id);
    int start = index;

    while (table[index].id != -1)
    {
        if (table[index].id == id)
        {
            cout << "\nFaculty Found\n";
            cout << "ID   : " << table[index].id << endl;
            cout << "Name : " << table[index].name << endl;
            return;
        }

        index = (index + 1) % SIZE;
        if (index == start)
            break;
    }

    cout << "Faculty not found.\n";
}

/* Display Table */
void display()
{
    int i;
    cout << "\n--- FACULTY HASH TABLE ---\n";
    for (i = 0; i < SIZE; i++)
    {
        if (table[i].id == -1)
            cout << i << " : EMPTY\n";
        else
            cout << i << " : [" << table[i].id
                 << ", " << table[i].name << "]\n";
    }
}

/* MAIN */
void main()
{
    int ch, id, i;
    char name[20];
    clrscr();

    cout << "Enter hash table size (max 20): ";
    cin >> SIZE;

    for (i = 0; i < SIZE; i++)
        table[i].id = -1;

    do
    {
        cout << "\n--- MENU ---\n";
        cout << "1. Insert Faculty\n";
        cout << "2. Search Faculty\n";
        cout << "3. Display Table\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch (ch)
        {
        case 1:
            cout << "Enter Faculty ID: ";
            cin >> id;
            cout << "Enter Name: ";
            cin >> name;
            insertFaculty(id, name);
            break;

        case 2:
            cout << "Enter Faculty ID to search: ";
            cin >> id;
            searchFaculty(id);
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
Faculty Hash Table: 
0 -> NULL
1 -> 101, Dr.Sharma
2 -> 112, Prof.Mehta
3 -> 123, Dr.Khan
4 -> 134, Prof.Rao
5 -> NULL
6 -> NULL
7 -> NULL
8 -> NULL
9 -> NULL

Searching Faculty ID 123:
Faculty Found:
ID   : 123
Name : Dr.Khan
```
