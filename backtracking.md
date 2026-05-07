12. Backtracking
--

At least these.

LeetCode Subsets
---

class Solution {
public:
    vector<vector<int>> ans;
    void sol(int index,vector<int>&nums, vector<int>& temp){
        
        if(index>= nums.size()){
            ans.push_back(temp);
            return;
        }
        temp.push_back(nums[index]);
        sol(index+1,nums,temp);
        temp.pop_back();
        sol(index+1,nums,temp);
    }

    vector<vector<int>> subsets(vector<int>& nums) {
        vector<int> temp;
        sol(0,nums,temp);
        return ans;


    }
};

TIME O(2^n *n);
space O(n);

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
