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

Que: 
You are given an array of meeting time intervals where:
intervals[i] = [start_i, end_i]
Determine if a person could attend all meetings.
Input
intervals = [[start1, end1], [start2, end2], ...]
 Output
Return true if a person can attend all meetings
Return false if any meetings overlap

 Example 1
Input: intervals = [[0,30],[5,10],[15,20]]
Output: false
 Explanation:
Meeting [0,30] overlaps with [5,10]


Solution:

class Solution {
public:
    bool canAttendMeetings(vector<vector<int>>& intervals) {
        
        sort(intervals.begin(),intervals.end());

        for(int i=1;i<intervals.size();i++;){
            if(intervals[i][0] < intervals[i-1][1]){
                return false;
            }
        }
        return true;
    }
};

Order(n log n);


Meeting room 2 ✅
---

❓ Problem
Minimum number of rooms required so all meetings can happen.
💡 Intuition (this is key)
👉 If meetings overlap → need more rooms
👉 If one ends before another starts → reuse room
🧪 Example
[[0,30],[5,10],[15,20]]

Solution:

class Solution {
public:
    int minMeetingRooms(vector<vector<int>>& intervals) {
        
       sort(intervals.begin(),intervals.end());

       priority_queue<int, vector<int>,greater<int>> pq;

       for(auto interval : intervals){
         if(!pq.empty() && pq.top() <= interval[0]){
            pq.pop();
         }
         pq.push(interval[1]);
       }

       return pq.size();
    }
};

Order(n logn);

Non- overlapping Intervals
---

class Solution {
public:
    int eraseOverlapIntervals(vector<vector<int>>& intervals) {
        
        int res=0;
        sort(intervals.begin(),intervals.end(),
            [](vector<int>& a, vector<int>& b){
             return a[1] < b[1];
            });

        int prevEnd = intervals[0][1];
        for(int i=1; i<intervals.size();i++){
            
            if(intervals[i][0] < prevEnd){
                res += 1;
            }else{
                prevEnd = intervals[i][1];
            }
            
        }
        return res;
    }
};

Order(n)
