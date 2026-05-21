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


Coin change
---

class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<int> dp(amount + 1, amount + 1);
        dp[0] = 0;

        for(int i=1; i<=amount;i++){
            for(int coin : coins){
                if(i-coin >= 0){
                    dp[i] = min(dp[i], dp[i-coin]+1);
                }
            }
        }
        return dp[amount] == amount + 1 ? -1 : dp[amount];
    }
};

Time Complexity
O(amount × number_of_coins)
Space Complexity
O(amount)


Longest increasing subsequence
---

class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        vector<int> dp(nums.size(),1);
        int ans = 1;

        for(int i=0;i<nums.size();i++){
            for(int j=0;j<i;j++){
                if(nums[j]<nums[i]){
                    dp[i] = max(dp[i],dp[j]+1);
                }
            }
            ans = max(ans,dp[i]);
        }
        return ans;
    }
};

Time Complexity
O(n²)
Space Complexity
O(n)


APPROACH 2 : O(n log n) time;


class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        vector<int> ans;
        for(int num : nums){
            auto i = lower_bound(ans.begin(),ans.end(),num);

            if(i==ans.end()){
                ans.push_back(num);
            }else{
                *i = num;
            }
        }
        return ans.size();
    }
};