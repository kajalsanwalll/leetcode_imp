13. One DP

Just one easy DP.

LeetCode Climbing Stairs
---

APPROACH 1


class Solution {
public:
    int climbStairs(int n) {
        if(n==0 || n == 1){
            return 1;
        }
        vector<int> dp(n+1);
        dp[0] = dp[1] = 1;
        
       for(int i=2;i<=n;i++){
        dp[i] = dp[i-1]+dp[i-2];
       }
       return dp[n];
        
    }
};

APPROACH 2

class Solution {
public:
    int climbStairs(int n) {
        if(n==0 || n == 1){
            return 1;
        }
        int prev=1; int curr =1;

        for(int i=2;i<=n;i++){
            int temp = curr;
            curr = prev + curr;
            prev = temp;
        }
        return curr;
    }
};


House Robber
---

class Solution {
public:
    int rob(vector<int>& nums) {
        
        int sum1=0,sum2=0;

        for(int num : nums){
            
            int ans = max(num+sum2,sum1);
            sum2 = sum1;
            sum1 = ans;
        }
        return sum1;
    }
};