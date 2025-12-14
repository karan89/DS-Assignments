# Assignment No: 5.1

## Title
WAP to build a simple stock price tracker that keeps a history of daily stock prices entered by the user. To allow users to go back and view or remove the most recent price, implement a stack using a linked list to store these integer prices.

Implement the following operations:
1. record(price) - Add a new stock price (an integer) to the stack.
2. remove()- Remove and return the most recent price (top of the stack).
3. latest()-Return the most recent stock price without removing it.
4. isEmpty()- Check if there are no prices recorded.

## Code

```cpp
#include<iostream.h>
#include<conio.h>

struct Node
{
    int price;
    Node *next;
};

Node *top = NULL;

/* record(price) -> push */
void record(int price)
{
    Node *temp = new Node;
    temp->price = price;
    temp->next = top;
    top = temp;
}

/* remove() -> pop */
void removePrice()
{
    if (top == NULL)
    {
        cout << "Stack Empty\n";
        return;
    }

    Node *temp = top;
    cout << "Removed price: " << top->price << endl;
    top = top->next;
    delete temp;
}

/* latest() -> peek */
void latest()
{
    if (top == NULL)
        cout << "No prices recorded\n";
    else
        cout << "Latest price: " << top->price << endl;
}

/* isEmpty() */
void isEmpty()
{
    if (top == NULL)
        cout << "Stack is Empty\n";
    else
        cout << "Stack is NOT Empty\n";
}

/* Display stack */
void display()
{
    Node *t = top;
    if (top == NULL)
    {
        cout << "No prices to display\n";
        return;
    }

    cout << "Prices: ";
    while (t != NULL)
    {
        cout << t->price << " ";
        t = t->next;
    }
    cout << endl;
}

/* -------- MAIN -------- */
void main()
{
    int ch, price;
    clrscr();

    do
    {
        cout << "\n1.Record Price\n2.Remove Price\n3.Latest Price\n4.Is Empty\n5.Display\n6.Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch (ch)
        {
            case 1:
                cout << "Enter price: ";
                cin >> price;
                record(price);
                break;

            case 2:
                removePrice();
                break;

            case 3:
                latest();
                break;

            case 4:
                isEmpty();
                break;

            case 5:
                display();
                break;
        }

    } while (ch != 6);
}
```

## Output

```text
MENU
1. Record new price
2. Remove most recent price
3. Show latest price
4. Check if empty
5. Display all prices
6. Exit
Enter choice: 1
Enter price: 120

Enter choice: 3
Latest price: 120

Enter choice: 4
Stack is NOT empty.

Enter choice: 5
Prices (top to bottom): 120 

Enter choice: 1
Enter price: 150

Enter choice: 5
Prices (top to bottom): 150 120
```
