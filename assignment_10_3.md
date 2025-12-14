# Assignment No: 10.3

## Title
Write a Program to implement Prim's algorithm to find minimum spanning tree of a user defined graph. Use Adjacency List to represent a graph.

## Code

```cpp
#include <iostream.h>
#include <conio.h>

#define MAX 10
#define INF 9999

/* Node for Adjacency List */
struct Node
{
    int vertex;
    int weight;
    Node *next;
};

/* Add edge (Undirected Graph) */
void addEdge(Node *adj[], int u, int v, int w)
{
    Node *t = new Node;
    t->vertex = v;
    t->weight = w;
    t->next = adj[u];
    adj[u] = t;

    t = new Node;
    t->vertex = u;
    t->weight = w;
    t->next = adj[v];
    adj[v] = t;
}

/* Prim's Algorithm */
void prim(int n, Node *adj[])
{
    int key[MAX], parent[MAX], visited[MAX];
    int i, count, u, min, total = 0;

    for (i = 0; i < n; i++)
    {
        key[i] = INF;
        visited[i] = 0;
        parent[i] = -1;
    }

    key[0] = 0;   // Start from vertex 0

    for (count = 0; count < n - 1; count++)
    {
        min = INF;

        for (i = 0; i < n; i++)
        {
            if (visited[i] == 0 && key[i] < min)
            {
                min = key[i];
                u = i;
            }
        }

        visited[u] = 1;

        Node *p = adj[u];
        while (p != NULL)
        {
            int v = p->vertex;
            int w = p->weight;

            if (visited[v] == 0 && w < key[v])
            {
                key[v] = w;
                parent[v] = u;
            }
            p = p->next;
        }
    }

    cout << "\nEdges in Minimum Spanning Tree:\n";
    for (i = 1; i < n; i++)
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
    int n, e, u, v, w, i;
    Node *adj[MAX];
    clrscr();

    cout << "Enter number of vertices: ";
    cin >> n;

    for (i = 0; i < n; i++)
        adj[i] = NULL;

    cout << "Enter number of edges: ";
    cin >> e;

    cout << "Enter edges (u v weight):\n";
    for (i = 0; i < e; i++)
    {
        cin >> u >> v >> w;
        addEdge(adj, u, v, w);
    }

    prim(n, adj);

    getch();
}

```

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
0 - 1 : 10
3 - 2 : 4
0 - 3 : 5
Total Cost = 19
```
