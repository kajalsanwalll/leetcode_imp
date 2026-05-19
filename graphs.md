10. Graphs
--

Only the essentials.

LeetCode Number of Islands
---

class Solution {
public:
    void dfs(vector<vector<char>>&grid, int r, int c){
        int rows = grid.size();
        int cols = grid[0].size();

        if(r<0 || c<0 || r>=rows || c>= cols || grid[r][c] == '0'){
            return;
        }

        grid[r][c] = '0'; //visited

        dfs(grid, r+1, c); //down
        dfs(grid, r-1, c); //top
        dfs(grid, r, c+1); //right
        dfs(grid, r, c-1); //left
        
    }

    int numIslands(vector<vector<char>>& grid) {
        
        int rows = grid.size();
        int cols = grid[0].size();
        int count = 0;

        for(int r=0;r<rows;r++){
            for(int c=0;c<cols;c++){
                if(grid[r][c] == '1'){
                    count++;
                    dfs(grid,r,c);
                };
            }
        }
        return count;
    }   
};

LeetCode Clone Graph
---

class Solution {
public:
    unordered_map<Node*,Node*> mp;
    Node* cloneGraph(Node* node) {
       if(!node){
        return NULL;
       }

       if(mp.count(node)) return mp[node]; //already cloned

       Node* clone = new Node(node->val);
       mp[node] = clone;

       for(Node* n : node->neighbors){
         clone->neighbors.push_back(cloneGraph(n));
       }
       return clone;
    }
};

LeetCode Course Schedule
---

class Solution {
public:
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        vector<vector<int>> adj(numCourses);
        vector<int> indegree(numCourses,0);

        for(auto& c : prerequisites){
            adj[c[1]].push_back(c[0]);
            indegree[c[0]]++;
        }

        queue<int> q;

        for(int i=0; i< numCourses;i++){
            if(indegree[i] == 0){
                q.push(i);
            }

        }
        int count = 0;

        while(!q.empty()){
            int node = q.front();
            q.pop();
            count ++;

            for(auto& n : adj[node]){
                indegree[n]--;
                if(indegree[n] == 0){
                    q.push(n);
                }
            }
        }
        return count == numCourses;
    }
};

Order(v+e);

Pacific Atlantic Water Flow
---

class Solution {
public:
    int rows,cols;
    
    void dfs(vector<vector<int>>& heights, int r, int c, vector<vector<bool>>& vis){
        vis[r][c] = true;

        vector<int> dr = {-1,1,0,0};
        vector<int> dc = {0,0,-1,1};

        for(int i=0;i<4;i++){
            int nr = r + dr[i];
            int nc = c + dc[i];

            if(nr >=0 && nr < rows && nc >= 0 && nc < cols && !vis[nr][nc] && heights[nr][nc] >= heights[r][c]){
                dfs(heights, nr, nc, vis);
            }
        }
    }
    vector<vector<int>> pacificAtlantic(vector<vector<int>>& heights) {
        rows = heights.size();
        cols = heights[0].size();

        vector<vector<bool>> pac(rows, vector<bool>(cols, false));
        vector<vector<bool>> atl(rows, vector<bool>(cols, false));

        for(int c=0;c<cols;c++){
            dfs(heights,0,c,pac);
            dfs(heights,rows-1,c,atl);
        }

        for(int r=0;r<rows;r++){
            dfs(heights,r,0,pac);
            dfs(heights,r,cols-1,atl);
        }
        vector<vector<int>> ans;

        for(int r=0;r<rows;r++){
            for(int c=0;c<cols;c++){
                if(pac[r][c] && atl[r][c]){
                    ans.push_back({r,c});
                }
            }
        }
        return ans;
    }
};

Order(m*n); time and space


Rotting Oranges
---

class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
        int rows = grid.size();
        int cols = grid[0].size();
        queue<pair<int,int>> q;

        int fresh = 0;

        for(int r=0;r<rows;r++){
            for(int c=0;c<cols;c++){
                if(grid[r][c] == 2){
                    q.push({r,c});
                }
                else if(grid[r][c] == 1){
                    fresh++;
                }
            }
        }
        if(fresh == 0) return 0;
        int min = 0;

        vector<int> dr = {-1,1,0,0};
        vector<int> dc = {0,0,-1,1};

        while(!q.empty()){
            int size = q.size();

            for(int i=0;i<size;i++){
                auto [r,c] = q.front();
                q.pop();

                for(int j=0;j<4;j++){

                    int nr = r + dr[j];
                    int nc = c + dc[j];

                    if(nr >=0 && nr < rows && nc >= 0 && nc < cols && grid[nr][nc] == 1){
                        grid[nr][nc] = 2;
                        fresh--;
                        q.push({nr,nc});
                    }
                }
            }
            min++;
        }
        if(fresh > 0) return -1;
        return min - 1;
    }
};


Order(m*n);

