# Assignment No: 6.4

## Title
Write a program to implement multiple queues i.e. two queues using array and perform following operations on it. A. Add Queue, B. Delete from Queue, C. Display Queue.

## Code

```cpp
#include <iostream.h>
#include <conio.h>

#define MAX 10

int q1[MAX], q2[MAX];
int f1 = -1, r1 = -1;
int f2 = -1, r2 = -1;

/* Enqueue Queue 1 */
void enqueue1(int x)
{
    if (r1 == MAX - 1)
    {
        cout << "Queue 1 Overflow\n";
        return;
    }
    if (f1 == -1)
        f1 = 0;
    q1[++r1] = x;
}

/* Enqueue Queue 2 */
void enqueue2(int x)
{
    if (r2 == MAX - 1)
    {
        cout << "Queue 2 Overflow\n";
        return;
    }
    if (f2 == -1)
        f2 = 0;
    q2[++r2] = x;
}

/* Dequeue Queue 1 */
void dequeue1()
{
    if (f1 == -1 || f1 > r1)
    {
        cout << "Queue 1 Underflow\n";
        return;
    }
    cout << "Deleted: " << q1[f1++] << endl;
}

/* Dequeue Queue 2 */
void dequeue2()
{
    if (f2 == -1 || f2 > r2)
    {
        cout << "Queue 2 Underflow\n";
        return;
    }
    cout << "Deleted: " << q2[f2++] << endl;
}

/* Display Queue 1 */
void display1()
{
    int i;
    if (f1 == -1 || f1 > r1)
    {
        cout << "Queue 1 Empty\n";
        return;
    }
    for (i = f1; i <= r1; i++)
        cout << q1[i] << " ";
    cout << endl;
}

/* Display Queue 2 */
void display2()
{
    int i;
    if (f2 == -1 || f2 > r2)
    {
        cout << "Queue 2 Empty\n";
        return;
    }
    for (i = f2; i <= r2; i++)
        cout << q2[i] << " ";
    cout << endl;
}

/* MAIN */
void main()
{
    int ch, qno, x;
    clrscr();

    do
    {
        cout << "\n1.Enqueue";
        cout << "\n2.Dequeue";
        cout << "\n3.Display";
        cout << "\n4.Exit";
        cout << "\nChoice: ";
        cin >> ch;

        if (ch == 4)
            break;

        cout << "Select Queue (1 or 2): ";
        cin >> qno;

        if (ch == 1)
        {
            cout << "Enter value: ";
            cin >> x;
            if (qno == 1) enqueue1(x);
            else enqueue2(x);
        }
        else if (ch == 2)
        {
            if (qno == 1) dequeue1();
            else dequeue2();
        }
        else if (ch == 3)
        {
            if (qno == 1) display1();
            else display2();
        }

    } while (1);

    getch();
}











// #include <iostream.h>
// #include <conio.h>

// /* Node structure */
// struct Node
// {
//     int data;
//     Node *next;
// };

// /* Queue 1 */
// Node *f1 = NULL;
// Node *r1 = NULL;

// /* Queue 2 */
// Node *f2 = NULL;
// Node *r2 = NULL;

// /* Enqueue Queue 1 */
// void enqueue1(int x)
// {
//     Node *t = new Node;
//     t->data = x;
//     t->next = NULL;

//     if (f1 == NULL)
//         f1 = r1 = t;
//     else
//     {
//         r1->next = t;
//         r1 = t;
//     }
// }

// /* Enqueue Queue 2 */
// void enqueue2(int x)
// {
//     Node *t = new Node;
//     t->data = x;
//     t->next = NULL;

//     if (f2 == NULL)
//         f2 = r2 = t;
//     else
//     {
//         r2->next = t;
//         r2 = t;
//     }
// }

// /* Dequeue Queue 1 */
// void dequeue1()
// {
//     Node *t;

//     if (f1 == NULL)
//     {
//         cout << "Queue Empty\n";
//         return;
//     }

//     t = f1;
//     cout << "Deleted: " << t->data << endl;
//     f1 = f1->next;

//     if (f1 == NULL)
//         r1 = NULL;

//     delete t;
// }

// /* Dequeue Queue 2 */
// void dequeue2()
// {
//     Node *t;

//     if (f2 == NULL)
//     {
//         cout << "Queue Empty\n";
//         return;
//     }

//     t = f2;
//     cout << "Deleted: " << t->data << endl;
//     f2 = f2->next;

//     if (f2 == NULL)
//         r2 = NULL;

//     delete t;
// }

// /* Display Queue 1 */
// void display1()
// {
//     Node *t = f1;

//     if (t == NULL)
//     {
//         cout << "Queue Empty\n";
//         return;
//     }

//     while (t != NULL)
//     {
//         cout << t->data << " ";
//         t = t->next;
//     }
//     cout << endl;
// }

// /* Display Queue 2 */
// void display2()
// {
//     Node *t = f2;

//     if (t == NULL)
//     {
//         cout << "Queue Empty\n";
//         return;
//     }

//     while (t != NULL)
//     {
//         cout << t->data << " ";
//         t = t->next;
//     }
//     cout << endl;
// }

// /* -------- MAIN -------- */
// void main()
// {
//     int ch, qno, x;

//     clrscr();

//     do
//     {
//         cout << "\n1.Enqueue";
//         cout << "\n2.Dequeue";
//         cout << "\n3.Display";
//         cout << "\n4.Exit";
//         cout << "\nChoice: ";
//         cin >> ch;

//         if (ch == 4)
//             break;

//         cout << "Select Queue (1 or 2): ";
//         cin >> qno;

//         if (ch == 1)
//         {
//             cout << "Enter value: ";
//             cin >> x;

//             if (qno == 1) enqueue1(x);
//             else enqueue2(x);
//         }
//         else if (ch == 2)
//         {
//             if (qno == 1) dequeue1();
//             else dequeue2();
//         }
//         else if (ch == 3)
//         {
//             if (qno == 1) display1();
//             else display2();
//         }

//     } while (1);

//     getch();
// }
```

## Output

```text
Enter size of each queue: 4

Multiple Queue Menu
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Exit
Enter choice: 1
Select Queue (1 or 2): 1
Enter value to add: 10
10 added to queue.

Enter choice: 1
Select Queue (1 or 2): 2
Enter value to add: 11
11 added to queue.

Enter choice: 3
Select Queue (1 or 2): 1
Queue elements: 10 
```
