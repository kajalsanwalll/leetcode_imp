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

class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int totalTank =0;
        int currTank =0;
        int start =0;

        for(int i=0; i< gas.size();i++){
            int gain = gas[i] - cost[i];

            currTank += gain;
            totalTank += gain;

            if(currTank < 0){
                start = i+1;
                currTank = 0;
            }
        }
        return (totalTank >= 0)? start : -1;
    }
};

O(n)
