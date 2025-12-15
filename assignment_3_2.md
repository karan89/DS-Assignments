# Assignment No: 3.2

## Title
The ticket reservation system for Galaxy Multiplex is to be implemented using a C++ program. The multiplex has 8 rows, with 8 seats in each row. A doubly circular linked list will be used to track the availability of seats in each row. Initially, assume that some seats are randomly booked. An array will store head pointers for each row's linked list. The system should support the following operations:
a) Display the current list of available seats.
b) Book one or more seats as per customer request.
c) Cancel an existing booking when requested.

## Code

```cpp
#include <iostream.h>
#include <conio.h>

struct Seat {
    int seatNum;
    int booked; // 0 for false, 1 for true
    Seat* next;
    Seat* prev;
};

class Galaxy {
    Seat* head;
    Seat* prevNode;
    public:
    Galaxy() {
        head = NULL;
        prevNode = NULL;
        int i, j;
        for(i=1; i<=8; i++) {
            for(j=1;j<=8;j++) {
                Seat* newSeat = new Seat();
                newSeat->seatNum = j;
                newSeat->booked = 0; // false
                newSeat->next = NULL;
                newSeat->prev = NULL;
                
                if(head == NULL) {
                    head = newSeat;
                    prevNode = newSeat;
                }
                else {
                    prevNode->next = newSeat;
                    newSeat->prev = prevNode;
                    prevNode = newSeat;
                }
            }
        }
    }

    void displaySeats() {
        Seat* temp = head;
        int i, j;
        for(i=1;i<=8;i++) {
            cout<<"Row "<<i<<": ";
            for(j=1;j<=8;j++) {
                if(temp->booked) {
                    cout<<"[ X ]";
                }
                else {
                    cout<<"[ Y ]";
                }
                temp = temp->next;
            }
            cout<<endl;
        }
    }

    void bookSeat(int row, int seat) {
        int i;
        if(row < 1 || row > 8 || seat < 1 || seat > 8) {
            cout<<"Invalid row or seat number. Please enter values between 1 and 8.\n";
            return;
        }
        int index = (row - 1) * 8 + (seat - 1);
        Seat* temp = head;
        for(i=0;i<index;i++) {
            temp = temp->next;
        }
        if(temp->booked) {
            cout<<"Seat is already booked. Choose another seat.\n";
        } 
        else {
            temp->booked = 1; // true
            cout<<"Seat "<<seat<<" from row "<<row<<" is booked successfully.\n";
        }
    }

    void cancelSeat(int row,int seat) {
        int i;
        char ch;
        if(row < 1 || row > 8 || seat < 1 || seat > 8) {
            cout<<"Invalid row or seat number. Please enter values between 1 and 8.\n";
            return;
        }
        int index = (row - 1) * 8 + (seat - 1);
        Seat* temp = head;
        for(i=0;i<index;i++) {
            temp = temp->next;
        }
        if(!temp->booked) {
            cout<<"Seat is not yet booked. Do you want to book it? (y/n)\n";
            cin>>ch;
            if(ch=='y') {
                temp->booked = 1;
                cout<<"Seat "<<seat<<" from row "<<row<<" is booked successfully.";
            }
        }
        else {
            temp->booked = 0;
            cout<<"Seat "<<seat<<" from row "<<row<<" is cancelled successfully.";
        }
        cout<<endl;
    }
};

int main() {
    Galaxy g;
    int ch,row,seat;
    clrscr();

    do {
        cout<<"\n\tGalaxy Multiplex Ticket System\t\n";
        cout<<"1. Display all seats\n";
        cout<<"2. Book a seat\n";
        cout<<"3. Cancel a seat\n";
        cout<<"4. Exit\n";
        cout<<"Enter your choice: ";
        cin>>ch;

        switch (ch) {
        case 1:
            g.displaySeats();
            break;
        case 2:
            cout<<"Enter Row (1 to 8): ";
            cin>>row;
            cout<<"Enter Seat (1 to 8): ";
            cin>>seat;
            g.bookSeat(row,seat);
            break;
        case 3:
            cout<<"Enter Row (1 to 8): ";
            cin>>row;
            cout<<"Enter Seat (1 to 8): ";
            cin>>seat;
            g.cancelSeat(row,seat);
            break;
        case 4:
            cout<<"Exiting..\n";
            break;
        default:
            cout<<"Invalid choice! Try again.\n";
        }
    } while(ch!= 4);

    return 0;
}

```

## Output

```text
Galaxy Multiplex Ticket System
1. Display all seats
2. Book a seat
3. Cancel a seat
4. Exit
Enter your choice: 1
Row 1: [ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ]
Row 2: [ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ]
Row 3: [ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ]
Row 4: [ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ]
Row 5: [ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ]
Row 6: [ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ]
Row 7: [ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ]
Row 8: [ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ]

Enter your choice: 2
Enter Row (1 to 8): 3
Enter Seat (1 to 8): 5
Seat 5 from row 3 is booked successfully.

Enter your choice: 1
Row 1: [ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ]
Row 2: [ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ][ Y ]
Row 3: [ Y ][ Y ][ Y ][ Y ][ X ][ Y ][ Y ][ Y ]
... (rows 4-8 omitted for brevity) ...

Enter your choice: 3
Enter Row (1 to 8): 3
Enter Seat (1 to 8): 5
Seat 5 from row 3 is cancelled successfully.
```
