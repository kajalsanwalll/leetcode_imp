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

