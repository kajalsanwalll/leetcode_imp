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