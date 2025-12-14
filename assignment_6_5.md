# Assignment No: 6.5

## Title
In a call center, customer calls are handled on a first-come, first-served basis. Implement a queue system using Linked list where:
• Each customer call is enqueued as it arrives.
• Customer service agents dequeue calls to assist customers.
If there are no calls, the system waits.

## Code

```cpp
#include <iostream.h>
#include <conio.h>
#include <string.h>

struct Node
{
    char name[20];
    Node *next;
};

Node *front = NULL;
Node *rear = NULL;

/* Enqueue */
void enqueue(char name[])
{
    Node *temp = new Node;
    strcpy(temp->name, name);
    temp->next = NULL;

    if (front == NULL)
        front = rear = temp;
    else
    {
        rear->next = temp;
        rear = temp;
    }
}

/* Dequeue */
void dequeue()
{
    if (front == NULL)
    {
        cout << "Queue Empty\n";
        return;
    }

    Node *temp = front;
    cout << "Serving: " << front->name << endl;
    front = front->next;

    if (front == NULL)
        rear = NULL;

    delete temp;
}

/* Display */
void display()
{
    Node *temp = front;
    if (temp == NULL)
    {
        cout << "Queue Empty\n";
        return;
    }

    while (temp != NULL)
    {
        cout << temp->name << " ";
        temp = temp->next;
    }
    cout << endl;
}

/* -------- MAIN -------- */
int main()
{
    int ch;
    char name[20];
    clrscr();

    do
    {
        cout << "\n1.Enqueue\n2.Dequeue\n3.Display\n4.Exit\n";
        cout << "Choice: ";
        cin >> ch;

        if (ch == 1)
        {
            cout << "Enter name: ";
            cin >> name;
            enqueue(name);
        }
        else if (ch == 2)
            dequeue();
        else if (ch == 3)
            display();

    } while (ch != 4);

    return 0;
}
```

## Output

```text
Call Center Queue Menu
1. Add Customer Call (Enqueue)
2. Serve Next Call (Dequeue)
3. Display All Calls
4. Exit
Enter your choice: 1
Enter customer name: Karan
Call from Karan added to the queue.

Enter your choice: 2
Serving call of: Karan
```
