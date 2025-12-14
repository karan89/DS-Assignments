# Assignment No: 8.1

## Title
Write a program using Trees to assign roll numbers to students based on their previous year's result, where the topper receives roll number 1.

## Code

```cpp
#include <iostream.h>
#include <conio.h>
#include <string.h>

struct Student
{
    char name[20];
    Student *next;
};

struct BST
{
    int marks;
    Student *list;
    BST *left, *right;
};

BST *root = NULL;
int roll = 1;

/* Create student node */
Student* createStudent(char name[])
{
    Student *t = new Student;
    strcpy(t->name, name);
    t->next = NULL;
    return t;
}

/* Create BST node */
BST* createBST(int marks, char name[])
{
    BST *t = new BST;
    t->marks = marks;
    t->list = createStudent(name);
    t->left = t->right = NULL;
    return t;
}

/* Insert student */
BST* insert(BST *r, int marks, char name[])
{
    if (r == NULL)
        return createBST(marks, name);

    if (marks < r->marks)
        r->left = insert(r->left, marks, name);
    else if (marks > r->marks)
        r->right = insert(r->right, marks, name);
    else
    {
        Student *s = r->list;
        while (s->next != NULL)
            s = s->next;
        s->next = createStudent(name);
    }
    return r;
}

/* Assign roll numbers (reverse inorder: Descending marks) */
void assignRoll(BST *r)
{
    if (r != NULL)
    {
        // Visit right (higher marks) first
        assignRoll(r->right);

        Student *s = r->list;
        while (s != NULL)
        {
            cout << "Roll No: " << roll++
                 << "  Name: " << s->name
                 << "  Marks: " << r->marks << endl;
            s = s->next;
        }

        assignRoll(r->left);
    }
}

/* Display marks-wise grouping (Inorder) */
void display(BST *r)
{
    if (r != NULL)
    {
        display(r->left);
        cout << "Marks " << r->marks << " : ";
        Student *s = r->list;
        while (s != NULL)
        {
            cout << s->name << " ";
            s = s->next;
        }
        cout << endl;
        display(r->right);
    }
}

/* MAIN */
void main()
{
    int ch, marks;
    char name[20];
    clrscr();

    do
    {
        cout << "\n--- MENU ---\n";
        cout << "1. Add Student\n";
        cout << "2. Display Marks Groups\n";
        cout << "3. Assign Roll Numbers\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch (ch)
        {
        case 1:
            cout << "Enter Name: ";
            cin >> name;
            cout << "Enter Marks: ";
            cin >> marks;
            root = insert(root, marks, name);
            break;

        case 2:
            if (root == NULL)
                cout << "No students added.\n";
            else
                display(root);
            break;

        case 3:
            if (root == NULL)
                cout << "No students to assign.\n";
            else
            {
                roll = 1;
                cout << "\nAssigned Roll Numbers:\n";
                assignRoll(root);
            }
            break;
        }
    } while (ch != 4);

    getch();
}
```

## Output

```text
=== Assign Roll Numbers by Previous Year Results (Topper Roll 1) ===

Menu:
1. Add student (name and marks)
2. Display marks groups (BST nodes)
3. Assign roll numbers now and display assignments
4. Clear assigned list
5. Exit
Enter choice: 1
Enter student name: Mahavir
Enter marks (integer): 93
Added student: Mahavir with marks 93.

Enter choice: 1
Enter student name: Udayan
Enter marks (integer): 95
Added student: Udayan with marks 95.

Enter choice: 2
Marks groups (ascending marks):
Marks = 93: Mahavir
Marks = 95: Udayan

Enter choice: 3
Assigned 2 roll numbers.

Assigned Roll Numbers (roll -> name -> marks):
1 -> Udayan -> 95
2 -> Mahavir -> 93

Enter choice: 4
Cleared assigned list.
```
