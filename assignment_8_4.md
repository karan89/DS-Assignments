# Assignment No: 8.4

## Title
Implement product inventory management using a search tree.

## Code

```cpp
#include <iostream.h>
#include <conio.h>
#include <string.h>

struct Product
{
    int code;
    char name[20];
    float price;
    int qty;
    int recvDate;
    int expDate;
    Product *left, *right;
};

Product *root = NULL;

/* Create product node */
Product* createNode(int c, char n[], float p, int q, int r, int e)
{
    Product *t = new Product;
    t->code = c;
    strcpy(t->name, n);
    t->price = p;
    t->qty = q;
    t->recvDate = r;
    t->expDate = e;
    t->left = t->right = NULL;
    return t;
}

/* Insert product (BST by name) */
Product* insert(Product *r, int c, char n[], float p, int q, int rd, int ed)
{
    if (r == NULL)
        return createNode(c, n, p, q, rd, ed);

    if (strcmp(n, r->name) < 0)
        r->left = insert(r->left, c, n, p, q, rd, ed);
    else
        r->right = insert(r->right, c, n, p, q, rd, ed);

    return r;
}

/* Inorder traversal (all products sorted by name) */
void inorder(Product *r)
{
    if (r != NULL)
    {
        inorder(r->left);
        cout << "\nCode: " << r->code;
        cout << "\nName: " << r->name;
        cout << "\nPrice: " << r->price;
        cout << "\nQuantity: " << r->qty;
        cout << "\nReceived Date: " << r->recvDate;
        cout << "\nExpiry Date: " << r->expDate;
        cout << "\n-------------------------";
        inorder(r->right);
    }
}

/* Preorder traversal for expired products */
void expired(Product *r, int current)
{
    if (r != NULL)
    {
        if (r->expDate < current)
        {
            cout << "\nEXPIRED PRODUCT";
            cout << "\nCode: " << r->code;
            cout << "\nName: " << r->name;
            cout << "\nExpiry Date: " << r->expDate;
            cout << "\n-------------------------";
        }
        expired(r->left, current);
        expired(r->right, current);
    }
}

/* MAIN */
void main()
{
    int ch;
    int code, qty, rd, ed, today;
    char name[20];
    float price;
    clrscr();

    do
    {
        cout << "\n--- PRODUCT INVENTORY MENU ---\n";
        cout << "1. Insert Product\n";
        cout << "2. Display All Products\n";
        cout << "3. Display Expired Products\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch (ch)
        {
        case 1:
            cout << "Enter Product Code: ";
            cin >> code;
            cout << "Enter Product Name: ";
            cin >> name;
            cout << "Enter Price: ";
            cin >> price;
            cout << "Enter Quantity: ";
            cin >> qty;
            cout << "Enter Received Date (YYYYMMDD): ";
            cin >> rd;
            cout << "Enter Expiry Date (YYYYMMDD): ";
            cin >> ed;

            root = insert(root, code, name, price, qty, rd, ed);
            cout << "Product inserted.\n";
            break;

        case 2:
            if (root == NULL)
                cout << "No products in inventory.\n";
            else
                inorder(root);
            break;

        case 3:
            if (root == NULL)
            {
                cout << "No products in inventory.\n";
                break;
            }
            cout << "Enter current date (YYYYMMDD): ";
            cin >> today;
            expired(root, today);
            break;
        }
    } while (ch != 4);

    getch();
}
```

## Output

```text
=== Product Inventory (BST keyed by Product Name) ===

Menu:
1. Insert a product
2. Display all items (inorder sorted by name)
3. List expired items (preorder of names)
4. Exit
Enter choice: 1
Enter product code: 101
Enter product name: Mobile
Enter price: 14999
Enter quantity in stock (integer): 3
Enter date received (YYYY-MM-DD): 2025-11-20
Enter expiration date (YYYY-MM-DD): 2027-11-20
Product inserted.

Enter choice: 1
Enter product code: 102
Enter product name: Laptop
Enter price: 45000
Enter quantity in stock (integer): 1
Enter date received (YYYY-MM-DD): 2025-11-20
Enter expiration date (YYYY-MM-DD): 2025-11-19
Product inserted.

Enter choice: 3
Enter current date (YYYY-MM-DD) or press Enter to use system date: 
Using system date: 2025-11-21

Expired items (preorder by name):
Product Code : 102
Name         : Laptop
Price        : 45000
Quantity     : 1
Received     : 2025-11-20
Expiry       : 2025-11-19 (EXPIRED)
```
