# Assignment No: 10.5

## Title
Write a Program to implement Dijkstra's algorithm to find shortest distance between two nodes of a user defined graph. Use Adjacency List to represent a graph.

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

/* Dijkstra Algorithm */
void dijkstra(Node *adj[], int n, int src, int dest)
{
    int dist[MAX], visited[MAX];
    int i, count, u, min;

    for (i = 0; i < n; i++)
    {
        dist[i] = INF;
        visited[i] = 0;
    }

    dist[src] = 0;

    for (count = 0; count < n - 1; count++)
    {
        min = INF;

        for (i = 0; i < n; i++)
        {
            if (visited[i] == 0 && dist[i] < min)
            {
                min = dist[i];
                u = i;
            }
        }

        visited[u] = 1;

        Node *p = adj[u];
        while (p != NULL)
        {
            int v = p->vertex;
            int w = p->weight;

            if (visited[v] == 0 && dist[u] + w < dist[v])
            {
                dist[v] = dist[u] + w;
            }
            p = p->next;
        }
    }

    cout << "\nShortest distance from "
         << src << " to " << dest
         << " = " << dist[dest] << endl;
}

/* MAIN */
void main()
{
    int n, e, u, v, w, src, dest, i;
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

    cout << "Enter source vertex: ";
    cin >> src;

    cout << "Enter destination vertex: ";
    cin >> dest;

    dijkstra(adj, n, src, dest);

    getch();
}

```

## Output

```text
Enter number of vertices: 5
Enter number of edges: 6
Enter edges (u v weight): 
0 1 4
0 2 2
1 2 5
1 3 10
2 4 3
3 4 7
Enter source vertex: 0

Shortest distances from source 0:
To 0 = 0
To 1 = 4
To 2 = 2
To 3 = 12
To 4 = 5
```
