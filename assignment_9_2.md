# Assignment No: 9.2

## Title
Write a Program to implement Prim's algorithm to find minimum spanning tree of a user defined graph. Use Adjacency List to represent a graph.

## Code

```cpp
#include <iostream.h>
#include <conio.h>

#define MAXV 20
#define MAXE 50

/* Adjacency List Node */
struct Node
{
    int v;
    int w;
    Node *next;
};

/* Edge structure for Kruskal */
struct Edge
{
    int src;
    int dest;
    int weight;
};

Node *adj[MAXV];
Edge edges[MAXE];
int parent[MAXV];

int V, E, edgeCount = 0;

/* Create adjacency list edge */
void addEdge(int u, int v, int w)
{
    Node *t = new Node;
    t->v = v;
    t->w = w;
    t->next = adj[u];
    adj[u] = t;

    t = new Node;
    t->v = u;
    t->w = w;
    t->next = adj[v];
    adj[v] = t;

    /* Store edge only once */
    edges[edgeCount].src = u;
    edges[edgeCount].dest = v;
    edges[edgeCount].weight = w;
    edgeCount++;
}

/* Find set */
int findSet(int i)
{
    while (parent[i] != i)
        i = parent[i];
    return i;
}

/* Union sets */
void unionSet(int a, int b)
{
    int x = findSet(a);
    int y = findSet(b);
    parent[x] = y;
}

/* Kruskal Algorithm */
void kruskal()
{
    int i, j;
    Edge temp;
    int totalCost = 0;

    /* Initialize parent */
    for (i = 0; i < V; i++)
        parent[i] = i;

    /* Sort edges by weight (Bubble Sort) */
    for (i = 0; i < edgeCount - 1; i++)
    {
        for (j = 0; j < edgeCount - i - 1; j++)
        {
            if (edges[j].weight > edges[j + 1].weight)
            {
                temp = edges[j];
                edges[j] = edges[j + 1];
                edges[j + 1] = temp;
            }
        }
    }

    cout << "\nEdges in Minimum Spanning Tree:\n";

    for (i = 0; i < edgeCount; i++)
    {
        int u = edges[i].src;
        int v = edges[i].dest;

        if (findSet(u) != findSet(v))
        {
            cout << u << " - " << v
                 << "   Weight: " << edges[i].weight << endl;
            totalCost += edges[i].weight;
            unionSet(u, v);
        }
    }

    cout << "Total Minimum Cost = " << totalCost << endl;
}

/* MAIN */
void main()
{
    int i, u, v, w;
    clrscr();

    cout << "Enter number of vertices: ";
    cin >> V;

    for (i = 0; i < V; i++)
        adj[i] = NULL;

    cout << "Enter number of edges: ";
    cin >> E;

    for (i = 0; i < E; i++)
    {
        cout << "Enter edge (u v weight): ";
        cin >> u >> v >> w;
        addEdge(u, v, w);
    }

    kruskal();

    getch();
}


```

## Output

```text
Enter number of vertices: 5
Enter number of edges: 6
Enter edge (source destination weight): 0 1 2
Enter edge (source destination weight): 0 3 6
Enter edge (source destination weight): 1 2 3
Enter edge (source destination weight): 1 3 8
Enter edge (source destination weight): 1 4 5
Enter edge (source destination weight): 2 4 7

Edges in Minimum Spanning Tree:
0 - 1 Weight: 2
1 - 2 Weight: 3
0 - 3 Weight: 6
1 - 4 Weight: 5
Total Minimum Cost = 16
```
