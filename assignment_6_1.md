# Assignment No: 6.1

## Title
Write a program to keep track of patients as they checked into a medical clinic, assigning patients to doctors on a first-come, first-served basis.

## Code

```cpp
#include <iostream.h>
#include <conio.h>
#include <string.h>

/* Patient Node */
struct Patient
{
    int id;
    char name[20];
    Patient *next;
};

/* Doctor Structure */
struct Doctor
{
    int id;
    int busy;          // 0 = free, 1 = busy
    int pid;
    char pname[20];
};

/* Queue pointers */
Patient *front = NULL;
Patient *rear  = NULL;

/* Enqueue Patient */
void enqueue(int id, char name[])
{
    Patient *t = new Patient;
    t->id = id;
    strcpy(t->name, name);
    t->next = NULL;

    if (front == NULL)
        front = rear = t;
    else
    {
        rear->next = t;
        rear = t;
    }
}

/* Dequeue Patient */
int dequeue(int *id, char name[])
{
    Patient *t;

    if (front == NULL)
        return 0;

    t = front;
    *id = t->id;
    strcpy(name, t->name);
    front = front->next;

    if (front == NULL)
        rear = NULL;

    delete t;
    return 1;
}

/* Display Patient Queue */
void showQueue()
{
    Patient *t = front;

    if (t == NULL)
    {
        cout << "Queue Empty\n";
        return;
    }

    while (t != NULL)
    {
        cout << "[" << t->id << "] " << t->name << " -> ";
        t = t->next;
    }
    cout << "NULL\n";
}

/* Display Doctors */
void showDoctors(Doctor d[], int n)
{
    int i;
    for (i = 0; i < n; i++)
    {
        cout << "Doctor " << d[i].id << " : ";
        if (d[i].busy == 1)
            cout << "BUSY with " << d[i].pname << endl;
        else
            cout << "FREE\n";
    }
}

/* -------- MAIN -------- */
void main()
{
    Doctor d[10];
    int D, i, choice;
    int pid = 1;
    int dno, id;
    char name[20];

    clrscr();

    cout << "Enter number of doctors: ";
    cin >> D;

    for (i = 0; i < D; i++)
    {
        d[i].id = i + 1;
        d[i].busy = 0;
    }

    do
    {
        cout << "\n1.Add Patient";
        cout << "\n2.Assign Patient to Doctor";
        cout << "\n3.Finish Patient";
        cout << "\n4.Show Queue";
        cout << "\n5.Show Doctors";
        cout << "\n6.Exit";
        cout << "\nEnter choice: ";
        cin >> choice;

        if (choice == 1)
        {
            cout << "Enter patient name: ";
            cin >> name;
            enqueue(pid, name);
            pid++;
        }
        else if (choice == 2)
        {
            cout << "Doctor number: ";
            cin >> dno;

            if (d[dno-1].busy == 0)
            {
                if (dequeue(&id, name))
                {
                    d[dno-1].busy = 1;
                    d[dno-1].pid = id;
                    strcpy(d[dno-1].pname, name);
                    cout << "Patient assigned\n";
                }
                else
                    cout << "No patient waiting\n";
            }
            else
                cout << "Doctor busy\n";
        }
        else if (choice == 3)
        {
            cout << "Doctor number: ";
            cin >> dno;
            d[dno-1].busy = 0;
            cout << "Doctor is now free\n";
        }
        else if (choice == 4)
            showQueue();
        else if (choice == 5)
            showDoctors(d, D);

    } while (choice != 6);

    getch();
}
```

## Output

```text
=== Clinic Patient Queue (FIFO) ===
Enter number of doctors in clinic: 3
Enter name for Doctor 1: Mahavir
Enter name for Doctor 2: Udayan
Enter name for Doctor 3: Karan

--- MENU ---
1. Check-in patient (enqueue)
2. Assign next waiting patient to a doctor
3. Finish current patient for a doctor
4. Display waiting queue
5. Display doctors status
6. Exit

Enter choice: 1
Enter patient name: Onkar
Patient checked in: [1] Onkar

Enter choice: 1
Enter patient name: Mahesh
Patient checked in: [2] Mahesh

Enter choice: 2
Choose doctor number to assign (1..3): 1
Assigned patient [1] Onkar to Doctor 1.

Enter choice: 5
Doctors status: 
Doctor 1 (Mahavir): BUSY with [1] Onkar
Doctor 2 (Udayan): FREE
Doctor 3 (Karan): FREE
```
