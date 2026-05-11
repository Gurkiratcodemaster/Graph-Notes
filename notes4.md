# Topological Sort (DFS Based)

## What is Topological Sort?

Topological Sort is a linear ordering of vertices in a graph such that:

```text
If there is an edge u -> v
then u must come before v
```

It is used only for:

- Directed Graph
- DAG (Directed Acyclic Graph)

---

# DAG

DAG means:

```text
Directed Acyclic Graph
```

- Directed → edges have direction
- Acyclic → no cycle/loop

Example:

```text
0 → 1 → 2
```

Valid DAG.

Example with cycle:

```text
0 → 1 → 2
↑       ↓
← ← ← ←
```

Not a DAG.

Topological sort is not possible if cycle exists.

---

# Why We Use Topological Sort

Used when one task depends on another.

Examples:

- Course Schedule
- Task Scheduling
- Job Ordering
- Build Systems
- Dependency Resolution

Example:

```text
Eat → Study → Sleep
```

You cannot study before eating if study depends on eating.

---

# DFS Based Approach

We use DFS.

Main idea:

```text
Push node into stack only after all its neighbors are visited.
```

Why?

Because dependent nodes should come later.

---

# Intuition

Graph:

```text
0 → 1 → 2
```

DFS Flow:

```text
dfs(0)
  dfs(1)
    dfs(2)
```

Push after recursion:

```text
push(2)
push(1)
push(0)
```

Stack becomes:

```text
Top -> 0 1 2
```

Correct topological order.

---

# Steps

## 1. Create adjacency list

```cpp
vector<int> adj[V];
```

---

## 2. Create visited array

```cpp
vector<bool> vis(V,false);
```

---

## 3. Run DFS on all unvisited nodes

```cpp
for(int i = 0; i < V; i++){
    if(!vis[i]){
        dfs(i,vis,st,adj);
    }
}
```

---

## 4. Push node after visiting neighbors

```cpp
st.push(curr);
```

This is the most important step.

---

## 5. Pop stack into answer vector

```cpp
while(!st.empty()){
    topology.push_back(st.top());
    st.pop();
}
```

---

# Complete Code

```cpp
class Solution {
public:

    void dfs(int curr,
             vector<bool>& vis,
             stack<int>& st,
             vector<int> adj[]) {

        vis[curr] = true;

        for(int n : adj[curr]) {
            if(!vis[n]) {
                dfs(n, vis, st, adj);
            }
        }

        st.push(curr);
    }

    vector<int> topoSort(int V, vector<vector<int>>& edges) {

        vector<int> adj[V];

        vector<int> topology;

        stack<int> st;

        vector<bool> vis(V,false);

        for(auto it : edges) {

            int u = it[0];
            int v = it[1];

            adj[u].push_back(v);
        }

        for(int i = 0; i < V; i++) {

            if(!vis[i]) {

                dfs(i, vis, st, adj);
            }
        }

        while(!st.empty()) {

            topology.push_back(st.top());

            st.pop();
        }

        return topology;
    }
};
```

---

# Dry Run

Graph:

```text
0 → 1
0 → 2
1 → 3
2 → 3
```

DFS:

```text
0
 ├── 1
 │    └── 3
 └── 2
```

Push order:

```text
3
1
2
0
```

Stack output:

```text
0 2 1 3
```

Possible topological order.

---

# Time Complexity

| Operation | Complexity |
|---|---|
| DFS Traversal | O(V + E) |
| Stack Operations | O(V) |

Total:

```text
O(V + E)
```

---

# Space Complexity

| Structure | Complexity |
|---|---|
| Visited Array | O(V) |
| Stack | O(V) |
| Recursion Stack | O(V) |

Total:

```text
O(V)
```

---

# Important Points

## 1. Works only for DAG

If cycle exists:

```text
Topological Sort not possible
```

---

## 2. Multiple valid answers possible

Example:

```text
0 → 2
1 → 2
```

Possible answers:

```text
0 1 2
```

or

```text
1 0 2
```

Both correct.

---

# Key Line

```cpp
st.push(curr);
```

Why after DFS?

Because:

```text
Dependencies should come first
```

---

# Interview One-Line Explanation

```text
In DFS based topological sort, we push a node into stack after visiting all its neighbors, so dependencies automatically come before dependent nodes.
```
