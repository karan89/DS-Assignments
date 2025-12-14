# Assignment No: 10.4

## Title
Write a Program to implement Kruskal's algorithm to find the minimum spanning tree of a user defined graph. Use Adjacency List to represent a graph.

## Code

```cpp
#include <iostream.h>
#include <conio.h>

#define MAXV 10
#define MAXE 30

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
    int u, v, w;
};

Node *adj[MAXV];
Edge edges[MAXE];
int parent[MAXV];
int V, E, edgeCount = 0;

/* Add edge to adjacency list */
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

    /* Store edge only once for Kruskal */
    edges[edgeCount].u = u;
    edges[edgeCount].v = v;
    edges[edgeCount].w = w;
    edgeCount++;
}

/* Find parent (Union-Find) */
int findParent(int parent[], int i)
{
    while (parent[i] != i)
        i = parent[i];
    return i;
}

/* Union two sets */
void unionSet(int parent[], int a, int b)
{
    int x = findParent(parent, a);
    int y = findParent(parent, b);
    parent[x] = y;
}

/* Sort edges by weight (Bubble Sort) */
void sortEdges()
{
    int i, j;
    Edge temp;

    for (i = 0; i < edgeCount - 1; i++)
    {
        for (j = 0; j < edgeCount - i - 1; j++)
        {
            if (edges[j].w > edges[j + 1].w)
            {
                temp = edges[j];
                edges[j] = edges[j + 1];
                edges[j + 1] = temp;
            }
        }
    }
}

/* Kruskal Algorithm */
void kruskal()
{
    int i, count = 0, total = 0;

    for (i = 0; i < V; i++)
        parent[i] = i;

    sortEdges();

    cout << "\nEdges in Minimum Spanning Tree:\n";

    for (i = 0; i < edgeCount && count < V - 1; i++)
    {
        int u = edges[i].u;
        int v = edges[i].v;

        if (findParent(parent, u) != findParent(parent, v))
        {
            cout << u << " - " << v
                 << "   Weight: " << edges[i].w << endl;

            total += edges[i].w;
            unionSet(parent, u, v);
            count++;
        }
    }

    cout << "Total Minimum Cost = " << total << endl;
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

    cout << "Enter edges (u v weight):\n";
    for (i = 0; i < E; i++)
    {
        cin >> u >> v >> w;
        addEdge(u, v, w);
    }

    kruskal();

    getch();
}
``

## Output

```text
Enter number of vertices: 4
Enter number of edges: 5
Enter edges (u v weight):
0 1 10
0 2 6
0 3 5
1 3 15
2 3 4

Edges in Minimum Spanning Tree: 
2 - 3 : 4
0 - 3 : 5
0 - 1 : 10
Total Cost = 19
```
