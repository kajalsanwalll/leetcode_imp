4. Intervals

Amazon loves interval merging.

LeetCode Merge Intervals
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


LeetCode Insert Interval
---


LeetCode Meeting Rooms
---
