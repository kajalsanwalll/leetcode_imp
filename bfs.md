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