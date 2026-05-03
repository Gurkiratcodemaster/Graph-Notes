# Breadth First Search (BFS) - Graph Traversal

## 1. What is BFS?

- BFS = **Breadth First Search**
- Traverses graph **level by level**
- Uses a **queue (FIFO)**

---

## 2. When to Use BFS

- Shortest path in **unweighted graph**
- Level-wise traversal
- Finding connected components
- Checking bipartite graph

---

## 3. BFS Function (Add to Previous Graph Class)

> Refer to the Graph class defined in the previous file.

```cpp id="bfs_func_1"
#include <queue>

void bfs(int start) {
    vector<bool> visited(V, false);
    queue<int> q;

    q.push(start);
    visited[start] = true;

    while (!q.empty()) {
        int node = q.front();
        q.pop();

        cout << node << " ";

        for (int neighbor : l[node]) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}
```
### Time & Space Complexity
Time Complexity:
- O(V + E)
Each vertex and edge is visited once
- Space Complexity:
 O(V)
Due to visited array and queue
