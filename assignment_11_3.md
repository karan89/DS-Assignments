# Assignment No: 11.3

## Title
Implement collision resolution using linked lists.

## Code

```cpp
#include <iostream.h>
#include <conio.h>

struct Node
{
    int data;
    Node *next;
};

Node *table[20];
int SIZE;

/* Hash function */
int hashFunction(int key)
{
    return key % SIZE;
}

/* Insert key using chaining */
void insertKey(int key)
{
    int index = hashFunction(key);

    Node *t = new Node;
    t->data = key;
    t->next = NULL;

    if (table[index] == NULL)
        table[index] = t;
    else
    {
        Node *p = table[index];
        while (p->next != NULL)
            p = p->next;
        p->next = t;
    }
}

/* Display hash table */
void display()
{
    int i;
    cout << "\nHash Table:\n";
    for (i = 0; i < SIZE; i++)
    {
        cout << i << " -> ";
        Node *p = table[i];
        while (p != NULL)
        {
            cout << p->data << " -> ";
            p = p->next;
        }
        cout << "NULL\n";
    }
}

/* MAIN */
void main()
{
    int choice, key, i;
    clrscr();

    cout << "Enter hash table size (max 20): ";
    cin >> SIZE;

    for (i = 0; i < SIZE; i++)
        table[i] = NULL;

    do
    {
        cout << "\n--- MENU ---\n";
        cout << "1. Insert\n";
        cout << "2. Display\n";
        cout << "3. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice)
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
    } while (choice != 3);

    getch();
}

```

## Output

```text
Enter number of elements: 5
Enter elements:
34 13 56 78 90

Hash Table:
0 -> 90 -> NULL
1 -> NULL
2 -> NULL
3 -> 13 -> NULL
4 -> 34 -> NULL
5 -> NULL
6 -> 56 -> NULL
7 -> NULL
8 -> 78 -> NULL
9 -> NULL
```
