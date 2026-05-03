# Graphs - Basics (DSA Notes)

## 1. Types of Graphs

### Based on Direction
- **Directed Graph (Unidirectional)**
  - Edges have direction  
  - Example: `u → v` (one-way connection)

- **Undirected Graph (Bidirectional)**
  - Edges have no direction  
  - Example: `u — v` (two-way connection)

---

### Based on Weight
- **Weighted Graph**
  - Each edge has a weight (cost/distance)
  - Example: `(u, v, w)` where `w` is weight

- **Unweighted Graph**
  - No weights on edges
  - All edges are treated equally

---

### Based on Connectivity
- **Connected Graph**
  - There is a path between every pair of vertices

- **Disconnected Graph**
  - Some vertices are not reachable from others

---

## 2. Graph Representation

### Adjacency List

- Stores neighbors of each vertex
- Efficient for sparse graphs

```cpp
#include <list>   // Doubly linked list in C++ STL

list<int> adj[V];   // Array of lists
```

### Building a Graph in c++

```
#include <iostream>
#include <vector>
#include <list>
using namespace std;

class Graph {
    int V;
    list<int>* l;

public:
    Graph(int V) {
        this->V = V;
        l = new list<int>[V];
    }

    void addEdge(int u, int v) {
        l[u].push_back(v);
        l[v].push_back(u);  // Remove this line for directed graph
    }
};

int main() {
    Graph g(5);

    g.addEdge(0, 1);
    g.addEdge(1, 2);
    g.addEdge(1, 3);
    g.addEdge(3, 4);

    return 0;
}
```
### Key Notes
Use adjacency list for better space efficiency

For directed graph, remove:
```
l[v].push_back(u);
```
Time Complexity:
- Adding edge → O(1)
- Space → O(V + E)
