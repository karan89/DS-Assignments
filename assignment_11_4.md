# Assignment No: 11.4

## Title
Store and retrieve student records using roll numbers.

## Code

```cpp
#include <iostream.h>
#include <conio.h>
#include <string.h>

struct Node
{
    int roll;
    char name[20];
    Node *next;
};

Node *table[20];
int SIZE;

/* Hash Function */
int hashFunction(int roll)
{
    return roll % SIZE;
}

/* Insert Student */
void insertStudent(int roll, char name[])
{
    int index = hashFunction(roll);

    Node *t = new Node;
    t->roll = roll;
    strcpy(t->name, name);
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

    cout << "Student record inserted.\n";
}

/* Search Student */
void searchStudent(int roll)
{
    int index = hashFunction(roll);
    Node *p = table[index];

    while (p != NULL)
    {
        if (p->roll == roll)
        {
            cout << "\nStudent Found\n";
            cout << "Roll No: " << p->roll << endl;
            cout << "Name   : " << p->name << endl;
            return;
        }
        p = p->next;
    }
    cout << "Student not found.\n";
}

/* Display Hash Table */
void display()
{
    int i;
    cout << "\n--- HASH TABLE ---\n";
    for (i = 0; i < SIZE; i++)
    {
        cout << i << " -> ";
        Node *p = table[i];
        while (p != NULL)
        {
            cout << "[" << p->roll << ", " << p->name << "] -> ";
            p = p->next;
        }
        cout << "NULL\n";
    }
}

/* MAIN */
void main()
{
    int ch, roll, i;
    char name[20];
    clrscr();

    cout << "Enter hash table size (max 20): ";
    cin >> SIZE;

    for (i = 0; i < SIZE; i++)
        table[i] = NULL;

    do
    {
        cout << "\n--- MENU ---\n";
        cout << "1. Insert Student\n";
        cout << "2. Search Student\n";
        cout << "3. Display All Records\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch (ch)
        {
        case 1:
            cout << "Enter Roll Number: ";
            cin >> roll;
            cout << "Enter Name: ";
            cin >> name;
            insertStudent(roll, name);
            break;

        case 2:
            cout << "Enter Roll Number to search: ";
            cin >> roll;
            searchStudent(roll);
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
1. Insert Student
2. Search Student
3. Display All
4. Exit
Enter choice: 1
Enter Roll Number: 34
Enter Name: Sakshi

1. Insert Student
2. Search Student
3. Display All
4. Exit
Enter choice: 1
Enter Roll Number: 13
Enter Name: neha

1. Insert Student
2. Search Student
3. Display All
4. Exit
Enter choice: 2
Enter Roll Number to search: 34

Student Found:
Roll No: 34
Name   : Sakshi

1. Insert Student
2. Search Student
3. Display All
4. Exit
Enter choice: 3

Student Records: 
Roll: 13 Name: neha
Roll: 34 Name: Sakshi
```
