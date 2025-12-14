# Assignment No: 12.1

## Title
WAP to simulate a faculty database as a hash table. Search a particular faculty by using 'divide' as a hash function for linear probing with chaining without replacement method of collision handling technique. Assume suitable data for faculty record.

## Code

```cpp
#include <iostream.h>
#include <conio.h>
#include <string.h>

#define SIZE 10

struct Faculty
{
    int id;
    char name[20];
    int next;   // index of next element in chain
};

Faculty table[SIZE];

/* Hash function (Divide method) */
int hashFunction(int key)
{
    return key % SIZE;
}

/* Insert using linear probing with chaining without replacement */
void insertFaculty(int id, char name[])
{
    int index = hashFunction(id);

    if (table[index].id == -1)
    {
        table[index].id = id;
        strcpy(table[index].name, name);
        table[index].next = -1;
        return;
    }

    /* Find empty slot using linear probing */
    int i = (index + 1) % SIZE;
    while (i != index && table[i].id != -1)
        i = (i + 1) % SIZE;

    if (i == index)
    {
        cout << "Hash table is full\n";
        return;
    }

    table[i].id = id;
    strcpy(table[i].name, name);
    table[i].next = -1;

    /* Link chain */
    int p = index;
    while (table[p].next != -1)
        p = table[p].next;
    table[p].next = i;
}

/* Search faculty */
void searchFaculty(int id)
{
    int index = hashFunction(id);

    int p = index;
    while (p != -1)
    {
        if (table[p].id == id)
        {
            cout << "\nFaculty Found\n";
            cout << "ID   : " << table[p].id << endl;
            cout << "Name : " << table[p].name << endl;
            return;
        }
        p = table[p].next;
    }

    cout << "Faculty Not Found\n";
}

/* Display hash table */
void display()
{
    int i;
    cout << "\n--- FACULTY HASH TABLE ---\n";
    for (i = 0; i < SIZE; i++)
    {
        cout << i << " : ";
        if (table[i].id == -1)
            cout << "EMPTY\n";
        else
            cout << table[i].id << ", " << table[i].name
                 << " -> " << table[i].next << endl;
    }
}

/* MAIN */
void main()
{
    int i, ch, id;
    char name[20];
    clrscr();

    for (i = 0; i < SIZE; i++)
    {
        table[i].id = -1;
        table[i].next = -1;
    }

    do
    {
        cout << "\n--- FACULTY MENU ---\n";
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
1 -> (21, Sharma) -> (31, Mehta) -> (41, Rao) -> NULL
2 -> (52, Khan) -> NULL
3 -> NULL
4 -> NULL
5 -> NULL
6 -> NULL
7 -> NULL
8 -> NULL
9 -> NULL

Searching Faculty ID 31:
Faculty Found:
ID   : 31
Name : Mehta
```
