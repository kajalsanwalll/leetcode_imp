7. Heap / Priority Queue
--

Super high priority.

LeetCode Kth Largest Element in an Array
---

class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        if(nums.size() == 1){
            return nums[0];
        }
        int ans = 0;
        priority_queue<int> pq;
        
        for(int i=0; i<nums.size()-1;i++){
            while(i< nums.size()){
                pq.push(nums[i]);
                i++;
            }

            while(k--){
                
                ans = pq.top();
                pq.pop();
                if(k == 0){
                    return ans;
                }
            }
        }
        return ans;
    }
};

Order(n);

LeetCode K Closest Points to Origin
---

class Solution {
public:
    vector<vector<int>> kClosest(vector<vector<int>>& points, int k) {
        priority_queue<pair<int,vector<int>>> pq;

        for(auto& c : points){
            int dist = c[0]*c[0] + c[1]*c[1];
            pq.push({dist,c});

            if(pq.size()>k){
                pq.pop();
            }
        }

        vector<vector<int>> ans;
        while(!pq.empty()){
            ans.push_back(pq.top().second);
            pq.pop();
        }
        return ans;
    }
};

Order (n log k);

LeetCode Task Scheduler
---

APPROACH 1

class Solution {
public:
    int leastInterval(vector<char>& tasks, int n) {
        vector<int> freq(26,0);

        for(char c : tasks){
            freq[c-'A']++;
        }

        int mx = *max_element(freq.begin(),freq.end());

        int cnt=0;

        for(int f : freq){
            if(f == mx){
                cnt++;
            }
        }
        return max((int)tasks.size(), (mx -1)* (n+1) + cnt);

    }
};

Time Order(n);
Space Order(1); 


APPROACH2 

class Solution {
public:
    int leastInterval(vector<char>& tasks, int n) {

        vector<int> freq(26, 0);

        for(char c : tasks) {
            freq[c - 'A']++;
        }

        priority_queue<int> pq;

        for(int f : freq) {
            if(f > 0) {
                pq.push(f);
            }
        }

        int time = 0;

        while(!pq.empty()) {

            vector<int> temp;

            int cycle = n + 1;

            // process one block
            while(cycle > 0 && !pq.empty()) {

                int cnt = pq.top();
                pq.pop();

                cnt--;

                if(cnt > 0) {
                    temp.push_back(cnt);
                }

                time++;
                cycle--;
            }

            // push remaining tasks back
            for(int x : temp) {
                pq.push(x);
            }

            // if heap empty -> no idle needed
            if(pq.empty()) break;

            // otherwise add idle slots
            time += cycle;
        }

        return time;
    }
};

Order( n); time
order(1); space

LeetCode Find Median from Data Stream

Amazon really likes heaps.