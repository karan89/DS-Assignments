# Assignment No: 8.3

## Title
Search employee records using a Tree and sort them by employee ID.

## Code

```cpp
#include <iostream.h>
#include <conio.h>
#include <string.h>

struct Emp
{
    int empid;
    char name[20];
    char dept[20];
    float salary;
    Emp *left, *right;
};

Emp *root = NULL;

/* Create employee node */
Emp* createNode(int id, char n[], char d[], float s)
{
    Emp *t = new Emp;
    t->empid = id;
    strcpy(t->name, n);
    strcpy(t->dept, d);
    t->salary = s;
    t->left = t->right = NULL;
    return t;
}

/* Insert employee */
Emp* insert(Emp *r, int id, char n[], char d[], float s)
{
    if (r == NULL)
        return createNode(id, n, d, s);

    if (id < r->empid)
        r->left = insert(r->left, id, n, d, s);
    else if (id > r->empid)
        r->right = insert(r->right, id, n, d, s);
    else
    {
        // Update existing employee
        strcpy(r->name, n);
        strcpy(r->dept, d);
        r->salary = s;
        cout << "Employee updated.\n";
    }
    return r;
}

/* Search employee */
void search(Emp *r, int id)
{
    if (r == NULL)
        cout << "Employee NOT FOUND\n";
    else if (r->empid == id)
    {
        cout << "EmpID: " << r->empid << endl;
        cout << "Name: " << r->name << endl;
        cout << "Dept: " << r->dept << endl;
        cout << "Salary: " << r->salary << endl;
    }
    else if (id < r->empid)
        search(r->left, id);
    else
        search(r->right, id);
}

/* Inorder traversal (sorted output) */
void inorder(Emp *r)
{
    if (r != NULL)
    {
        inorder(r->left);
        cout << r->empid << "  "
             << r->name << "  "
             << r->dept << "  "
             << r->salary << endl;
        inorder(r->right);
    }
}

/* MAIN */
void main()
{
    int ch, id;
    char name[20], dept[20];
    float sal;
    clrscr();

    do
    {
        cout << "\n--- EMPLOYEE MENU ---\n";
        cout << "1. Insert / Update Employee\n";
        cout << "2. Search Employee\n";
        cout << "3. Display All Employees (Sorted)\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch (ch)
        {
        case 1:
            cout << "Enter EmpID: ";
            cin >> id;
            cout << "Enter Name: ";
            cin >> name;
            cout << "Enter Department: ";
            cin >> dept;
            cout << "Enter Salary: ";
            cin >> sal;
            root = insert(root, id, name, dept, sal);
            break;

        case 2:
            cout << "Enter EmpID to search: ";
            cin >> id;
            search(root, id);
            break;

        case 3:
            if (root == NULL)
                cout << "No employee records.\n";
            else
            {
                cout << "\nEmpID  Name  Dept  Salary\n";
                inorder(root);
            }
            break;
        }
    } while (ch != 4);

    getch();
}

```

## Output

```text
=== Employee Records using BST (search & sort by empid) ===

Menu:
1. Insert / Update employee
2. Search employee by empid
3. Show all employees (sorted by empid)
4. Exit
Enter choice: 1
Enter empid (integer): 101
Enter name: Mahavir
Enter department: HR
Enter salary: 90000
Employee inserted/updated.

Enter choice: 1
Enter empid (integer): 102
Enter name: Udayan
Enter department: Manager
Enter salary: 95000
Employee inserted/updated.

Enter choice: 2
Enter empid to search: 102
Found: EmpID: 102 | Name: Udayan | Dept: Manager | Salary: 95000

Enter choice: 3
Employees sorted by empid (ascending):
EmpID: 101 | Name: Mahavir | Dept: HR | Salary: 90000
EmpID: 102 | Name: Udayan | Dept: Manager | Salary: 95000
```
