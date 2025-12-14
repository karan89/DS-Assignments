# Assignment No: 5.5

## Title
You are given a postfix expression (also known as Reverse Polish Notation) consisting of single-digit operands and binary operators (+, -, *, /). Your task is to evaluate the expression using stack and return its result.

## Code

```cpp
#include <iostream.h>
#include <conio.h>
#include <ctype.h>   // for isdigit

/* Node structure */
struct Node
{
    int data;
    Node *next;
};

/* Stack top */
Node *top = NULL;

/* Push */
void push(int x)
{
    Node *t = new Node;
    t->data = x;
    t->next = top;
    top = t;
}

/* Pop */
int pop()
{
    Node *t;
    int x;

    if (top == NULL)
        return 0;

    t = top;
    x = t->data;
    top = t->next;
    delete t;
    return x;
}

/* -------- MAIN -------- */
void main()
{
    char postfix[50];
    int i;
    char ch;
    int a, b, result;

    clrscr();

    cout << "Enter postfix expression: ";
    cin >> postfix;

    for (i = 0; postfix[i] != '\0'; i++)
    {
        ch = postfix[i];

        /* Operand */
        if (isdigit(ch))
        {
            push(ch - '0');
        }
        /* Operator */
        else
        {
            b = pop();
            a = pop();

            if (ch == '+') result = a + b;
            else if (ch == '-') result = a - b;
            else if (ch == '*') result = a * b;
            else if (ch == '/') result = a / b;

            push(result);
        }
    }

    cout << "Result = " << pop();

    getch();
}
```

## Output

```text
Enter postfix expression: 231*+9-
Result: -4
```
