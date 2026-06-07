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


Template BFS for graphs
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

Template BFS for Grids
---

class Solution {
public:
    void bfs(int sr, int sc,
             vector<vector<int>>& grid,
             vector<vector<int>>& vis) {

        int rows = grid.size();
        int cols = grid[0].size();

        queue<pair<int,int>> q;

        q.push({sr, sc});
        vis[sr][sc] = 1;

        int dr[4] = {-1, 1, 0, 0};
        int dc[4] = {0, 0, -1, 1};

        while(!q.empty()) {

            auto [r, c] = q.front();
            q.pop();

            // Process current cell here

            for(int k = 0; k < 4; k++) {

                int nr = r + dr[k];
                int nc = c + dc[k];

                if(nr >= 0 && nr < rows &&
                   nc >= 0 && nc < cols &&
                   !vis[nr][nc]) {

                    vis[nr][nc] = 1;
                    q.push({nr, nc});
                }
            }
        }
    }
};

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


Surrounded Regions
---

class Solution {
public:
    void solve(vector<vector<char>>& board) {
        int rows = board.size();
        int cols = board[0].size();

        vector<vector<int>> vis(rows,vector<int>(cols,-1));
        queue<pair<int,int>> q;

        for(int r=0;r<rows;r++){
            for(int c=0;c<cols;c++){
                if(r==0 || r == rows-1 || c ==0 || c == cols-1 ){
                    
                    if(board[r][c] == 'O' && vis[r][c] == -1){
                        q.push({r,c});
                        vis[r][c]=1;
                    }

                }
            }
        }

        int dr[4] = {-1,1,0,0};
        int dc[4] = {0,0,-1,1};

        while(!q.empty()){
            auto [r,c] = q.front();
            q.pop();

            for(int j=0;j<4;j++){
                int nr = r + dr[j];
                int nc = c + dc[j];

                if(nr>=0 && nr<rows && nc>=0 && nc<cols && vis[nr][nc] == -1 && board[nr][nc] == 'O'){
                    vis[nr][nc] = 1;
                    q.push({nr,nc});
                }
            }
        }
        for(int r=0;r<rows;r++){
            for(int c=0;c<cols;c++){
                if(board[r][c] == 'O' && vis[r][c] == -1){
                    
                    board[r][c] = 'X';
                }
            }
        }
    }
};


Open the lock
---

class Solution {
public:
    int openLock(vector<string>& deadends, string target) {
        unordered_set<string> dead(deadends.begin(),deadends.end());
        queue<pair<string,int>> q;
        unordered_set<string> vis;

        if(dead.count("0000")) return -1;

        q.push({"0000",0});
        vis.insert("0000");

        while(!q.empty()){
            auto [curr,steps] = q.front();
            q.pop();

            if(curr == target){
                return steps;
            }
            for(int i=0;i<4;i++){
                int ch = curr[i];

                //forward

                if(curr[i] == '9'){
                    curr[i] = '0';
                }else{
                    curr[i] = ch+1;
                }

                if(!dead.count(curr) && !vis.count(curr)){
                    vis.insert(curr);
                    q.push({curr,steps+1});
                }

                //restore

                curr[i] = ch;

                //backward

                if(curr[i] == '0'){
                    curr[i] = '9';
                }else{
                    curr[i] = ch-1;
                }

                if(!dead.count(curr) && !vis.count(curr)){
                    vis.insert(curr);
                    q.push({curr,steps+1});
                }
                curr[i] = ch;
            }
        }
        return -1;
    }
};

Word Ladder
---

class Solution {
public:
    int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
        unordered_set<string> s(wordList.begin(), wordList.end());
        queue<pair<string,int>> q;

        if(s.find(endWord) == s.end()){
            return 0;
        }
        q.push({beginWord,1});

        while(!q.empty()){
            auto [word,steps] = q.front();
            q.pop();

            if(word == endWord){
                return steps;
            }

            for(int i=0;i<word.size();i++){
                string curr = word;

                for(char c = 'a'; c<= 'z';c++){
                    curr[i] = c;

                    if(s.find(curr) != s.end() ){
                    q.push({curr,steps+1});
                    s.erase(curr);
                }
                }
            }
        }
        return 0;
    }
};

Nearest exit from entrance in maze
---

class Solution {
public:
    int nearestExit(vector<vector<char>>& maze, vector<int>& entrance) {
        int rows = maze.size();
        int cols = maze[0].size();

        queue<pair<int,int>> q;
        q.push({entrance[0],entrance[1]});

        maze[entrance[0]][entrance[1]] = '+';

        int dr[4] = {-1,1,0,0};
        int dc[4] = {0,0,-1,1};
        int steps =0;

        while(!q.empty()){
            int size = q.size();

            while(size--){
                auto [one,two] = q.front();
                q.pop();

                if(!(one == entrance[0] && two == entrance[1]) &&(one==0 || one== rows-1 || two==0 || two== cols-1)){
                    
                    return steps;
                    
                }

                for(int i=0;i<4;i++){
                  int nr = one + dr[i];
                  int nc = two + dc[i];

                 if(nr>=0 && nr<rows && nc>=0 && nc<cols && maze[nr][nc] == '.'){
                      maze[nr][nc] = '+';
                      q.push({nr,nc});
                    
                    }
                }
            }
            steps++;
        }
        return -1;
    }
};


Bus Routes
---

class Solution {
public:
    int numBusesToDestination(vector<vector<int>>& routes, int source, int target) {
        unordered_map<int,vector<int>> stopToBus;
        if(source == target){
            return 0;
        }

        for(int bus=0; bus<routes.size();bus++){
            for(int stop : routes[bus]){
                stopToBus[stop].push_back(bus);
            }
        }
        queue<pair<int,int>> q;
        q.push({source,0});
        unordered_set<int> visStops;
        unordered_set<int> visBus;

        visStops.insert(source);

        while(!q.empty()){
            auto [stop,taken] = q.front();
            q.pop();

            for(int bus : stopToBus[stop]){
                if(visBus.count(bus)){
                    continue;
                }
                visBus.insert(bus);

                for(int nextStop : routes[bus]){
                    if(nextStop == target){
                        return 1 + taken;
                    }
                    if(!visStops.count(nextStop)){
                        visStops.insert(nextStop);
                        q.push({nextStop,taken+1});
                    }
                }
            }
        }
        return -1;
    }
};