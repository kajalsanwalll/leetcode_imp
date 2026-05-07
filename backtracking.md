12. Backtracking
--

At least these.

LeetCode Subsets
---



LeetCode Combination Sum
---

class Solution {
public:

vector<vector<int>> ans;
    void solve(int index, vector<int>& candidates,int target,vector<int>& temp){
            if(target == 0){
                ans.push_back(temp);
                return;
            }
            if(target < 0 || index>= candidates.size()) return;

            temp.push_back(candidates[index]);
            solve(index,candidates,target-candidates[index],temp);
            temp.pop_back();
            solve(index+1,candidates,target,temp);

        }

    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<int> temp;
        solve(0,candidates,target,temp);
        return ans;
    }
};

Order(2^target); time
Order(target); space
