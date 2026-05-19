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


Jump Game 2
---

class Solution {
public:
    int jump(vector<int>& nums) {
        int jumps =0;
        int l=0,r=0;

        while(r < nums.size() - 1){
            int farthest = 0;
            for(int i=l;i<=r;i++){
                farthest = max(farthest, i + nums[i]);
            }
            l=r+1;
            r=farthest;

            jumps++;
        }
        return jumps;
    }
};


Hand of Straights
---

class Solution {
public:
    bool isNStraightHand(vector<int>& hand, int groupSize) {
        int n = hand.size();

        if(n%groupSize != 0) return false;

        map<int,int> mp;
        for(int x : hand){
            mp[x]++;
        }

        for(auto &[card,freq] : mp){
            int count = freq;

            if(freq > 0){

                for(int i=0 ; i< groupSize; i++){
                    int curr = card + i;

                    if(mp.find(curr) == mp.end() || mp[curr] < count){
                        return false;
                    }
                    mp[curr]-= count;
                }
            }
        }
        return true;
    }
};
