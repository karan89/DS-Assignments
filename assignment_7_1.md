# Assignment No: 7.1

## Title
Write a program to perform Binary Search Tree (BST) operations (Create, Insert, Delete, Levelwise display ).

## Code

```cpp
/*Write a program to perform Binary Search Tree (BST) operations (Create, Insert, Delete,Levelwise display ) */

#include <iostream.h>
#include <conio.h>

struct node {
    int data;
    node *left, *right;
};

node* create(int x) {
    node* t = new node;
    t->data = x;
    t->left = t->right = NULL;
    return t;
}

node* insert(node* root, int x) {
    if (root == NULL)
        return create(x);

    if (x < root->data)
        root->left = insert(root->left, x);
    else
        root->right = insert(root->right, x);

    return root;
}

node* findMin(node* root) {
    while (root->left != NULL)
        root = root->left;
    return root;
}

node* del(node* root, int x) {
    if (root == NULL) return root;

    if (x < root->data)
        root->left = del(root->left, x);
    else if (x > root->data)
        root->right = del(root->right, x);
    else {
        if (root->left == NULL) {
            node* temp = root->right;
            delete root;
            return temp;
        }
        else if (root->right == NULL) {
            node* temp = root->left;
            delete root;
            return temp;
        }
        node* temp = findMin(root->right);
        root->data = temp->data;
        root->right = del(root->right, temp->data);
    }
    return root;
}

void levelOrder(node* root) {
    if (!root) return;
    node* q[30];
    int f = 0, r = 0;

    q[r++] = root;
    while (f < r) {
        node* t = q[f++];
        cout << t->data << " ";
        if (t->left) q[r++] = t->left;
        if (t->right) q[r++] = t->right;
    }
}

void main() {
    clrscr();
    node* root = NULL;
    int n, i, x, delkey;

    cout << "Enter number of nodes: ";
    cin >> n;

    for (i = 0; i < n; i++) {
        cout << "Enter data: ";
        cin >> x;
        root = insert(root, x);
    }

    cout << "\nLevel Order Traversal: ";
    levelOrder(root);

    cout << "\nEnter element to delete: ";
    cin >> delkey;
    root = del(root, delkey);

    cout << "After Deletion: ";
    levelOrder(root);

    getch();
}
```

## Output

```text
=== Binary Search Tree Operations ===
MENU:
1. Create tree (insert multiple keys)
2. Insert key
3. Delete key
4. Level-wise display
5. Inorder display (sorted)
6. Exit
Enter choice: 1
How many keys to insert initially? 3
Enter keys (space separated): 
10 20 30
Tree created/updated.

Enter choice: 2
Enter key to insert: 40
Inserted 40.

Enter choice: 4
Level-order: 10 20 30 40 

Enter choice: 3
Enter key to delete: 20

Enter choice: 5
Inorder: 10 30 40
```
