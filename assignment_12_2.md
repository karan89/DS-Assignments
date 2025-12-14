# Assignment No: 12.2

## Title
WAP to simulate a faculty database as a hash table. Search a particular faculty by using MOD as a hash function for linear probing with chaining with replacement method of collision handling technique. Assume suitable data for faculty record.

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
    char dept[20];
    int next;   // index for chain
};

Faculty table[SIZE];

/* Hash Function (MOD / Divide method) */
int hashFunction(int key)
{
    return key % SIZE;
}

/* Insert using chaining with replacement */
void insertFaculty(int id, char name[], char dept[])
{
    int index = hashFunction(id);

    /* If home position empty */
    if (table[index].id == -1)
    {
        table[index].id = id;
        strcpy(table[index].name, name);
        strcpy(table[index].dept, dept);
        table[index].next = -1;
        return;
    }

    /* Find empty slot using linear probing */
    int i = (index + 1) % SIZE;
    while (i != index && table[i].id != -1)
        i = (i + 1) % SIZE;

    if (i == index)
    {
        cout << "Hash table full\n";
        return;
    }

    /* If occupant at home index does NOT belong there → replace */
    if (hashFunction(table[index].id) != index)
    {
        table[i] = table[index];   // move old record
        table[index].id = id;
        strcpy(table[index].name, name);
        strcpy(table[index].dept, dept);
        table[index].next = i;
    }
    else
    {
        table[i].id = id;
        strcpy(table[i].name, name);
        strcpy(table[i].dept, dept);
        table[i].next = -1;

        int p = index;
        while (table[p].next != -1)
            p = table[p].next;
        table[p].next = i;
    }
}

/* Search Faculty */
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
            cout << "Dept : " << table[p].dept << endl;
            return;
        }
        p = table[p].next;
    }

    cout << "Faculty Not Found\n";
}

/* Display Hash Table */
void display()
{
    int i;
    cout << "\n--- FACULTY HASH TABLE ---\n";
    for (i = 0; i < SIZE; i++)
    {
        if (table[i].id == -1)
            cout << i << " : EMPTY\n";
        else
            cout << i << " : [" << table[i].id << ", "
                 << table[i].name << "] -> " << table[i].next << endl;
    }
}

/* MAIN */
void main()
{
    int i, ch, id;
    char name[20], dept[20];
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
        cout << "3. Display Hash Table\n";
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
            cout << "Enter Department: ";
            cin >> dept;
            insertFaculty(id, name, dept);
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
--- Faculty Database Menu ---
1. Insert Faculty
2. Search Faculty
3. Display Hash Table
4. Exit
Enter choice: 1
Enter Faculty ID: 1
Enter Name: sakshi
Enter Department: co

Enter choice: 1
Enter Faculty ID: 2
Enter Name: neha
Enter Department: ENTC

Enter choice: 2
Enter Faculty ID to Search: 2
Faculty Found!
ID: 2
Name: neha
Department: ENTC

Enter choice: 3
0 -> NULL
1 -> [1 | sakshi] -> NULL
2 -> [2 | neha] -> NULL
3 -> NULL
4 -> NULL
5 -> NULL
6 -> NULL
7 -> NULL
8 -> NULL
9 -> NULL
```
