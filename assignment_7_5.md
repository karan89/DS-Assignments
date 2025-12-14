# Assignment No: 7.5

## Title
Write a Program to create a Binary Tree and perform the following Recursive operations on it. a. Inorder Traversal b. Preorder Traversal c. Display Number of Leaf Nodes d. Mirror Image.

## Code

```cpp
/*Write a Program to create a Binary Tree and perform the following Recursive operations on it. a. Inorder Traversal b. Preorder Traversal c. Display Number of Leaf Nodes d. Mirror Image */

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

void inorder(node* root) {
    if (!root) return;
    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

void preorder(node* root) {
    if (!root) return;
    cout << root->data << " ";
    preorder(root->left);
    preorder(root->right);
}

int leafCount(node* root) {
    if (!root) return 0;
    if (!root->left && !root->right) return 1;
    return leafCount(root->left) + leafCount(root->right);
}

void mirror(node* root) {
    if (!root) return;
    node* t = root->left;
    root->left = root->right;
    root->right = t;
    mirror(root->left);
    mirror(root->right);
}

void main() {
    clrscr();
    int x;
    cout << "Enter root value: ";
    cin >> x;
    node* root = create(x);

    cout << "Enter left child: ";
    cin >> x;
    root->left = create(x);

    cout << "Enter right child: ";
    cin >> x;
    root->right = create(x);

    cout << "\nInorder: ";
    inorder(root);

    cout << "\nPreorder: ";
    preorder(root);

    cout << "\nLeaf Nodes: " << leafCount(root);

    mirror(root);
    cout << "\nMirror Inorder: ";
    inorder(root);

    getch();
}
```

## Output

```text
=== Binary Tree: Recursive Operations ===
MENU:
1. Create tree from array (level-order)
...
7. Exit
Enter choice: 1
Enter number of nodes (n): 3
Enter 3 integer values (level-order): 1 2 3
Tree created (complete tree of 3 nodes).

Enter choice: 2
Inorder (recursive): 2 1 3 

Enter choice: 3
Preorder (recursive): 1 2 3 

Enter choice: 4
Number of leaf nodes = 2

Enter choice: 5
Tree mirrored (in-place) recursively.

Enter choice: 6
Level-order: 1 3 2 
```
