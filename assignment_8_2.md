# Assignment No: 8.2

## Title
Write a program to illustrate operations on a BST with numeric keys: Insert, Delete, Find, Show.

## Code

```cpp
#include <iostream.h>
#include <conio.h>

struct Node
{
    int data;
    Node *left;
    Node *right;
};

Node *root = NULL;

/* Create Node */
Node* createNode(int x)
{
    Node *t = new Node;
    t->data = x;
    t->left = t->right = NULL;
    return t;
}

/* Insert Node */
Node* insert(Node *r, int x)
{
    if (r == NULL)
        return createNode(x);

    if (x < r->data)
        r->left = insert(r->left, x);
    else if (x > r->data)
        r->right = insert(r->right, x);
    else
        cout << "Duplicate value not allowed\n";

    return r;
}

/* Search Node */
void search(Node *r, int x)
{
    if (r == NULL)
        cout << "Key NOT FOUND\n";
    else if (r->data == x)
        cout << "Key FOUND\n";
    else if (x < r->data)
        search(r->left, x);
    else
        search(r->right, x);
}

/* Find Minimum */
Node* findMin(Node *r)
{
    while (r->left != NULL)
        r = r->left;
    return r;
}

/* Delete Node */
Node* del(Node *r, int x)
{
    if (r == NULL)
    {
        cout << "Key not found\n";
        return r;
    }

    if (x < r->data)
        r->left = del(r->left, x);
    else if (x > r->data)
        r->right = del(r->right, x);
    else
    {
        // Case 1: No child or 1 child
        if (r->left == NULL)
        {
            Node *temp = r->right;
            delete r;
            return temp;
        }
        else if (r->right == NULL)
        {
            Node *temp = r->left;
            delete r;
            return temp;
        }

        // Case 2: 2 children
        Node *t = findMin(r->right);
        r->data = t->data;
        r->right = del(r->right, t->data);
    }
    return r;
}

/* Inorder Traversal */
void inorder(Node *r)
{
    if (r != NULL)
    {
        inorder(r->left);
        cout << r->data << " ";
        inorder(r->right);
    }
}

/* MAIN */
void main()
{
    int ch, x;
    clrscr();

    do
    {
        cout << "\n--- BST MENU ---\n";
        cout << "1. Insert\n";
        cout << "2. Delete\n";
        cout << "3. Search\n";
        cout << "4. Display (Inorder)\n";
        cout << "5. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch (ch)
        {
        case 1:
            cout << "Enter value: ";
            cin >> x;
            root = insert(root, x);
            break;

        case 2:
            cout << "Enter value to delete: ";
            cin >> x;
            root = del(root, x);
            break;

        case 3:
            cout << "Enter value to search: ";
            cin >> x;
            search(root, x);
            break;

        case 4:
            cout << "BST Inorder: ";
            inorder(root);
            cout << endl;
            break;
        }
    } while (ch != 5);

    getch();
}
```

## Output

```text
=== BST Operations: Insert | Delete | Find | Show ===

Menu:
1. Insert key
2. Delete key
3. Find key
4. Show (Inorder Traversal)
5. Exit
Enter choice: 1
Enter key to insert: 10

Enter choice: 1
Enter key to insert: 20

Enter choice: 1
Enter key to insert: 30

Enter choice: 4
BST (Inorder): 10 20 30 

Enter choice: 3
Enter key to search: 20
Key FOUND in BST.

Enter choice: 2
Enter key to delete: 10
```
