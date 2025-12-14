# Assignment No: 11.2

## Title
Implement collision handling using separate chaining.

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

/* Hash Function */
int hashFunc(int key)
{
    return key % SIZE;
}

/* Insert Key */
void insertKey(int key)
{
    int index = hashFunc(key);

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

/* Display Hash Table */
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
    int ch, key, i;
    clrscr();

    cout << "Enter Hash Table Size (max 20): ";
    cin >> SIZE;

    for (i = 0; i < SIZE; i++)
        table[i] = NULL;

    do
    {
        cout << "\n--- HASH TABLE MENU ---\n";
        cout << "1. Insert\n";
        cout << "2. Display\n";
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
45 14 23 78 90

Hash Table with Separate Chaining: 
0 -> 90 -> NULL
1 -> NULL
2 -> NULL
3 -> 23 -> NULL
4 -> 14 -> NULL
5 -> 45 -> NULL
6 -> NULL
7 -> NULL
8 -> 78 -> NULL
9 -> NULL
```
