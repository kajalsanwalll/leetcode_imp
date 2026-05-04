11. Greedy
--

High frequency.

LeetCode Jump Game
---

class Solution {
public:
    bool canJump(vector<int>& nums) {
        int n = nums.size();
        int maxLen =0;
        for(int i=0;i<n;i++){
            if(i> maxLen) return false;
            maxLen = max(maxLen, i + nums[i]);
        }
        
        return true;
    }
};

o(n);

LeetCode Gas Station
---


