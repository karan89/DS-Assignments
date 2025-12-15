# Assignment No: 3.1

## Title
Implementation of Singly Linked List to Manage 'Vertex Club' Membership Records. The Department of Computer Engineering has a student club named 'Vertex Club' for second, third, and final year students. The first member is the President and the last member is the Secretary. Write a C++ program to:
- Add/delete members (including President/Secretary)
- Count members
- Display members
- Concatenate two division lists
- Also implement: reverse, search by PRN, and sort by PRN operations.

## Code

```cpp
#include<iostream.h>
#include<conio.h>
#include<string.h>
#include<stdlib.h>

struct Node {
    int prn;
    char name[20];
    Node* next;

    Node(int p, char n[]) {
        prn = p;
        strcpy(name, n);
        next = NULL;
    }
};

class Club {
    Node* head;

public:
    Club() { 
        head = NULL; 
    }

    void addPresident(int prn, char name[]) {
        Node* newNode = new Node(prn, name);
        newNode->next = head;
        head = newNode;
        cout<<"President added successfully.\n";
    }

    void addSecretary(int prn, char name[]) {
        Node* newNode = new Node(prn, name);
        if(!head) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while(temp->next != NULL){ 
            temp = temp->next;
        }
        temp->next = newNode;
        cout<<"Secretary added successfully.\n";
    }

    void addMember(int prn, char name[]) {
        if(!head) {
            cout<<"No President found. Add President first.\n";
            return;
        }
        Node* newNode = new Node(prn, name);
        Node* temp = head;

        if(head->next == NULL) {
            head->next = newNode;
            return;
        }

        while(temp->next->next != NULL) {
            temp = temp->next;
        }
        newNode->next = temp->next;
        temp->next = newNode;
        cout<<"Member added successfully.\n";
    }

    void deleteMember(int prn) {
        if(!head) {
            cout<<"Club list is empty.\n";
            return;
        }
        Node* temp = head;
        Node* prev = NULL;

        if(head->prn == prn) {
            head = head->next;
            delete temp;
            cout<<"President deleted successfully.\n";
            return;
        }

        while(temp != NULL && temp->prn != prn) {
            prev = temp;
            temp = temp->next;
        }

        if(temp == NULL) {
            cout<<"Member not found.\n";
            return;
        }

        prev->next = temp->next;
        cout<<"Member deleted successfully.\n";
        delete temp;
    }

    int countMembers() {
        int count = 0;
        Node* temp = head;
        while(temp != NULL) {
            count++;
            temp = temp->next;
        }
        return count;
    }

    void display() {
        if (head == NULL) {
            cout<<"No members in the club.\n";
            return;
        }
        cout<<"\nClub Members:\n";
        Node* temp = head;
        int i = 1;
        while(temp != NULL) {
            cout<<i<< ". PRN: " << temp->prn << ", Name: " << temp->name;
            if (temp == head)
                cout << "(Pre)";
            else if (temp->next == NULL)
                cout << "(Sec)";
            cout<<"\n";
            temp = temp->next;
            i++;
        }
    }

    void reverse() {
        Node* prev = NULL;
        Node* temp = head;
        Node* next = NULL;
        while(temp != NULL) {
            next = temp->next;
            temp->next = prev;
            prev = temp;
            temp = next;
        }
        head = prev;
        cout<<"Club list reversed.\n";
    }

    void search(int prn) {
        Node* temp = head;
        while(temp != NULL) {
            if(temp->prn == prn) {
                cout<<"Member found: "<<temp->name<<" PRN: "<<prn<<" \n";
                return;
            }
            temp = temp->next;
        }
        cout<<"Member not found.\n";
    }

    void sortByPRN() {
        if(head == NULL || head->next == NULL) return;

        Node* i;
        Node* j;
        int tempPrn;
        char tempName[20];

        for(i = head; i != NULL; i = i->next) {
            for(j = i->next; j != NULL; j = j->next) {
                if (i->prn > j->prn) {
                    // Swap PRN
                    tempPrn = i->prn;
                    i->prn = j->prn;
                    j->prn = tempPrn;
                    
                    // Swap Name
                    strcpy(tempName, i->name);
                    strcpy(i->name, j->name);
                    strcpy(j->name, tempName);
                }
            }
        }
        cout<<"Club members sorted by PRN.\n";
    }

    // Needed for concatenation logic in main
    Node* getHead() { return head; }
    void setHead(Node* h) { head = h; }
};

int main() {
    Club div;
    int choice,prn,div1_n,div2_n,i;
    char name[20];

    // Variables for concatenation
    Club div1, div2; 
    
    clrscr();

    do {
        cout << "\n--- Vertex Club Menu ---\n";
        cout << "1. Add President\n2. Add Secretary\n3. Add Member\n4. Delete Member\n5. Display Members\n";
        cout << "6. Count Members\n7. Concatenate Division Lists\n8. Reverse List\n9. Search by PRN\n10. Sort by PRN\n0. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter PRN and Name: ";
                cin >> prn >> name;
                div.addPresident(prn, name);
                break;

            case 2:
                cout << "Enter PRN and Name: ";
                cin >> prn >> name;
                div.addSecretary(prn, name);
                break;

            case 3:
                cout << "Enter PRN and Name: ";
                cin >> prn >> name;
                div.addMember(prn, name);
                break;

            case 4:
                cout << "Enter PRN to delete: ";
                cin >> prn;
                div.deleteMember(prn);
                break;

            case 5:
                div.display();
                break;

            case 6:
                cout<<"Total members: "<<div.countMembers()<<endl;
                break;

            case 7:
                // Simplified concatenation for Turbo C logic
                cout<<"Enter the total number of members in div 1 list: ";
                cin>>div1_n;
                cout<<"Enter the details div 1 (PRN Name):\n";
                for(i=0;i<div1_n;i++) {
                    cin>>prn>>name;
                    div1.addSecretary(prn, name); // Using addSecretary to append
                }

                cout<<"Enter the total number of members in div 2 list: ";
                cin>>div2_n;
                cout<<"Enter the details div 2 (PRN Name):\n";
                for(i=0;i<div2_n;i++) {
                    cin>>prn>>name;
                    div2.addSecretary(prn, name);
                }

                // Concatenate Logic
                if(div1.getHead() == NULL) {
                    div1.setHead(div2.getHead());
                } else {
                    Node* temp = div1.getHead();
                    while (temp->next != NULL) {
                        temp = temp->next;
                    }
                    temp->next = div2.getHead();
                }
                
                cout<<"\nAfter concatenation, the combined list is:\n";
                div1.display();
                break;

            case 8:
                div.reverse();
                break;

            case 9:
                cout<<"Enter PRN to search: ";
                cin>>prn;
                div.search(prn);
                break;

            case 10:
                div.sortByPRN();
                break;

            case 0:
                cout<<"Exiting...\n";
                break;

            default:
                cout<<"Invalid choice!\n";
        }
    } while (choice != 0);

    return 0;
}

```

## Output

```text
Vertex Club Menu
1. Add President
2. Add Secretary
3. Add Member
4. Delete Member
5. Display Members
6. Count Members
7. Concatenate Division Lists
8. Reverse List
9. Search by PRN
10. Sort by PRN
0. Exit
Enter choice: 1
Enter PRN and Name: 101 Karan
President added successfully.

Enter choice: 3
Enter PRN and Name: 205 Rahul
Member added successfully.

Enter choice: 2
Enter PRN and Name: 309 Manoj
Secretary added successfully.

Enter choice: 5
Club Members:
1. PRN: 101, Name: Karan (Pre)
2. PRN: 205, Name: Rahul
3. PRN: 309, Name: Manoj (Sec)

Enter choice: 6
Total members: 3

Enter choice: 9
Enter PRN to search: 205
Member found: Rahul PRN: 205

Enter choice: 10
Club members sorted by PRN.

Enter choice: 5
Club Members:
1. PRN: 101, Name: Karan (Pre)
2. PRN: 205, Name: Rahul
3. PRN: 309, Name: Manoj (Sec)

Enter choice: 8
Club list reversed.

Enter choice: 5
Club Members:
1. PRN: 309, Name: Manoj (Pre)
2. PRN: 205, Name: Rahul
3. PRN: 101, Name: Karan (Sec)
```
