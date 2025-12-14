# Assignment No: 12.4

## Title
WAP to simulate student databases as a hash table. a student database management system using hashing techniques to allow efficient insertion, search, and deletion of student records.

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
    char course[20];
    Student *next;
};

Student *hashTable[SIZE];

/* Hash Function */
int hashFunction(int roll)
{
    return roll % SIZE;
}

/* Create Node */
Student* createNode(int roll, char name[], char course[])
{
    Student *t = new Student;
    t->roll = roll;
    strcpy(t->name, name);
    strcpy(t->course, course);
    t->next = NULL;
    return t;
}

/* Insert Student */
void insertStudent(int roll, char name[], char course[])
{
    int index = hashFunction(roll);
    Student *t = createNode(roll, name, course);

    if (hashTable[index] == NULL)
        hashTable[index] = t;
    else
    {
        Student *p = hashTable[index];
        while (p->next != NULL)
            p = p->next;
        p->next = t;
    }
    cout << "Student inserted successfully.\n";
}

/* Search Student */
void searchStudent(int roll)
{
    int index = hashFunction(roll);
    Student *p = hashTable[index];

    while (p != NULL)
    {
        if (p->roll == roll)
        {
            cout << "\nStudent Found\n";
            cout << "Roll No : " << p->roll << endl;
            cout << "Name    : " << p->name << endl;
            cout << "Course  : " << p->course << endl;
            return;
        }
        p = p->next;
    }
    cout << "Student not found.\n";
}

/* Delete Student */
void deleteStudent(int roll)
{
    int index = hashFunction(roll);
    Student *p = hashTable[index];
    Student *prev = NULL;

    while (p != NULL)
    {
        if (p->roll == roll)
        {
            if (prev == NULL)
                hashTable[index] = p->next;
            else
                prev->next = p->next;

            delete p;
            cout << "Student deleted successfully.\n";
            return;
        }
        prev = p;
        p = p->next;
    }
    cout << "Student not found.\n";
}

/* Display Hash Table */
void display()
{
    int i;
    cout << "\n--- Student Hash Table ---\n";
    for (i = 0; i < SIZE; i++)
    {
        cout << i << " -> ";
        Student *p = hashTable[i];
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
    int i, ch, roll;
    char name[20], course[20];
    clrscr();

    for (i = 0; i < SIZE; i++)
        hashTable[i] = NULL;

    do
    {
        cout << "\n--- STUDENT DATABASE MENU ---\n";
        cout << "1. Insert Student\n";
        cout << "2. Search Student\n";
        cout << "3. Delete Student\n";
        cout << "4. Display Hash Table\n";
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
            cout << "Enter Course: ";
            cin >> course;
            insertStudent(roll, name, course);
            break;

        case 2:
            cout << "Enter Roll No to search: ";
            cin >> roll;
            searchStudent(roll);
            break;

        case 3:
            cout << "Enter Roll No to delete: ";
            cin >> roll;
            deleteStudent(roll);
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
Student Database Menu
1. Insert Student
2. Search Student
3. Delete Student
4. Display Hash Table
5. Exit
Enter your choice: 1
Enter Roll No: 1
Enter Name: sakshi
Enter Course: co
Student Inserted Successfully!

Enter your choice: 1
Enter Roll No: 2
Enter Name: John
Enter Course: Ai
Student Inserted Successfully!

Enter your choice: 4
--- Student Hash Table ---
0 -> NULL
1 -> [1,sakshi] -> NULL
2 -> [2,John] -> NULL
...
```
