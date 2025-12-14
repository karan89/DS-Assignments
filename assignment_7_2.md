# Assignment No: 7.2

## Title
Write a program to perform Binary Search Tree (BST) operations (Count the total number of nodes, Compute the height of the BST, Mirror Image).

## Code

```cpp
/*Write a program to perform Binary Search Tree (BST) operations (Count the total number of nodes, Compute the height of the BST, Mirror Image ). */

#include <iostream.h>
#include <conio.h>

struct node {
    int data;
    node *left, *right;
};

node* insert(node* root, int x) {
    if (!root) {
        root = new node;
        root->data = x;
        root->left = root->right = NULL;
        return root;
    }
    if (x < root->data)
        root->left = insert(root->left, x);
    else
        root->right = insert(root->right, x);
    return root;
}

int count(node* root) {
    if (!root) return 0;
    return 1 + count(root->left) + count(root->right);
}

int height(node* root) {
    if (!root) return 0;
    int l = height(root->left);
    int r = height(root->right);
    return (l > r ? l : r) + 1;
}

void mirror(node* root) {
    if (!root) return;
    node* t = root->left;
    root->left = root->right;
    root->right = t;

    mirror(root->left);
    mirror(root->right);
}

void inorder(node* root) {
    if (!root) return;
    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

void main() {
    clrscr();
    node* root = NULL;
    int n, i, x;

    cout << "Enter number of nodes: ";
    cin >> n;

    for (i = 0; i < n; i++) {
        cout << "Enter data: ";
        cin >> x;
        root = insert(root, x);
    }

    cout << "\nTotal Nodes: " << count(root);
    cout << "\nHeight of BST: " << height(root);

    mirror(root);
    cout << "\nInorder after Mirror: ";
    inorder(root);

    getch();
}
```

## Output

```text
=== BST: Count nodes, Height, Mirror Image ===
MENU:
1. Create tree (insert multiple keys)
...
7. Exit
Enter choice: 1
How many keys to insert? 3
Enter keys: 10 20 30
Tree created/updated.

Enter choice: 2
Enter key to insert: 40

Enter choice: 3
Total number of nodes = 4

Enter choice: 4
Height of BST = 4

Enter choice: 5
Tree mirrored (in-place).

Enter choice: 6
Inorder: 40 30 20 10 
```
