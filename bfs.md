Breadth- First Search (BFS)
---

Remember: BFs (bestfriends : always close).   
uses a queue

Biggest Rule
---

If the problem says:
shortest path.  
minimum moves.  
minimum operations.   
minimum jumps.   
nearest.   
closest.   
fewest steps.   
🚨 Think BFS first.


Template BFS
---

queue<int> q;

q.push(src);
vis[src] = 1;

while(!q.empty()){
    int node = q.front();
    q.pop();

    for(auto c : adj[node]){
        if(!vis[c]){
            vis[c] = 1;
            q.push(c);
        }
    }
}

Key Points
---

Input is edges?
→ Build adj.

Need BFS/DFS?
→ Create visited array.

Undirected?
→ Add both directions.

Directed?
→ Add one direction.

Need shortest path?
→ BFS.

Need exploration/components?
→ DFS or BFS.


Find if path exists in Graph
---

class Solution {
public:
    bool validPath(int n, vector<vector<int>>& edges, int source, int destination) {
        vector<vector<int>> adj(n);

        for(auto& e : edges){
            adj[e[0]].push_back(e[1]);
            adj[e[1]].push_back(e[0]);
        }

        vector<int> vis(n,0);
        queue<int> q;
        q.push(source);
        vis[source] = 1;

        while(!q.empty()){
            int node = q.front();
            q.pop();
            if(node == destination){
                return true;
            }

            for(auto c : adj[node]){
                if(!vis[c]){
                    vis[c] = 1;
                    q.push(c);
                }
            }
        }
        return false;
    }
};


Number of provinces
---

class Solution {
public:
    int findCircleNum(vector<vector<int>>& isConnected) {
        int n = isConnected.size();

        vector<vector<int>> adj(n);

        for(int i=0;i<n;i++){
            for(int j=0; j<n;j++){
                if(i != j && isConnected[i][j] == 1){
                    adj[i].push_back(j);
                }
            }
        }

        vector<int> vis(n,0);
        int count =0;
        
        for(int i=0;i<n;i++){

            if(!vis[i]){

                count++;

                queue<int> q;
                q.push(i);
                vis[i] = 1;

                while(!q.empty()){
                    int node = q.front();
                    q.pop();

                    for(auto c : adj[node]){
                        if(!vis[c]){
                            vis[c] = 1;
                            q.push(c);
                        }
                    }
                }
            }
        }
        return count;
        
    }
};


Keys and Rooms
---

class Solution {
public:
    bool canVisitAllRooms(vector<vector<int>>& rooms) {
        int n = rooms.size();
        vector<int> key(n,0);

        queue<int> q;
        q.push(0);
        key[0] = 1;

        while(!q.empty()){
            int node = q.front();
            q.pop();

            for(auto c : rooms[node]){
                if(!key[c]){
                    key[c] = 1;
                    q.push(c);
                }
            }
        } 
        for(int i=0;i<n;i++){
            if(!key[i]){
                return false;
            }
        }
        return true;
    }
};

Binary tree level order traversal
---

class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> ans;
        queue<TreeNode*> q;

        if(!root) return {};
        q.push(root);

        while(!q.empty()){
            int size = q.size();
            vector<int> level;

            while(size--){
                TreeNode* node = q.front();
                q.pop();
                level.push_back(node->val);

                if(node->left) q.push(node->left);
                if(node->right) q.push(node->right);

            }
            ans.push_back(level);
        }
        return ans;
    }
};

Rotting Oranges
---

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



01 Matrix
---

class Solution {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        int rows = mat.size();
        int cols = mat[0].size();
        queue<pair<int,int>> q;
        vector<vector<int>> vis(rows, vector<int>(cols,-1));

        for(int r=0;r<rows;r++){
            for(int c=0;c<cols;c++){
                if(mat[r][c] == 0){
                    q.push({r,c});
                    vis[r][c] = 0;
                }
            }
        }
        vector<int> dr = {-1,1,0,0};
        vector<int> dc = {0,0,-1,1};

        while(!q.empty()){

            auto [r,c] = q.front();
            q.pop();
            
            for(int j=0;j<4;j++){
                
                int nr = r + dr[j];
                int nc = c + dc[j];

                if(nr>=0 && nr< rows && nc>=0 && nc<cols && vis[nr][nc] == -1){
                      vis[nr][nc] = vis[r][c] + 1;
                      q.push({nr,nc});
                }
                
            }
        }
        return vis;
    }
};


Use 2 for loops inside while loop when u care about levels, like if with each level mins increase or fresh-- etc. otherwise go for one loop


Shortest Path in Binary Matrix
---

class Solution {
public:
    int shortestPathBinaryMatrix(vector<vector<int>>& grid) {
        int rows = grid.size();
        int cols = grid[0].size();
        vector<vector<int>> vis(rows,vector<int>(cols,-1));

        if(grid[0][0] != 0 || grid[rows-1][rows-1] == 1){
            return -1;
        }

        queue<pair<int,int>> q;

        q.push({0,0});
        vis[0][0] = 1;

        int dr[8] = {-1,-1,-1,0,0,1,1,1};
        int dc[8] = {-1,0,1,-1,1,-1,0,1};

        while(!q.empty()){
            auto [r,c] = q.front();
            q.pop();

            if(r == rows-1 && c == rows-1){
                return vis[r][c];
            }

            for(int j=0;j<8;j++){
                int nr = r+ dr[j];
                int nc = c + dc[j];

                if(nr>=0 && nr<rows && nc>=0 && nc<cols && grid[nr][nc] == 0 && vis[nr][nc] == -1 ){
                    vis[nr][nc] = 1 + vis[r][c];
                    q.push({nr,nc});
                }
            }
        }
        return -1;
    }
};

Max Area of Island
---

class Solution {
public:
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        int rows = grid.size();
        int cols = grid[0].size();
        vector<vector<int>> vis(rows,vector<int>(cols,-1));
        int ans =0;

        int dr[4] = {-1,1,0,0};
        int dc[4] = {0,0,-1,1};

        for(int r=0;r<rows;r++){
            for(int c=0;c<cols;c++){

                if(grid[r][c] == 1 && vis[r][c] == -1){

                    int area = 0;
                    queue<pair<int,int>> q;
                    q.push({r,c});
                    vis[r][c]=1;

                    while(!q.empty()){

                    auto [r,c] = q.front();
                    q.pop();

                    area++;

                    for(int j=0;j<4;j++){
                        int nr= r + dr[j];
                        int nc = c + dc[j];

                        if(nr>=0 && nr<rows && nc>=0 && nc<cols && vis[nr][nc] == -1 && grid[nr][nc] == 1){
                            vis[nr][nc] = 1 ;
                            q.push({nr,nc});
                        }
                    }
                }
                ans = max(ans,area);
                }
                
            }
        }
        return ans;
    }
};
