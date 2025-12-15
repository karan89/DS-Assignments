# Assignment No: 3.4

## Title
In the Second Year Computer Engineering class, there are two groups of students based on their favorite sports:
Set A includes students who like Cricket.
Set B includes students who like Football.
Write a C++ program to represent these two sets using linked lists and perform the following operations:
a) Find and display the set of students who like both Cricket and Football.
b) Find and display the set of students who like either Cricket or Football, but not both.
c) Display the number of students who like neither Cricket nor Football.

## Code

```cpp
#include <iostream.h>
#include <conio.h>
#include <string.h>

struct CricketNode {
    char sname[20];
    CricketNode* next;

    CricketNode(char nm[]) {
        strcpy(sname, nm);
        next = NULL;
    }
};

struct FootballNode {
    char sname[20];
    FootballNode* next;

    FootballNode(char nm[]) {
        strcpy(sname, nm);
        next = NULL;
    }
};

class VITCollege {
    CricketNode* head1;
    FootballNode* head2;

public:
    VITCollege() {
        head1 = NULL;
        head2 = NULL;
    }

    void insertCricket(char name[]) {
        CricketNode* newNode = new CricketNode(name);
        if (!head1) {
            head1 = newNode;
            return;
        }
        CricketNode* temp = head1;
        while (temp->next) temp = temp->next;
        temp->next = newNode;
    }

    void insertFootball(char name[]) {
        FootballNode* newNode = new FootballNode(name);
        if (!head2) {
            head2 = newNode;
            return;
        }
        FootballNode* temp = head2;
        while (temp->next) temp = temp->next;
        temp->next = newNode;
    }

    // Helper: check if name in Cricket list
    int inCricket(char name[]) {
        CricketNode* t = head1;
        while (t) {
            if (strcmp(t->sname, name) == 0) return 1;
            t = t->next;
        }
        return 0;
    }

    // Helper: check if name in Football list
    int inFootball(char name[]) {
        FootballNode* t = head2;
        while (t) {
            if (strcmp(t->sname, name) == 0) return 1;
            t = t->next;
        }
        return 0;
    }

    void bothCriFoot() {
        cout << "\n\tStudents who like BOTH Cricket and Football:\n";
        int found = 0;

        CricketNode* c = head1;
        while (c) {
            if (inFootball(c->sname)) {
                cout << "  " << c->sname << endl;
                found = 1;
            }
            c = c->next;
        }

        if (!found) cout << "  None\n";
    }

    void eitherButNotBoth() {
        cout << "\n\tStudents who like EITHER Cricket or Football BUT NOT BOTH:\n";
        int found = 0;

        CricketNode* c = head1;
        while (c) {
            if (!inFootball(c->sname)) {
                cout << "  " << c->sname << endl;
                found = 1;
            }
            c = c->next;
        }

        FootballNode* f = head2;
        while (f) {
            if (!inCricket(f->sname)) {
                cout << "  " << f->sname << endl;
                found = 1;
            }
            f = f->next;
        }

        if (!found) cout << "  None\n";
    }

    void neither(int total) {
        cout << "\n\tStudents who like NEITHER Cricket nor Football:\n";

        char name[20];
        int found = 0;
        int i;

        for (i = 0; i < total; i++) {
            cout << "Enter student name: ";
            cin >> name;

            if (!inCricket(name) && !inFootball(name)) {
                cout << "  " << name << endl;
                found = 1;
            }
        }

        if (!found) cout << "  None\n";
    }
};

int main() {
    VITCollege clg;
    int total, n, ch, i;
    char name[20];
    clrscr();

    cout << "Enter total number of students: ";
    cin >> total;

    cout << "\nEnter number of students who like Cricket: ";
    cin >> n;
    cout << "Enter names:\n";
    for (i = 0; i < n; i++) {
        cin >> name;
        clg.insertCricket(name);
    }

    cout << "\nEnter number of students who like Football: ";
    cin >> n;
    cout << "Enter names:\n";
    for (i = 0; i < n; i++) {
        cin >> name;
        clg.insertFootball(name);
    }

    do {
        cout << "\n\n=== Sports Preference Menu ===\n";
        cout << "1. Students who like BOTH Cricket and Football\n";
        cout << "2. Students who like EITHER Cricket or Football but NOT BOTH\n";
        cout << "3. Students who like NEITHER Cricket nor Football\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch (ch) {
            case 1:
                clg.bothCriFoot();
                break;
            case 2:
                clg.eitherButNotBoth();
                break;
            case 3:
                clg.neither(total);
                break;
            case 4:
                cout << "Exiting...\n";
                break;
            default:
                cout << "Invalid choice. Please try again.\n";
        }
    } while (ch != 4);

    return 0;
}

```

## Output

```text
Total students: 5
Enter number of students who like Cricket: 3
Enter names: 
Mahavir
Rahul
Aman

Enter number of students who like Football: 4
Enter names: 
Rahul
Rohit
Aman
Sahil

=== Sports Preference Menu ===
1. Students who like BOTH Cricket and Football
2. Students who like EITHER Cricket or Football but NOT BOTH
3. Students who like NEITHER Cricket nor Football
4. Exit

Enter choice: 1
    Students who like BOTH Cricket and Football:
 Rahul
 Aman

Enter choice: 2
    Students who like EITHER Cricket or Football BUT NOT BOTH:
 Mahavir
 Rohit
 Sahil

Enter choice: 3
(Checking for NEITHER...)
Enter student name: Meena
 -> Meena likes neither.
```
