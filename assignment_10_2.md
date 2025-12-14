# Assignment No: 10.2

## Title
Write a Program to implement Dijkstra's algorithm to find shortest distance between two nodes of a user defined graph. Use Adjacency Matrix to represent a graph.

## Code

```cpp
#include <iostream.h>
#include <conio.h>

#define MAX 10
#define INF 9999

/* Linked List Node for Path */
struct Node
{
    int data;
    Node *next;
};

/* Insert at beginning (simple) */
void insert(Node* &head, int value)
{
    Node *t = new Node;
    t->data = value;
    t->next = head;
    head = t;
}

/* Display linked list */
void display(Node *head)
{
    while (head != NULL)
    {
        cout << head->data << " ";
        head = head->next;
    }
}

/* Dijkstra Algorithm */
void dijkstra(int graph[MAX][MAX], int n, int src, int dest)
{
    int dist[MAX], visited[MAX], parent[MAX];
    int i, j, count, u, min;
    Node *path = NULL;
    int temp;

    for (i = 0; i < n; i++)
    {
        dist[i] = INF;
        visited[i] = 0;
        parent[i] = -1;
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

        for (j = 0; j < n; j++)
        {
            if (visited[j] == 0 && graph[u][j] != 0 &&
                dist[u] + graph[u][j] < dist[j])
            {
                dist[j] = dist[u] + graph[u][j];
                parent[j] = u;
            }
        }
    }

    /* Build path using linked list */
    temp = dest;

    while (temp != -1)
    {
        insert(path, temp);
        temp = parent[temp];
    }

    cout << "\nShortest Distance = " << dist[dest] << endl;
    cout << "Path: ";
    display(path);
}

/* MAIN */
void main()
{
    int graph[MAX][MAX];
    int n, i, j, src, dest;
    clrscr();

    cout << "Enter number of vertices: ";
    cin >> n;

    cout << "Enter adjacency matrix:\n";
    for (i = 0; i < n; i++)
        for (j = 0; j < n; j++)
            cin >> graph[i][j];

    cout << "Enter source vertex: ";
    cin >> src;

    cout << "Enter destination vertex: ";
    cin >> dest;

    dijkstra(graph, n, src, dest);

    getch();
}

```

## Output

```text
Enter number of vertices: 5
Enter Adjacency Matrix: 
0 10 0 30 100
10 0 50 0 0
0 50 0 20 10
30 0 20 0 60
100 0 10 60 0
Enter source node: 0
Enter destination node: 4

Shortest Distance from 0 to 4 = 60
Path (in reverse using linked list): 4 2 3 0 
```
