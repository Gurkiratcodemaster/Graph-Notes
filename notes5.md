# Topological Sorting using Kahn’s Algorithm (BFS)

## 1. What is Topological Sorting?

- Topological Sort is a linear ordering of vertices in a **Directed Acyclic Graph (DAG)**.
- For every directed edge:

```text
u -> v
```

Vertex `u` appears before `v` in ordering.

---

## 2. Important Condition

Topological Sorting works only for:

- Directed Graph
- Acyclic Graph (DAG)

If cycle exists:
- Topological ordering is not possible.

---

## 3. Kahn’s Algorithm

Kahn’s Algorithm uses:

- BFS
- Queue
- Indegree Array

---

# 4. Steps of Kahn's Algorithm

## Step 1
Calculate indegree of all vertices.

```text
Indegree = Number of incoming edges
```

---

## Step 2
Push all vertices with indegree `0` into queue.

---

## Step 3
Run BFS until queue becomes empty.

---

## Step 4
Pop node from queue:
- Add it to answer
- Reduce indegree of neighbors

---

## Step 5
If neighbor indegree becomes `0`,
push it into queue.

---

# 5. Dry Run Example

## Graph

```text
5 ----> 0 <---- 4
|               |
v               v
2 ----> 3 ----> 1
```

---

## Indegree Array

| Node | Indegree |
|---|---|
| 0 | 2 |
| 1 | 2 |
| 2 | 1 |
| 3 | 1 |
| 4 | 0 |
| 5 | 0 |

---

## Queue Initially

```text
[4, 5]
```

---

## Processing

### Pop 4
- Answer: `[4]`
- Reduce indegree of:
  - 0 → 1
  - 1 → 1

---

### Pop 5
- Answer: `[4, 5]`
- Reduce indegree of:
  - 0 → 0
  - 2 → 0

Push:
```text
0, 2
```

---

### Pop 0
Answer:
```text
[4, 5, 0]
```

---

### Pop 2
Reduce indegree of 3:

```text
3 → 0
```

Push 3.

---

### Pop 3
Reduce indegree of 1:

```text
1 → 0
```

Push 1.

---

### Final Topological Order

```text
4 5 0 2 3 1
```

---

# 6. C++ Code

```cpp
#include <iostream>
#include <vector>
#include <queue>

using namespace std;

class Solution {
public:

    vector<int> topoSort(int V, vector<int> adj[]) {

        vector<int> indegree(V, 0);

        // Step 1:
        // Calculate indegree

        for(int i = 0; i < V; i++) {

            for(int neighbor : adj[i]) {
                indegree[neighbor]++;
            }
        }

        // Step 2:
        // Push all 0 indegree nodes into queue

        queue<int> q;

        for(int i = 0; i < V; i++) {

            if(indegree[i] == 0) {
                q.push(i);
            }
        }

        vector<int> ans;

        // Step 3:
        // BFS

        while(!q.empty()) {

            int node = q.front();
            q.pop();

            ans.push_back(node);

            // Step 4:
            // Reduce indegree of neighbors

            for(int neighbor : adj[node]) {

                indegree[neighbor]--;

                // Step 5:
                // Push if indegree becomes 0

                if(indegree[neighbor] == 0) {
                    q.push(neighbor);
                }
            }
        }

        return ans;
    }
};
```

---

# 7. Time Complexity

## Time Complexity

```text
O(V + E)
```

Where:
- V = Vertices
- E = Edges

Reason:
- Every node processed once
- Every edge processed once

---

## Space Complexity

```text
O(V)
```

Due to:
- Queue
- Indegree array
- Answer vector

---

# 8. Detect Cycle using Kahn’s Algorithm

If:

```text
Topological sort size < V
```

Then:
- Cycle exists in graph.

Because some nodes never become indegree `0`.

---

# 9. Cycle Detection Code

```cpp
bool isCyclic(int V, vector<int> adj[]) {

    vector<int> indegree(V, 0);

    for(int i = 0; i < V; i++) {

        for(int neighbor : adj[i]) {
            indegree[neighbor]++;
        }
    }

    queue<int> q;

    for(int i = 0; i < V; i++) {

        if(indegree[i] == 0) {
            q.push(i);
        }
    }

    int count = 0;

    while(!q.empty()) {

        int node = q.front();
        q.pop();

        count++;

        for(int neighbor : adj[node]) {

            indegree[neighbor]--;

            if(indegree[neighbor] == 0) {
                q.push(neighbor);
            }
        }
    }

    return count != V;
}
```

---

# 10. BFS vs Kahn's Algorithm

| BFS | Kahn's Algorithm |
|---|---|
| Normal graph traversal | Topological sorting |
| Uses queue | Uses queue |
| No indegree needed | Indegree required |
| Works on all graphs | Works on DAG only |

---

# 11. Applications of Topological Sort

- Course Schedule Problems
- Dependency Resolution
- Build Systems
- Task Scheduling
- Package Managers
- Compiler Design

---

# 12. LeetCode Problems

## Easy
- Find Eventual Safe States

## Medium
- Course Schedule
- Course Schedule II
- Alien Dictionary

## Hard
- Parallel Courses III

---

# 13. Key Interview Points

- Topological Sort only works on DAG
- Kahn’s Algorithm uses BFS
- Uses indegree array
- If answer size < V → cycle exists
- Time Complexity = O(V + E)

---

# 14. Simple Kahn’s Algorithm Template

```cpp
vector<int> topoSort(int V, vector<int> adj[]) {

    vector<int> indegree(V, 0);

    for(int i = 0; i < V; i++) {

        for(int neighbor : adj[i]) {
            indegree[neighbor]++;
        }
    }

    queue<int> q;

    for(int i = 0; i < V; i++) {

        if(indegree[i] == 0) {
            q.push(i);
        }
    }

    vector<int> ans;

    while(!q.empty()) {

        int node = q.front();
        q.pop();

        ans.push_back(node);

        for(int neighbor : adj[node]) {

            indegree[neighbor]--;

            if(indegree[neighbor] == 0) {
                q.push(neighbor);
            }
        }
    }

    return ans;
}
```
