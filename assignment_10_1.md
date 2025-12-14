# Assignment No: 10.1

## Title
Write a Program to implement Kruskal's algorithm to find the minimum spanning tree of a user defined graph. Use Adjacency Matrix to represent a graph.

## Code

```cpp
#include <iostream.h>
#include <conio.h>

#define MAX 20

struct Edge
{
    int src;
    int dest;
    int weight;
    Edge *next;
};

/* Add edge to linked list */
void addEdge(Edge* &head, int s, int d, int w)
{
    Edge *t = new Edge;
    t->src = s;
    t->dest = d;
    t->weight = w;
    t->next = head;
    head = t;
}

/* Find parent */
int findParent(int parent[], int i)
{
    while (parent[i] != i)
        i = parent[i];
    return i;
}

/* Union sets */
void unionSet(int parent[], int a, int b)
{
    int x = findParent(parent, a);
    int y = findParent(parent, b);
    parent[x] = y;
}

/* Sort edges by weight (Bubble sort on linked list) */
void sortEdges(Edge *head)
{
    Edge *i, *j;
    int t;

    for (i = head; i != NULL; i = i->next)
    {
        for (j = i->next; j != NULL; j = j->next)
        {
            if (i->weight > j->weight)
            {
                t = i->weight; i->weight = j->weight; j->weight = t;
                t = i->src;    i->src    = j->src;    j->src    = t;
                t = i->dest;   i->dest   = j->dest;   j->dest   = t;
            }
        }
    }
}

/* MAIN */
void main()
{
    int n, i, j;
    int graph[MAX][MAX];
    Edge *edgeList = NULL;
    Edge *p;
    int parent[MAX];
    int count = 0, total = 0;
    
    clrscr();

    cout << "Enter number of vertices: ";
    cin >> n;

    cout << "Enter adjacency matrix:\n";
    for (i = 0; i < n; i++)
        for (j = 0; j < n; j++)
            cin >> graph[i][j];

    /* Convert adjacency matrix to edge list */
    for (i = 0; i < n; i++)
    {
        for (j = i + 1; j < n; j++)
        {
            if (graph[i][j] != 0)
                addEdge(edgeList, i, j, graph[i][j]);
        }
    }

    sortEdges(edgeList);

    for (i = 0; i < n; i++)
        parent[i] = i;

    cout << "\nEdges in Minimum Spanning Tree:\n";
    p = edgeList;

    while (p != NULL && count < n - 1)
    {
        int u = p->src;
        int v = p->dest;

        if (findParent(parent, u) != findParent(parent, v))
        {
            cout << u << " - " << v
                 << "   Weight: " << p->weight << endl;
            total += p->weight;
            unionSet(parent, u, v);
            count++;
        }
        p = p->next;
    }

    cout << "Total Minimum Cost = " << total << endl;

    getch();
}

```

## Output

```text
Enter number of vertices: 4
Enter Adjacency Matrix: 
0 10 6 5
10 0 0 15
6 0 0 4
5 15 4 0

Edges in Minimum Spanning Tree: 
2 - 3 : 4
0 - 3 : 5
0 - 1 : 10
Total Minimum Cost = 19
```
