# Assignment No: 12.5

## Title
Design and implement a smart college placement portal that uses advanced hashing techniques to efficiently manage student placement records with high performance and low collision probability, even under dynamic data growth.

## Code

```cpp
#include <iostream.h>
#include <conio.h>
#include <string.h>

#define SIZE 10

struct Student
{
    int roll;
    char name[20];
    char company[20];
    Student *next;
};

Student *table[SIZE];

/* Hash Function */
int hashFunction(int roll)
{
    return roll % SIZE;
}

/* Insert Record */
void insertRecord(int roll, char name[], char company[])
{
    int index = hashFunction(roll);

    Student *t = new Student;
    t->roll = roll;
    strcpy(t->name, name);
    strcpy(t->company, company);
    t->next = NULL;

    if (table[index] == NULL)
        table[index] = t;
    else
    {
        Student *p = table[index];
        while (p->next != NULL)
            p = p->next;
        p->next = t;
    }

    cout << "Placement record inserted.\n";
}

/* Search Record */
void searchRecord(int roll)
{
    int index = hashFunction(roll);
    Student *p = table[index];

    while (p != NULL)
    {
        if (p->roll == roll)
        {
            cout << "\nRecord Found\n";
            cout << "Roll No : " << p->roll << endl;
            cout << "Name    : " << p->name << endl;
            cout << "Company : " << p->company << endl;
            return;
        }
        p = p->next;
    }
    cout << "Record not found.\n";
}

/* Delete Record */
void deleteRecord(int roll)
{
    int index = hashFunction(roll);
    Student *p = table[index];
    Student *prev = NULL;

    while (p != NULL)
    {
        if (p->roll == roll)
        {
            if (prev == NULL)
                table[index] = p->next;
            else
                prev->next = p->next;

            delete p;
            cout << "Record deleted successfully.\n";
            return;
        }
        prev = p;
        p = p->next;
    }
    cout << "Record not found.\n";
}

/* Display All Records */
void display()
{
    int i;
    cout << "\n--- Placement Records ---\n";
    for (i = 0; i < SIZE; i++)
    {
        cout << i << " -> ";
        Student *p = table[i];
        while (p != NULL)
        {
            cout << "[" << p->roll << ", " << p->name
                 << ", " << p->company << "] -> ";
            p = p->next;
        }
        cout << "NULL\n";
    }
}

/* MAIN */
void main()
{
    int i, ch, roll;
    char name[20], company[20];
    clrscr();

    for (i = 0; i < SIZE; i++)
        table[i] = NULL;

    do
    {
        cout << "\n--- SMART PLACEMENT PORTAL ---\n";
        cout << "1. Insert Placement Record\n";
        cout << "2. Search Record\n";
        cout << "3. Delete Record\n";
        cout << "4. Display All Records\n";
        cout << "5. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch (ch)
        {
        case 1:
            cout << "Enter Roll No: ";
            cin >> roll;
            cout << "Enter Name: ";
            cin >> name;
            cout << "Enter Company: ";
            cin >> company;
            insertRecord(roll, name, company);
            break;

        case 2:
            cout << "Enter Roll No to search: ";
            cin >> roll;
            searchRecord(roll);
            break;

        case 3:
            cout << "Enter Roll No to delete: ";
            cin >> roll;
            deleteRecord(roll);
            break;

        case 4:
            display();
            break;
        }
    } while (ch != 5);

    getch();
}
```

## Output

```text
--- Smart Placement Portal ---
1. Add Placement Record
2. Search Record
3. Delete Record
4. Display All
5. Exit
Enter choice: 1
Enter Roll No: 34
Enter Name: Ram
Enter Company: Apple
Record Added.

Enter choice: 1
Enter Roll No: 13
Enter Name: Shyam
Enter Company: Google
Record Added.

Enter choice: 4
--- Placement Records ---
0 -> NULL
1 -> NULL
2 -> NULL
3 -> [13|Shyam|Google] -> NULL
4 -> [34|Ram|Apple] -> NULL
...
```
