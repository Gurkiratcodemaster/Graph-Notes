# Cycle Detection in Directed Graph using DFS

## Main Idea

A cycle exists in a directed graph if:

- Node is already visited
- And that node is also present in current DFS path

We use two arrays:

| Array | Purpose |
|---|---|
| `vis[]` | Checks if node was visited before |
| `recPath[]` | Checks if node is in current recursion stack/path |

---

# Algorithm Steps

## Step 1

Mark current node as visited.

```cpp
vis[curr] = true;
```

---

## Step 2

Add current node into recursion path.

```cpp
recPath[curr] = true;
```

---

## Step 3

Traverse all neighbors.

```cpp
for(auto v : adj[curr])
```

---

## Step 4

If neighbor is not visited:

```cpp
if(!vis[v])
```

Call DFS again.

```cpp
if(dfs(v, adj, vis, recPath))
    return true;
```

If deeper DFS finds cycle, return true.

---

## Step 5

If neighbor is already visited and also present in recursion path:

```cpp
else if(recPath[v])
```

Then cycle exists.

```cpp
return true;
```

---

## Step 6

After finishing DFS of current node:

Remove node from recursion path.

```cpp
recPath[curr] = false;
```

Because now backtracking starts.

---

# Complete Code

```cpp
bool dfs(int curr,
         vector<int> adj[],
         vector<bool>& vis,
         vector<bool>& recPath)
{
    vis[curr] = true;
    recPath[curr] = true;

    for(auto v : adj[curr])
    {
        if(!vis[v])
        {
            if(dfs(v, adj, vis, recPath))
                return true;
        }
        else if(recPath[v])
        {
            return true;
        }
    }

    recPath[curr] = false;

    return false;
}
```

---

# Important Difference

## `vis[]`

```text
Node was visited anytime before
```

---

## `recPath[]`

```text
Node is currently present in DFS recursion stack
```

---

# Example

```text
1 → 2 → 3
    ↑   ↓
    ← ← 4
```

DFS traversal:

```text
1 → 2 → 3 → 4
```

From `4`, we again reach `2`.

At that moment:

```text
vis[2] = true
recPath[2] = true
```

So cycle exists.

---

# Time Complexity

```text
O(V + E)
```

Where:

- `V` = Vertices
- `E` = Edges

---

# Space Complexity

```text
O(V)
```

Used for:

- `vis[]`
- `recPath[]`
- Recursion stack

---

# Memory Trick

```text
Visited + Present in current DFS path = Cycle
```
