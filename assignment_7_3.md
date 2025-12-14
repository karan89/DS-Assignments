# Assignment No: 7.3

## Title
Write a Program to create a Binary Tree Search and Find Minimum/Maximum in BST.

## Code

```cpp
/*Write a Program to create a Binary Tree Search and Find Minimum/Maximum in BST  */

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

int findMin(node* root) {
    while (root->left)
        root = root->left;
    return root->data;
}

int findMax(node* root) {
    while (root->right)
        root = root->right;
    return root->data;
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

    cout << "\nMinimum Value: " << findMin(root);
    cout << "\nMaximum Value: " << findMax(root);

    getch();
}
```

## Output

```text
=== BST: Insert, Find Min & Max ===
MENU
1. Insert Key
2. Display Inorder
3. Find Minimum
4. Find Maximum
5. Exit
Enter choice: 1
Enter value to insert: 10

Enter choice: 1
Enter value to insert: 20

Enter choice: 1
Enter value to insert: 30

Enter choice: 2
Inorder Traversal: 10 20 30 

Enter choice: 3
Minimum value = 10

Enter choice: 4
Maximum value = 30
```
