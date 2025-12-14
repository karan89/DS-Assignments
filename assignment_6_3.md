# Assignment No: 6.3

## Title
Write a program that maintains a queue of passengers waiting to see a ticket agent. The program user should be able to insert a new passenger at the rear of the queue, Display the passenger at the front of the Queue, or remove the passenger at the front of the queue. The program will display the number of passengers left in the queue just before it terminates.

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
Node *rear  = NULL;
int count = 0;

/* Enqueue */
void enqueue(char name[])
{
    Node *t = new Node;
    strcpy(t->name, name);
    t->next = NULL;

    if (front == NULL)
        front = rear = t;
    else
    {
        rear->next = t;
        rear = t;
    }
    count++;
}

/* Dequeue */
void dequeue()
{
    Node *t;

    if (front == NULL)
    {
        cout << "Queue Empty\n";
        return;
    }

    t = front;
    cout << "Removed: " << t->name << endl;
    front = front->next;

    if (front == NULL)
        rear = NULL;

    delete t;
    count--;
}

/* Show front */
void showFront()
{
    if (front == NULL)
        cout << "Queue Empty\n";
    else
        cout << "Front: " << front->name << endl;
}

/* MAIN */
void main()
{
    int ch;
    char name[20];
    clrscr();

    do
    {
        cout << "\n1.Enqueue";
        cout << "\n2.Dequeue";
        cout << "\n3.Show Front";
        cout << "\n4.Exit";
        cout << "\nChoice: ";
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
            showFront();

    } while (ch != 4);

    cout << "\nPassengers left in queue: " << count;

    getch();
}
```

## Output

```text
Passenger Queue Menu
1. Insert new passenger
2. Show front passenger
3. Remove front passenger
4. Exit
Enter choice: 1
Enter passenger name: Mahavir
Mahavir added to the queue.

Enter choice: 1
Enter passenger name: Udayan
Udayan added to the queue.

Enter choice: 2
Front passenger: Mahavir

Enter choice: 3
Removing: Mahavir

Enter choice: 4
Program ending...
Passengers left in queue: 1
```
