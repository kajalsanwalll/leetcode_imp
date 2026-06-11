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
---

class MedianFinder {
public:

    priority_queue<int> leftMax;

    priority_queue<int, vector<int>, greater<int>> rightMin;

    MedianFinder() {
        
    }
    
    void addNum(int num) {

        // step 1
        leftMax.push(num);

        // step 2
        rightMin.push(leftMax.top());
        leftMax.pop();

        // step 3
        if(rightMin.size() > leftMax.size()) {
            leftMax.push(rightMin.top());
            rightMin.pop();
        }
    }
    
    double findMedian() {

        if(leftMax.size() > rightMin.size()) {
            return leftMax.top();
        }

        return (leftMax.top() + rightMin.top()) / 2.0;
    }
};

time O(log n);
space O(1);


Reorganize String
---

class Solution {
public:
    string reorganizeString(string s) {
        int n = s.size();
        unordered_map<char,int> freq;
        for(char c : s){
            freq[c]++;
        }
        for(auto x : freq){
            if(x.second > (n+1)/2){
                return "";
            }
        }
        priority_queue<pair<int,char>> pq;
        for(auto c : freq){
            pq.push({c.second,c.first});
        }
        string ans = "";

        while(pq.size() >= 2){
            auto one = pq.top();
            pq.pop();

            auto two = pq.top();
            pq.pop();

            ans+= one.second;
            ans+= two.second;

            one.first--;
            two.first--;

            if(one.first > 0){
                pq.push(one);
            }
            if(two.first > 0){
                pq.push(two);
            }
        }
        if(!pq.empty()){
            ans+= pq.top().second;
        }
        return ans;
    }
};

time O(n);
space O(1);


Design Twitter
---


class Twitter {
public:

    int timer = 0;

    // follower -> followees
    unordered_map<int, unordered_set<int>> followMap;

    // user -> {time, tweetId}
    unordered_map<int, vector<pair<int,int>>> tweetMap;

    Twitter() {
    }
    
    void postTweet(int userId, int tweetId) {

        tweetMap[userId].push_back({timer++, tweetId});
    }
    
    vector<int> getNewsFeed(int userId) {

        vector<int> feed;

        // user should follow themselves
        followMap[userId].insert(userId);

        priority_queue<vector<int>> pq;

        // push latest tweet of every followee
        for(int followee : followMap[userId]){

            auto &tweets = tweetMap[followee];

            if(tweets.size() > 0){

                int idx = tweets.size() - 1;

                pq.push({
                    tweets[idx].first,   // timestamp
                    tweets[idx].second,  // tweetId
                    followee,
                    idx
                });
            }
        }

        while(!pq.empty() && feed.size() < 10){

            auto top = pq.top();
            pq.pop();

            int time = top[0];
            int tweetId = top[1];
            int followee = top[2];
            int idx = top[3];

            feed.push_back(tweetId);

            // push older tweet
            if(idx > 0){

                pq.push({
                    tweetMap[followee][idx-1].first,
                    tweetMap[followee][idx-1].second,
                    followee,
                    idx-1
                });
            }
        }

        return feed;
    }
    
    void follow(int followerId, int followeeId) {

        followMap[followerId].insert(followeeId);
    }
    
    void unfollow(int followerId, int followeeId) {

        if(followerId != followeeId){
            followMap[followerId].erase(followeeId);
        }
    }
};


Smallest range covering elements from K lists
---

class Solution {
public:
    vector<int> smallestRange(vector<vector<int>>& nums) {
        priority_queue<vector<int>,vector<vector<int>>,greater<vector<int>>> pq;

        int currMax = INT_MIN;
        int k = nums.size();
        for(int i=0; i<k ; i++){

            pq.push({nums[i][0], i, 0});
            currMax = max(currMax, nums[i][0]);
        }
        
        int start = 0;
        int end = INT_MAX;
        
        while(pq.size() == k){

            auto top = pq.top();
            pq.pop();

            int currMin = top[0];
            int row = top[1];
            int col = top[2];

            if(currMax - currMin < end - start){
                start = currMin;
                end = currMax;
            }

            if(col + 1 < nums[row].size()){

                int nextVal = nums[row][col + 1];
                pq.push({nextVal, row, col + 1});
                currMax = max(currMax, nextVal); 
            }
        }
        return {start, end};
    }
};

hint: basically always keep 1 element from each list and keep a track of range {max,min} and keep popping out the minimum digit and replace it with another digit from same list.

Each push/pop:
O(log k)

total time : O(n log k)
total space: O(k)


Merge k sorted lists
---

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        auto cmp = [](ListNode* a, ListNode* b){
            return a->val > b->val;
        };

        priority_queue<ListNode*,vector<ListNode*>,decltype(cmp)> pq(cmp);

        for(auto c : lists){
            if(c){
              pq.push(c);
            }
        }
        ListNode dummy(0);
        ListNode* tail = &dummy;

        while(!pq.empty()){
            ListNode* a = pq.top();
            pq.pop();
            
            tail->next = a;
            tail = a;

            if(a->next){
                pq.push(a->next);
            }
        }
        return dummy.next;
    }
};


IPO
---

class Solution {
public:
    int findMaximizedCapital(int k, int w, vector<int>& profits, vector<int>& capital) {

        int n = profits.size();
        vector<pair<int,int>> projects;

        for(int i=0;i<n;i++){
            projects.push_back({capital[i],profits[i]});
        }
        sort(projects.begin(),projects.end());

        priority_queue<int> pq;
        int i=0;

        while(k--){

            while( i<n && projects[i].first <= w){
                pq.push(projects[i].second);
                i++;
            }
            if(pq.empty()){
                break;
            }
            w+= pq.top();
            pq.pop();
        }
        return w;
    }
};

Time O(n logn);
Space O(n);


Max performance of a team
---

class Solution {
public:
    int maxPerformance(int n, vector<int>& speed, vector<int>& efficiency, int k) {
        int MOD = 1e9 + 7;

        vector<pair<int,int>> engineers; //array

        for(int i=0;i<n;i++){
            engineers.push_back({efficiency[i],speed[i]});
        }
        sort(engineers.rbegin(),engineers.rend()); 

        priority_queue<int, vector<int>,greater<int>> pq; //min heap

        long long speedSum=0;
        long long ans =0;

        for(auto& e : engineers){
            int currEff = e.first;
            int currSpeed = e.second;

            pq.push(currSpeed);
            speedSum += currSpeed;

            while(pq.size() > k){
                speedSum -= pq.top();
                pq.pop();
            }
            ans = max(ans,speedSum*currEff);
        }
        return ans%MOD;
    }
};

time O(n log n);
space O(n);

Furthest building you can reach
---

class Solution {
public:
    int furthestBuilding(vector<int>& heights, int bricks, int ladders) {
        int n = heights.size();
        priority_queue<int,vector<int>,greater<int>> pq; //min heap

        for(int i=0;i<n-1;i++){
            int diff = heights[i+1]-heights[i];

            if(diff > 0){
                pq.push(diff);
                if(pq.size() > ladders){
                    bricks -= pq.top();
                    pq.pop();
                }
                if(bricks < 0){
                    return i;
                }
            }
        }
        return heights.size()-1;
    }
};

Amazon really likes heaps.