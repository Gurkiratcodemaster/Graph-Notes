# Dijkstra Algorithm Notes

## What is Dijkstra Algorithm?

Dijkstra Algorithm is a greedy algorithm used to find the shortest distance from a source node to all other nodes in a weighted graph.

It works only for:
- Non-negative edge weights

---

# Important Concepts

## 1. Edge Relaxation

Edge relaxation means checking whether we can get a shorter path.

Formula:

```cpp
if(dist[u] + weight < dist[v])
```

then update:

```cpp
dist[v] = dist[u] + weight
```

---

# Priority Queue (Min Heap)

We use a priority queue to always pick the node with the minimum distance.

## Syntax

```cpp
priority_queue<
    pair<int,int>,
    vector<pair<int,int>>,
    greater<pair<int,int>>
> pq;
```

---

# Why use greater<pair<int,int>> ?

Normally priority queue in C++ is a max heap.

Using:

```cpp
greater<pair<int,int>>
```

makes it a min heap.

So smallest distance comes first.

---

# Distance Array

```cpp
vector<int> dist(V, INT_MAX);
```

Meaning:
- Store shortest distance for every vertex
- Initially all distances are infinity

---

# Graph Representation

```cpp
vector<pair<int,int>> graph[V];
```

Each pair contains:

```cpp
{neighbor, weight}
```

---

# Simple Dijkstra Code

```cpp
#include <bits/stdc++.h>
using namespace std;

void dijkstra(int src,
              vector<pair<int,int>> graph[],
              int V)
{
    priority_queue<
        pair<int,int>,
        vector<pair<int,int>>,
        greater<pair<int,int>>
    > pq;

    vector<int> dist(V, INT_MAX);

    dist[src] = 0;

    pq.push({0, src});

    while(!pq.empty())
    {
        int d = pq.top().first;
        int node = pq.top().second;

        pq.pop();

        for(auto it : graph[node])
        {
            int adjNode = it.first;
            int wt = it.second;

            // Edge Relaxation
            if(dist[node] + wt < dist[adjNode])
            {
                dist[adjNode] = dist[node] + wt;

                pq.push({dist[adjNode], adjNode});
            }
        }
    }

    // Print shortest distances
    for(int i = 0; i < V; i++)
    {
        cout << "Distance from source to "
             << i << " = "
             << dist[i] << endl;
    }
}

int main()
{
    int V = 5;

    vector<pair<int,int>> graph[V];

    graph[0].push_back({1,2});
    graph[0].push_back({2,4});

    graph[1].push_back({2,1});
    graph[1].push_back({3,7});

    graph[2].push_back({4,3});

    graph[3].push_back({4,1});

    dijkstra(0, graph, V);
}
```

---

# Time Complexity

```text
O((V + E) log V)
```

Where:
- V = Vertices
- E = Edges

---

# Steps of Dijkstra Algorithm

1. Initialize all distances as infinity
2. Set source distance = 0
3. Push source into min heap
4. Pick minimum distance node
5. Relax all adjacent edges
6. Update distances if shorter path found
7. Repeat until queue becomes empty

---

# Key Point

Dijkstra always selects the node with the smallest current distance first.
