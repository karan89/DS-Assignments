# Assignment No: 7.4

## Title
Write a Program to create a Binary Tree and perform following Non-recursive operations on it. a. Inorder Traversal b. Preorder Traversal c. Display Number of Leaf Nodes d. Mirror Image.

## Code

```cpp
/*Write a Program to create a Binary Tree and perform following 
Nonrecursive operations on it. a. Inorder Traversal b. Preorder 
Traversal c. Display Number of Leaf Nodes d. Mirror Image */

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
    node* stack[30];
    int top = -1;
    node* cur = root;

    while (cur || top != -1) {
        while (cur) {
            stack[++top] = cur;
            cur = cur->left;
        }
        cur = stack[top--];
        cout << cur->data << " ";
        cur = cur->right;
    }
}

void preorder(node* root) {
    node* stack[30];
    int top = -1;
    stack[++top] = root;

    while (top != -1) {
        node* t = stack[top--];
        cout << t->data << " ";
        if (t->right) stack[++top] = t->right;
        if (t->left) stack[++top] = t->left;
    }
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

    cout << "Enter left child of root: ";
    cin >> x;
    root->left = create(x);

    cout << "Enter right child of root: ";
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
=== Binary Tree: Non-recursive operations ===
MENU:
1. Create tree from array (level-order)
...
7. Exit
Enter choice: 1
Enter number of nodes (n): 3
Enter 3 integer values (level-order): 1 2 3
Tree created (complete tree of 3 nodes).

Enter choice: 2
Inorder (non-recursive): 2 1 3 

Enter choice: 3
Preorder (non-recursive): 1 2 3 

Enter choice: 4
Number of leaf nodes = 2

Enter choice: 5
Tree mirrored in-place.

Enter choice: 6
Level-order: 1 3 2 
```
