# Assignment No: 9.1

## Title
Write a Program to accept a graph from a user and represent it with Adjacency Matrix and perform BFS and DFS traversals on it.

## Code

```cpp
#include <stdio.h>
#include <conio.h>

int adj[20][20];
int visited[20];
int n;

/* DFS Traversal */
void DFS(int v)
{
    int i;
    printf("%d ", v);
    visited[v] = 1;

    for (i = 0; i < n; i++)
    {
        if (adj[v][i] == 1 && visited[i] == 0)
        {
            DFS(i);
        }
    }
}

/* BFS Traversal */
void BFS(int start)
{
    int queue[20], front = 0, rear = 0;
    int i, v;

    for (i = 0; i < n; i++)
        visited[i] = 0;

    queue[rear++] = start;
    visited[start] = 1;

    while (front < rear)
    {
        v = queue[front++];
        printf("%d ", v);

        for (i = 0; i < n; i++)
        {
            if (adj[v][i] == 1 && visited[i] == 0)
            {
                visited[i] = 1;
                queue[rear++] = i;
            }
        }
    }
}

void main()
{
    int edges, i, j, u, v, start;

    clrscr();

    printf("Enter number of vertices: ");
    scanf("%d", &n);

    /* Initialize adjacency matrix */
    for (i = 0; i < n; i++)
        for (j = 0; j < n; j++)
            adj[i][j] = 0;

    printf("Enter number of edges: ");
    scanf("%d", &edges);

    printf("Enter edges (u v):\n");
    for (i = 0; i < edges; i++)
    {
        scanf("%d %d", &u, &v);
        adj[u][v] = 1;
        adj[v][u] = 1;   /* Undirected graph */
    }

    printf("\nAdjacency Matrix:\n");
    for (i = 0; i < n; i++)
    {
        for (j = 0; j < n; j++)
            printf("%d ", adj[i][j]);
        printf("\n");
    }

    printf("\nEnter starting vertex: ");
    scanf("%d", &start);

    for (i = 0; i < n; i++)
        visited[i] = 0;

    printf("\nDFS Traversal: ");
    DFS(start);

    printf("\nBFS Traversal: ");
    BFS(start);

    getch();
}

```

## Output

```text
Enter number of vertices: 4
Enter number of edges: 3
Enter edge (source destination): 1 3
Enter edge (source destination): 3 2
Enter edge (source destination): 1 2

Adjacency Matrix:
0 0 0 0 
0 0 1 1 
0 1 0 1 
0 1 1 0 

Enter starting vertex for BFS and DFS: 3

BFS Traversal: 3 2 1 
DFS Traversal: 3 2 1 
```
