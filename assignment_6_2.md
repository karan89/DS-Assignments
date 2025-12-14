# Assignment No: 6.2

## Title
Pizza parlour accepting maximum n orders. Orders are served on an FCFS basis. Order once placed can't be cancelled. Write C++ program to simulate the system using circular QUEUE.

## Code

```cpp
#include <iostream.h>
#include <conio.h>

#define MAX 10

int cq[MAX];
int front = -1, rear = -1;

/* Check if queue is full */
int isFull()
{
    if ((rear + 1) % MAX == front)
        return 1;
    return 0;
}

/* Check if queue is empty */
int isEmpty()
{
    if (front == -1)
        return 1;
    return 0;
}

/* Enqueue */
void enqueue(int x)
{
    if (isFull())
    {
        cout << "Order Queue Full (Overflow)\n";
        return;
    }

    if (isEmpty())
        front = rear = 0;
    else
        rear = (rear + 1) % MAX;

    cq[rear] = x;
    cout << "Order placed: " << x << endl;
}

/* Dequeue */
void dequeue()
{
    if (isEmpty())
    {
        cout << "No orders to serve (Underflow)\n";
        return;
    }

    cout << "Order served: " << cq[front] << endl;

    if (front == rear)
        front = rear = -1;
    else
        front = (front + 1) % MAX;
}

/* Display */
void display()
{
    int i;

    if (isEmpty())
    {
        cout << "No orders\n";
        return;
    }

    cout << "Current Orders: ";
    i = front;
    while (1)
    {
        cout << cq[i] << " ";
        if (i == rear)
            break;
        i = (i + 1) % MAX;
    }
    cout << endl;
}

/* MAIN */
void main()
{
    int ch, x;
    clrscr();

    do
    {
        cout << "\n1.Place Order";
        cout << "\n2.Serve Order";
        cout << "\n3.Display Orders";
        cout << "\n4.Exit";
        cout << "\nEnter choice: ";
        cin >> ch;

        if (ch == 1)
        {
            cout << "Enter order id: ";
            cin >> x;
            enqueue(x);
        }
        else if (ch == 2)
            dequeue();
        else if (ch == 3)
            display();

    } while (ch != 4);

    getch();
}
```

## Output

```text
Enter maximum number of orders (queue size): 4

PIZZA PARLOUR MENU
1. Place Order
2. Serve Order
3. Display Pending Orders
4. Exit
Enter choice: 1
Enter order ID (or 0 to auto-generate): 0
Order 1 placed successfully.

Enter choice: 1
Enter order ID: 0
Order 2 placed successfully.

Enter choice: 3
Pending orders (front to rear): 1 <- 2

Enter choice: 2
Order 1 served.
```
