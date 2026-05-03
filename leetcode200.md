# Number of Islands (DFS Approach)

## 🧠 Intuition (Simple Explanation)

The problem is to count how many **separate islands** exist in a 2D grid.

* `'1'` represents land
* `'0'` represents water

An **island** is formed by connecting adjacent lands (up, down, left, right).

### 💡 Approach

1. Traverse the grid cell by cell.
2. Whenever you find a `'1'` that is **not visited**, it means:

   * You found a **new island**
3. Start a **DFS (Depth First Search)** from that cell:

   * Mark all connected `'1'` cells as visited
4. Increase island count.
5. Continue scanning the grid.

### 🔁 DFS Logic

From any cell `(i, j)`:

* Go in 4 directions:

  * Up `(i-1, j)`
  * Right `(i, j+1)`
  * Down `(i+1, j)`
  * Left `(i, j-1)`
* Stop if:

  * Out of bounds
  * Already visited
  * Water (`'0'`)

---

## ⏱️ Complexity

* Time: **O(n × m)** → Each cell visited once
* Space: **O(n × m)** → For visited array + recursion stack

---

## 💻 Code (C++)

```cpp
class Solution {
public:
    void dfs(int i, int j, vector<vector<bool>> &vis, vector<vector<char>>& grid, int n, int m){
        if(i < 0 || j < 0 || i >= n || j >= m || vis[i][j] || grid[i][j] != '1'){
            return;
        }

        vis[i][j] = true;

        dfs(i - 1, j, vis, grid, n, m); // up
        dfs(i, j + 1, vis, grid, n, m); // right
        dfs(i + 1, j, vis, grid, n, m); // down
        dfs(i, j - 1, vis, grid, n, m); // left
    }

    int numIslands(vector<vector<char>>& grid) {
        int islands = 0;
        int n = grid.size();
        int m = grid[0].size();

        vector<vector<bool>> vis(n, vector<bool>(m, false));

        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(grid[i][j] == '1' && vis[i][j] == false){
                    dfs(i, j, vis, grid, n, m);
                    islands++;
                }
            }
        }

        return islands;
    }
};
```

---

## 📌 Key Takeaways

* Use DFS to **mark the full island at once**
* Avoid revisiting cells using a `visited` array
* Each DFS call = **1 complete island**

---
