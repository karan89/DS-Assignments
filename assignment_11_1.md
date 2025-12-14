# Assignment No: 11.1

## Title
Implement a hash table with collision resolution using linear probing.

## Code

```cpp
#include <iostream.h>
#include <conio.h>

#define MAX 20

int table[MAX];
int SIZE;

/* Hash function */
int hashFunc(int key)
{
    return key % SIZE;
}

/* Insert key using Linear Probing */
void insertKey(int key)
{
    int index = hashFunc(key);
    int start = index;

    while (table[index] != -1)
    {
        index = (index + 1) % SIZE;

        if (index == start)
        {
            cout << "Hash Table is full\n";
            return;
        }
    }

    table[index] = key;
}

/* Display hash table */
void display()
{
    int i;
    cout << "\nHash Table:\n";
    for (i = 0; i < SIZE; i++)
    {
        if (table[i] == -1)
            cout << i << " : EMPTY\n";
        else
            cout << i << " : " << table[i] << endl;
    }
}

/* MAIN */
void main()
{
    int i, ch, key;
    clrscr();

    cout << "Enter Hash Table Size (max 20): ";
    cin >> SIZE;

    for (i = 0; i < SIZE; i++)
        table[i] = -1;

    do
    {
        cout << "\n--- HASH TABLE MENU ---\n";
        cout << "1. Insert Key\n";
        cout << "2. Display Table\n";
        cout << "3. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch (ch)
        {
        case 1:
            cout << "Enter key: ";
            cin >> key;
            insertKey(key);
            break;

        case 2:
            display();
            break;
        }
    } while (ch != 3);

    getch();
}

```

## Output

```text
Enter number of elements: 5
Enter elements:
34 56 13 34 67

Hash Table: 
0 --> NULL
1 --> NULL
2 --> NULL
3 --> 13
4 --> 34
5 --> 34
6 --> 56
7 --> 67
8 --> NULL
9 --> NULL
```
