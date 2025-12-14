# Assignment No: 5.3

## Title
Write a program to implement multiple stack i.e more than two stack using array and perform following operations on it.
A. Push B. Pop C. Stack Overflow D. Stack Underflow E. Display.

## Code

```cpp
#include<iostream.h>
#include<conio.h>
#include<stdlib.h>

/* Node structure */
struct Node {
    int data;
    Node *next;
};

/* Array of stack tops */
Node *top[10];

/* Push operation */
void push(int s, int x)
{
    Node *temp = new Node;
    temp->data = x;
    temp->next = top[s];
    top[s] = temp;
}

/* Pop operation */
void pop(int s)
{
    if (top[s] == NULL)
    {
        cout << "Stack Underflow\n";
        return;
    }
    Node *t = top[s];
    cout << "Popped element: " << t->data << endl;
    top[s] = t->next;
    delete t;
}

/* Display all stacks */
void display(int k)
{
    int i;
    Node *temp;
    for (i = 0; i < k; i++)
    {
        cout << "Stack " << i + 1 << ": ";
        temp = top[i];
        if (temp == NULL)
        {
            cout << "Empty";
        }
        else
        {
            while (temp != NULL)
            {
                cout << temp->data << " ";
                temp = temp->next;
            }
        }
        cout << endl;
    }
}

/* ---------- MAIN ---------- */
void main()
{
    int k, ch, s, x, i;
    clrscr();

    cout << "Enter number of stacks (<=10): ";
    cin >> k;

    if (k > 10)
    {
        cout << "Invalid number of stacks";
        return;
    }

    /* Initialize all stacks as empty */
    for (i = 0; i < k; i++)
        top[i] = NULL;

    do
    {
        cout << "\n1.Push\n2.Pop\n3.Display\n4.Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        if (ch == 1)
        {
            cout << "Enter stack number: ";
            cin >> s;

            if (s < 1 || s > k)
            {
                cout << "Invalid stack number\n";
                continue;
            }

            cout << "Enter value: ";
            cin >> x;
            push(s - 1, x);
        }
        else if (ch == 2)
        {
            cout << "Enter stack number: ";
            cin >> s;

            if (s < 1 || s > k)
            {
                cout << "Invalid stack number\n";
                continue;
            }

            pop(s - 1);
        }
        else if (ch == 3)
        {
            display(k);
        }

    } while (ch != 4);

    getch();
}
```

## Output

```text
Enter total array size N: 4
Enter number of stacks k (>1): 2

Configuration:
Total size N=4, stacks k = 2
Stack 1: base = 0, capacity = 2
Stack 2: base = 2, capacity = 2

MENU
...
Enter choice: 1
Enter stack number (1..2): 1
Enter value to push: 10
Pushed 10 into stack 1.

Enter choice: 1
Enter stack number (1..2): 2
Enter value to push: 20
Pushed 20 into stack 2.

Enter choice: 6
Stacks content (top shown first):
Stack 1: 10
Stack 2: 20
```
