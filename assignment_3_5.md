# Assignment No: 3.5

## Title
Write a C++ program to store a binary number using a doubly linked list. Implement the following functions:
a) Calculate and display the 1's complement and 2's complement of the stored binary number.
b) Perform addition of two binary numbers represented using doubly linked lists and display the result.

## Code

```cpp
#include <iostream.h>
#include <conio.h>

struct Node {
    int bit;
    Node* prev;
    Node* next;

    Node(int b) {
        bit = b;
        prev = NULL;
        next = NULL;
    }
};

class Binary {
    Node* head;
    Node* tail;

public:
    Binary() {
        head = NULL;
        tail = NULL;
    }

    void insertBit(int b) {
        Node* newNode = new Node(b);
        if(!head) {
            head = newNode;
            tail = newNode;
        } else {
            tail->next = newNode;
            newNode->prev = tail;
            tail = newNode;
        }
    }

    void clear() {
        head = NULL;
        tail = NULL;
    }

    void display() {
        if(!head) {
            cout << "(empty)\n";
            return;
        }
        Node* temp = head;
        while(temp) {
            cout << temp->bit;
            temp = temp->next;
        }
        cout << endl;
    }

    // 1s complement
    Binary onesComplement() {
        Binary comp;
        Node* temp = head;
        while(temp) {
            comp.insertBit(temp->bit == 0 ? 1 : 0);
            temp = temp->next;
        }
        return comp;
    }

    // Reverse a binary number
    Binary reverse(Binary& B) {
        Binary R;
        Node* temp = B.tail;
        while(temp) {
            R.insertBit(temp->bit);
            temp = temp->prev;
        }
        return R;
    }

    // 2s complement = 1s complement + 1
    Binary twosComplement() {
        Binary oneC = onesComplement();
        Binary twoC;

        Node* temp = oneC.tail;
        int carry = 1;

        while(temp) {
            int sum = temp->bit + carry;
            twoC.insertBit(sum % 2);
            carry = sum / 2;
            temp = temp->prev;
        }
        if(carry) twoC.insertBit(1);

        return reverse(twoC);
    }

    // Add two binary numbers
    // Note: In Turbo C, passing objects works, but keeping it simple is better.
    Binary add(Binary B) {
        Binary result;
        Node* p = tail;      // this object's tail
        Node* q = B.tail;    // passed object's tail
        int carry = 0;

        while(p || q || carry) {
            int x = 0;
            int y = 0;
            
            if(p != NULL) x = p->bit;
            if(q != NULL) y = q->bit;

            int sum = x + y + carry;

            result.insertBit(sum % 2);
            carry = sum / 2;

            if(p) p = p->prev;
            if(q) q = q->prev;
        }

        return reverse(result);
    }
};

int main() {
    Binary B1, B2, result;
    int choice, n, bit, i;
    clrscr();

    do {
        cout << "\n=== Binary Menu Using Doubly Linked List ===\n";
        cout << "1. Enter Binary Number 1\n";
        cout << "2. Display 1's Complement of Number 1\n";
        cout << "3. Display 2's Complement of Number 1\n";
        cout << "4. Enter Binary Number 2\n";
        cout << "5. Add Binary Number 1 and 2\n";
        cout << "6. Display Binary Number 1\n";
        cout << "7. Display Binary Number 2\n";
        cout << "8. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch(choice) {
            case 1:
                B1.clear();
                cout << "Enter number of bits: ";
                cin >> n;
                cout << "Enter bits: ";
                for(i=0; i<n; i++) {
                    cin >> bit;
                    B1.insertBit(bit);
                }
                break;

            case 2:
                cout << "1's Complement: ";
                result = B1.onesComplement();
                result.display();
                break;

            case 3:
                cout << "2's Complement: ";
                result = B1.twosComplement();
                result.display();
                break;

            case 4:
                B2.clear();
                cout << "Enter number of bits: ";
                cin >> n;
                cout << "Enter bits: ";
                for(i=0; i<n; i++) {
                    cin >> bit;
                    B2.insertBit(bit);
                }
                break;

            case 5:
                cout << "Addition Result: ";
                // Modified call slightly to use member function approach
                result = B1.add(B2);
                result.display();
                break;

            case 6:
                cout << "Binary Number 1: ";
                B1.display();
                break;

            case 7:
                cout << "Binary Number 2: ";
                B2.display();
                break;

            case 8:
                cout << "Exiting...\n";
                break;

            default:
                cout << "Invalid choice! Try again.\n";
        }

    } while(choice != 8);

    return 0;
}

```

## Output

```text
Binary Menu Using Doubly Linked List
...
Enter your choice: 1
Enter number of bits: 4
Enter bits: 1 0 1 1

Enter your choice: 6
Binary Number 1: 1011

Enter your choice: 2
1's Complement: 0100

Enter your choice: 3
2's Complement: 0101

Enter your choice: 4
Enter number of bits: 4
Enter bits: 0 1 0 1

Enter your choice: 7
Binary Number 2: 0101

Enter your choice: 5
Addition Result: 10000
```
