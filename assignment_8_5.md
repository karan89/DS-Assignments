# Assignment No: 8.5

## Title
Implement deletion operations in the product inventory system (based on product code and expiration).

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

/* Create node */
Product* createNode(int c, char n[], float p, int q, int rd, int ed)
{
    Product *t = new Product;
    t->code = c;
    strcpy(t->name, n);
    t->price = p;
    t->qty = q;
    t->recvDate = rd;
    t->expDate = ed;
    t->left = t->right = NULL;
    return t;
}

/* Insert product */
Product* insert(Product *r, int c, char n[], float p, int q, int rd, int ed)
{
    if (r == NULL)
        return createNode(c, n, p, q, rd, ed);

    if (c < r->code)
        r->left = insert(r->left, c, n, p, q, rd, ed);
    else if (c > r->code)
        r->right = insert(r->right, c, n, p, q, rd, ed);
    else
        cout << "Duplicate product code not allowed.\n";

    return r;
}

/* Find minimum node */
Product* findMin(Product *r)
{
    while (r->left != NULL)
        r = r->left;
    return r;
}

/* Delete product by code */
Product* deleteProduct(Product *r, int code)
{
    if (r == NULL)
    {
        cout << "Product not found.\n";
        return r;
    }

    if (code < r->code)
        r->left = deleteProduct(r->left, code);
    else if (code > r->code)
        r->right = deleteProduct(r->right, code);
    else
    {
        // Case 1: 0 or 1 child
        if (r->left == NULL)
        {
            Product *temp = r->right;
            delete r;
            return temp;
        }
        else if (r->right == NULL)
        {
            Product *temp = r->left;
            delete r;
            return temp;
        }

        // Case 2: 2 children
        Product *t = findMin(r->right);
        r->code = t->code;
        strcpy(r->name, t->name);
        r->price = t->price;
        r->qty = t->qty;
        r->recvDate = t->recvDate;
        r->expDate = t->expDate;
        r->right = deleteProduct(r->right, t->code);
    }
    return r;
}

/* Display inventory (inorder) */
void inorder(Product *r)
{
    if (r != NULL)
    {
        inorder(r->left);
        cout << "\nCode: " << r->code;
        cout << "\nName: " << r->name;
        cout << "\nPrice: " << r->price;
        cout << "\nQuantity: " << r->qty;
        cout << "\nReceived: " << r->recvDate;
        cout << "\nExpiry: " << r->expDate;
        cout << "\n-------------------------";
        inorder(r->right);
    }
}

/* Delete expired products (Post-order traversal) */
Product* deleteExpired(Product *r, int today)
{
    if (r == NULL)
        return NULL;

    r->left = deleteExpired(r->left, today);
    r->right = deleteExpired(r->right, today);

    if (r->expDate < today)
    {
        // Recursive delete call
        r = deleteProduct(r, r->code);
    }

    return r;
}

/* MAIN */
void main()
{
    int ch, code, qty, rd, ed, today;
    char name[20];
    float price;
    clrscr();

    do
    {
        cout << "\n--- PRODUCT DELETION MENU ---\n";
        cout << "1. Insert Product\n";
        cout << "2. Display Products\n";
        cout << "3. Delete Product by Code\n";
        cout << "4. Delete Expired Products\n";
        cout << "5. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch (ch)
        {
        case 1:
            cout << "Enter Product Code: ";
            cin >> code;
            cout << "Enter Name: ";
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
            break;

        case 2:
            if (root == NULL)
                cout << "Inventory empty.\n";
            else
                inorder(root);
            break;

        case 3:
            cout << "Enter Product Code to delete: ";
            cin >> code;
            root = deleteProduct(root, code);
            break;

        case 4:
            cout << "Enter current date (YYYYMMDD): ";
            cin >> today;
            root = deleteExpired(root, today);
            cout << "Expired products deleted.\n";
            break;
        }
    } while (ch != 5);

    getch();
}

```

## Output

```text
=== Product Inventory: Deletion Operations (BST keyed by product code) ===

Menu:
1. Insert a product
2. Display all products (inorder)
3. Delete a product by code
4. Delete all expired products
5. Exit
Enter choice: 1
Enter product code (unique): 101
Enter product name: Mobile
Enter price: 15999
Enter quantity (integer): 4
Enter date received (YYYY-MM-DD): 2025-11-21
Enter expiration date (YYYY-MM-DD): 2027-11-21
Inserted/Updated.

Enter choice: 1
Enter product code (unique): 102
Enter product name: Laptop
Enter price: 50000
Enter quantity (integer): 1
Enter date received (YYYY-MM-DD): 2025-11-21
Enter expiration date (YYYY-MM-DD): 2025-11-20
Inserted/Updated.

Enter choice: 2
------
Code     : 101
Name     : Mobile
Price    : 15999
Qty      : 4
Received : 2025-11-21
Expiry   : 2027-11-21
------
Code     : 102
Name     : Laptop
Price    : 50000
Qty      : 1
Received : 2025-11-21
Expiry   : 2025-11-20

Enter choice: 3
Enter code: 101
Deleted product if existed.

Enter choice: 4
Enter date (YYYY-MM-DD) or press Enter: 
Expired items removed.
```
