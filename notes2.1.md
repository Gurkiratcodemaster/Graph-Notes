# Depth First Search (DFS) - Graph Traversal

## 1. What is DFS?

- DFS = **Depth First Search**
- Traverses graph by going **deep first**
- Uses **recursion** or **stack**
- Backtracks after visiting a path completely

---

## 2. Features of DFS

- Visits one path completely before moving to another
- Can be implemented using:
  - Recursion
  - Stack
- Useful for many graph problems

---

## 3. When to Use DFS

- Detecting cycles
- Topological sorting
- Finding connected components
- Path finding
- Solving maze/grid problems
- Backtracking problems

---

# 4. Graph Class Example

```cpp
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

        // For undirected graph
        l[v].push_back(u);
    }

    void dfsHelper(int node, vector<bool>& visited) {
        visited[node] = true;

        cout << node << " ";

        for (int neighbor : l[node]) {
            if (!visited[neighbor]) {
                dfsHelper(neighbor, visited);
            }
        }
    }

    void dfs(int start) {
        vector<bool> visited(V, false);

        dfsHelper(start, visited);
    }
};

int main() {
    Graph g(5);

    g.addEdge(0, 1);
    g.addEdge(0, 3);
    g.addEdge(1, 2);
    g.addEdge(3, 4);

    g.dfs(0);

    return 0;
}
```

---

# 5. DFS Working Step by Step

## Graph

```text
0 -- 1 -- 2
|
3 -- 4
```

## DFS Starting from 0

### Step 1
Visit 0

```text
0
```

### Step 2
Go deeper to 1

```text
0 -> 1
```

### Step 3
Go deeper to 2

```text
0 -> 1 -> 2
```

### Step 4
Backtrack to 0 and visit 3

```text
0 -> 3
```

### Step 5
Visit 4

```text
0 -> 3 -> 4
```

---

# 6. DFS Traversal Output

```text
0 1 2 3 4
```

> Traversal can vary depending on adjacency list order.

---

# 7. DFS Using Stack (Iterative DFS)

```cpp
#include <iostream>
#include <vector>
#include <list>
#include <stack>

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
        l[v].push_back(u);
    }

    void dfsIterative(int start) {
        vector<bool> visited(V, false);

        stack<int> st;

        st.push(start);

        while (!st.empty()) {
            int node = st.top();
            st.pop();

            if (!visited[node]) {
                visited[node] = true;

                cout << node << " ";

                for (int neighbor : l[node]) {
                    if (!visited[neighbor]) {
                        st.push(neighbor);
                    }
                }
            }
        }
    }
};

int main() {
    Graph g(5);

    g.addEdge(0, 1);
    g.addEdge(0, 3);
    g.addEdge(1, 2);
    g.addEdge(3, 4);

    g.dfsIterative(0);

    return 0;
}
```

---

# 8. Time & Space Complexity

## Time Complexity

```text
O(V + E)
```

Where:
- V = Number of vertices
- E = Number of edges

Reason:
- Every vertex is visited once
- Every edge is explored once

---

## Space Complexity

```text
O(V)
```

Due to:
- Visited array
- Recursion stack / explicit stack

---

# 9. BFS vs DFS

| Feature | BFS | DFS |
|---|---|---|
| Data Structure | Queue | Stack / Recursion |
| Traversal Style | Level-wise | Depth-wise |
| Shortest Path | Yes (Unweighted Graph) | No |
| Memory Usage | More | Less |
| Backtracking | No | Yes |
| Used In | Shortest path | Cycle detection, Topological sort |

---

# 10. Recursive DFS Flow

```text
dfs(0)
|
|-- dfs(1)
|    |
|    |-- dfs(2)
|
|-- dfs(3)
     |
     |-- dfs(4)
```

---

# 11. Important Notes

- DFS may not give shortest path
- DFS uses backtracking
- Recursive DFS internally uses stack
- Iterative DFS uses explicit stack

---

# 12. Applications of DFS

- Cycle Detection
- Topological Sorting
- Connected Components
- Maze Solving
- Path Finding
- Strongly Connected Components
- Flood Fill Algorithm

---

# 13. LeetCode / Practice Problems

## Easy
- Number of Provinces
- Flood Fill
- Find if Path Exists in Graph

## Medium
- Course Schedule
- Clone Graph
- Number of Islands
- Surrounded Regions

## Hard
- Word Search II
- Critical Connections in a Network

---

# 14. Key Interview Points

- DFS uses recursion/stack
- BFS uses queue
- DFS explores depth first
- Time Complexity = O(V + E)
- Recursive DFS can cause stack overflow for very deep graphs

---

# 15. Simple DFS Template

```cpp
void dfs(int node, vector<bool>& visited, vector<int> adj[]) {

    visited[node] = true;

    for (int neighbor : adj[node]) {

        if (!visited[neighbor]) {
            dfs(neighbor, visited, adj);
        }
    }
}
```
