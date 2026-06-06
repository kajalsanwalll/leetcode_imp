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

    for(auto nbr : adj[node]){
        if(!vis[nbr]){
            vis[nbr] = 1;
            q.push(nbr);
        }
    }
}