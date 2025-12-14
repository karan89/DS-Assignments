# Assignment No: 5.4

## Title
You are given a string containing only parentheses characters: '(', ')', '{', '}', '[', and ']'. Your task is to check whether the parentheses are balanced or not.
A string is considered balanced if:
1. Every opening bracket has a corresponding closing bracket of the same type
2. Brackets are closed in the correct order.

## Code

```cpp
#include <iostream.h>
#include <conio.h>

/* Node structure */
struct Node
{
    char data;
    Node *next;
};

/* Stack top */
Node *top = NULL;

/* Push */
void push(char c)
{
    Node *t = new Node;
    t->data = c;
    t->next = top;
    top = t;
}

/* Pop */
char pop()
{
    Node *t;
    char c;

    if (top == NULL)
        return '\0';

    t = top;
    c = t->data;
    top = t->next;
    delete t;
    return c;
}

/* Check matching pair */
int isMatch(char open, char close)
{
    if (open == '(' && close == ')') return 1;
    if (open == '{' && close == '}') return 1;
    if (open == '[' && close == ']') return 1;
    return 0;
}

void main()
{
    char exp[50];
    int balanced = 1;
    int i;
    char ch, open;

    clrscr();

    cout << "Enter expression: ";
    cin >> exp;

    for (i = 0; exp[i] != '\0'; i++)
    {
        ch = exp[i];

        /* Opening bracket */
        if (ch == '(' || ch == '{' || ch == '[')
            push(ch);

        /* Closing bracket */
        else if (ch == ')' || ch == '}' || ch == ']')
        {
            if (top == NULL)
            {
                balanced = 0;
                break;
            }

            open = pop();

            if (!isMatch(open, ch))
            {
                balanced = 0;
                break;
            }
        }
    }

    /* Stack should be empty */
    if (top != NULL)
        balanced = 0;

    if (balanced)
        cout << "Balanced";
    else
        cout << "Not Balanced";

    getch();
}
```

## Output

```text
Enter string of parentheses: (){[()]}
Balanced
```
