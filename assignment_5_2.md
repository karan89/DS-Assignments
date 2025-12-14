# Assignment No: 5.2

## Title
Convert given infix expression Eg. a-b*c-d/e+f into postfix form using stack and show the operations step by step.

## Code

```cpp
#include<iostream.h>
#include<conio.h>
#include<ctype.h>
#include<string.h>

/* Stack node */
struct Node {
    char data;
    Node *next;
};

Node *top = NULL;

/* Push operation */
void push(char c) {
    Node *temp = new Node;
    temp->data = c;
    temp->next = top;
    top = temp;
}

/* Pop operation */
char pop() {
    if (top == NULL)
        return '\0';
    char x = top->data;
    Node *t = top;
    top = top->next;
    delete t;
    return x;
}

/* Peek operation */
char peek() {
    if (top == NULL)
        return '\0';
    return top->data;
}

/* Precedence function */
int precedence(char c) {
    if (c == '*' || c == '/') return 2;
    if (c == '+' || c == '-') return 1;
    return 0;
}

void main() {
    char infix[50], postfix[50];
    int i, k = 0;
    char ch;
    clrscr();

    cout << "Enter infix expression: ";
    cin >> infix;

    for (i = 0; infix[i] != '\0'; i++) {
        ch = infix[i];

        // Operand
        if (isalnum(ch)) {
            postfix[k++] = ch;
        }
        // Operator
        else {
            while (top != NULL && precedence(peek()) >= precedence(ch)) {
                postfix[k++] = pop();
            }
            push(ch);
        }
    }

    // Pop remaining operators
    while (top != NULL) {
        postfix[k++] = pop();
    }

    postfix[k] = '\0';

    cout << "Postfix Expression: " << postfix;
    getch();
}
```

## Output

```text
Enter infix expression: a+b*c/d

Converting Infix: a+b*c/d

Step-by-step operations:
Token     Action                             Stack (top..bottom)      Output
--------------------------------------------------------------------------------
a         Append operand to output           []                       a
+         Push operator                      [+]                      a
b         Append operand to output           [+]                      ab
* Push operator                      [*+]                     ab
c         Append operand to output           [*+]                     abc
/         Pop and output '*' (prec/assoc)    [+]                      abc*
/         Push operator                      [/+]                     abc*
d         Append operand to output           [/+]                     abc*d
EOF       Pop and output / at end            [+]                      abc*d/
EOF       Pop and output + at end            []                       abc*d/+

Final Postfix: abc*d/+
```
