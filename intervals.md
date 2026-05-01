4. Intervals

Amazon loves interval merging.

LeetCode Merge Intervals ✅
---

class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        

        vector<vector<int>> ans;
        sort(intervals.begin(), intervals.end());

        for(auto interval : intervals){
            if(ans.empty() || ans.back()[1]< interval[0]){
                ans.push_back(interval);
            }
            else{
                ans.back()[1] = max(ans.back()[1], interval[1]);
            }
        }
        return ans;

    }
};

Order(n logn); //optimal soln


LeetCode Insert Interval ✅
---

class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        

        vector<vector<int>> ans;

        for(auto interval : intervals){
            
            if(interval[1] < newInterval[0]){
                ans.push_back(interval);
            }
            else if(interval[0] > newInterval[1]){
                ans.push_back(newInterval);
                newInterval = interval;
            }
            else{
                newInterval[0] = min(newInterval[0], interval[0]);
                newInterval[1] = max(newInterval[1], interval[1]);
            }
        }
        ans.push_back(newInterval);
        return ans;
    }
};

Order(n);

LeetCode Meeting Rooms ✅
---


