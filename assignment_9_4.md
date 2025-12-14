# Assignment No: 9.4

## Title
Write a Program to implement Dijkstra's algorithm to find shortest distance between two nodes of a user defined graph. Use Adjacency List to represent a graph.

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

/* Add edge (undirected weighted graph) */
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

/* Dijkstra Algorithm */
void dijkstra(int start, int end)
{
    int dist[MAX], visited[MAX];
    int i, count, u, min;

    for (i = 0; i < V; i++)
    {
        dist[i] = INF;
        visited[i] = 0;
    }

    dist[start] = 0;

    for (count = 0; count < V - 1; count++)
    {
        min = INF;
        for (i = 0; i < V; i++)
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
            if (visited[p->v] == 0 &&
                dist[u] + p->w < dist[p->v])
            {
                dist[p->v] = dist[u] + p->w;
            }
            p = p->next;
        }
    }

    cout << "\nShortest distance from "
         << start << " to " << end
         << " = " << dist[end] << endl;
}

/* MAIN */
void main()
{
    int e, u, v, w, i, start, end;
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

    cout << "Enter starting vertex: ";
    cin >> start;

    cout << "Enter destination vertex: ";
    cin >> end;

    dijkstra(start, end);

    getch();
}

```

## Output

```text
Enter number of vertices: 5
Enter number of edges: 6
Enter edge (source destination weight): 0 1 4
Enter edge (source destination weight): 0 2 1
Enter edge (source destination weight): 2 1 2
Enter edge (source destination weight): 1 3 1
Enter edge (source destination weight): 2 3 5
Enter edge (source destination weight): 3 4 3
Enter starting node: 0
Enter destination node: 4

Shortest distance from 0 to 4 = 7
```
