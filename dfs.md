Depth- First Search (DFS)
---

TEMPLATES FOR DFS
---


1. Graphs Template
---

vector<vector<int>> adj;

void dfs(int node, vector<vector<int>>& adj, vector<int>& vis) {

    vis[node] = 1;

    for(int nei : adj[node]) {

        if(!vis[nei]) {
            dfs(nei, adj, vis);
        }
    }
}

vector<int> vis(n,0);

dfs(0, adj, vis);


2. DFS on a Grid Template
---

void dfs(int r, int c,
         vector<vector<int>>& grid) {

    int rows = grid.size();
    int cols = grid[0].size();

    if(r < 0 || c < 0 ||
       r >= rows || c >= cols ||
       grid[r][c] == 0)
        return;

    grid[r][c] = 0;

    dfs(r+1,c,grid);
    dfs(r-1,c,grid);
    dfs(r,c+1,grid);
    dfs(r,c-1,grid);
}


3. DFS with Directions Array Template
---

int dr[4] = {-1,1,0,0};
int dc[4] = {0,0,-1,1};

void dfs(int r, int c,
         vector<vector<int>>& grid){

    int rows = grid.size();
    int cols = grid[0].size();

    if(r<0 || c<0 ||
       r>=rows || c>=cols ||
       grid[r][c]==0)
        return;

    grid[r][c] = 0;

    for(int i=0;i<4;i++){
        dfs(r + dr[i],
            c + dc[i],
            grid);
    }
}

4. DFS returning something Template
---

int dfs(int r, int c,
        vector<vector<int>>& grid){

    int rows = grid.size();
    int cols = grid[0].size();

    if(r<0 || c<0 ||
       r>=rows || c>=cols ||
       grid[r][c]==0)
        return 0;

    grid[r][c] = 0;

    return 1
         + dfs(r+1,c,grid)
         + dfs(r-1,c,grid)
         + dfs(r,c+1,grid)
         + dfs(r,c-1,grid);
}

5. DFS + Backtracking Template
---

void dfs(...) {

    choose;

    dfs(...);

    undo;
}

Ex: path.push_back(node);

dfs(next);

path.pop_back();
