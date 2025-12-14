# Assignment No: 9.5

## Title
Write a Program to accept a graph from a user and represent it with Adjacency List and perform BFS and DFS traversals on it.

## Code

```cpp
#include <iostream.h>
#include <conio.h>

#define MAX 20

struct Node
{
    int vertex;
    Node *next;
};

Node *adj[MAX];
int visited[MAX];
int V;

/* Add edge (Undirected Graph) */
void addEdge(int u, int v)
{
    Node *t = new Node;
    t->vertex = v;
    t->next = adj[u];
    adj[u] = t;

    t = new Node;
    t->vertex = u;
    t->next = adj[v];
    adj[v] = t;
}

/* BFS using array queue */
void BFS(int start)
{
    int queue[MAX];
    int front = 0, rear = 0;
    int i;

    for (i = 0; i < V; i++)
        visited[i] = 0;

    visited[start] = 1;
    queue[rear++] = start;

    cout << "\nBFS Traversal: ";

    while (front < rear)
    {
        int v = queue[front++];
        cout << v << " ";

        Node *p = adj[v];
        while (p != NULL)
        {
            if (!visited[p->vertex])
            {
                visited[p->vertex] = 1;
                queue[rear++] = p->vertex;
            }
            p = p->next;
        }
    }
}

/* DFS using recursion */
void DFS(int v)
{
    visited[v] = 1;
    cout << v << " ";

    Node *p = adj[v];
    while (p != NULL)
    {
        if (!visited[p->vertex])
            DFS(p->vertex);
        p = p->next;
    }
}

/* MAIN */
void main()
{
    int e, u, v, start, i;
    clrscr();

    cout << "Enter number of vertices: ";
    cin >> V;

    for (i = 0; i < V; i++)
        adj[i] = NULL;

    cout << "Enter number of edges: ";
    cin >> e;

    for (i = 0; i < e; i++)
    {
        cout << "Enter edge (u v): ";
        cin >> u >> v;
        addEdge(u, v);
    }

    cout << "Enter starting vertex: ";
    cin >> start;

    BFS(start);

    for (i = 0; i < V; i++)
        visited[i] = 0;

    cout << "\nDFS Traversal: ";
    DFS(start);

    getch();
}

```

## Output

```text
Enter number of vertices: 5
Enter number of edges: 4
Enter edge (source destination): 0 1
Enter edge (source destination): 0 2
Enter edge (source destination): 1 3
Enter edge (source destination): 2 4
Enter starting vertex: 0

BFS Traversal: 0 2 1 4 3 
DFS Traversal: 0 2 4 1 3 
```
