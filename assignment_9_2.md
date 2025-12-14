# Assignment No: 9.2

## Title
Write a Program to implement Prim's algorithm to find minimum spanning tree of a user defined graph. Use Adjacency List to represent a graph.

## Code

```cpp
#include <iostream.h>
#include <conio.h>

#define MAX 20
#define INF 9999

struct Node
{
    int v;
    int w;
    Node *next;
};

Node *adj[MAX];
int V;

/* Add edge (undirected graph) */
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
}

/* Prim's Algorithm */
void primMST()
{
    int parent[MAX], key[MAX], mst[MAX];
    int i, count, u, min, total = 0;

    for (i = 0; i < V; i++)
    {
        key[i] = INF;
        mst[i] = 0;
    }

    key[0] = 0;
    parent[0] = -1;

    for (count = 0; count < V - 1; count++)
    {
        min = INF;
        for (i = 0; i < V; i++)
        {
            if (mst[i] == 0 && key[i] < min)
            {
                min = key[i];
                u = i;
            }
        }

        mst[u] = 1;

        Node *p = adj[u];
        while (p != NULL)
        {
            if (mst[p->v] == 0 && p->w < key[p->v])
            {
                key[p->v] = p->w;
                parent[p->v] = u;
            }
            p = p->next;
        }
    }

    cout << "\nEdges in Minimum Spanning Tree:\n";
    for (i = 1; i < V; i++)
    {
        cout << parent[i] << " - " << i
             << "   Weight: " << key[i] << endl;
        total += key[i];
    }

    cout << "Total Minimum Cost = " << total << endl;
}

/* MAIN */
void main()
{
    int e, u, v, w, i;
    clrscr();

    cout << "Enter number of vertices: ";
    cin >> V;

    for (i = 0; i < V; i++)
        adj[i] = NULL;

    cout << "Enter number of edges: ";
    cin >> e;

    for (i = 0; i < e; i++)
    {
        cout << "Enter edge (u v weight): ";
        cin >> u >> v >> w;
        addEdge(u, v, w);
    }

    primMST();

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
