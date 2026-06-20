13. DP

Universal DP Template
---

Step 1: Define the State
--
Ask:
"What minimum information completely describes my current situation?"
Usually:
dp[i]
dp[i][j]
dp[index][target]
dp[index][prev]

example:

| Problem         | State           |
| --------------- | --------------- |
| Climbing Stairs | dp[i]           |
| House Robber    | dp[i]           |
| Coin Change     | dp[amount]      |
| LCS             | dp[i][j]        |
| Knapsack        | dp[i][capacity] |
| Edit Distance   | dp[i][j]        |


Step 2: Find the Choices
--
Ask:
"From this state, what decisions can I make?"

ex:

Climbing Stairs:
take 1 step
take 2 steps

House Robber:
rob current house
skip current house

Knapsack:
pick item
don't pick item

Step 3: Write Recurrence
--
Combine the choices.

Sum
dp[state] = choice1 + choice2;

Maximum
dp[state] = max(choice1, choice2);

Minimum
dp[state] = min(choice1, choice2);

Step 4: Base Case
--
Ask:
"When does recursion stop?"

Examples:
if(i == n)
    return ...;

if(target == 0)
    return ...;

if(i < 0)
    return ...;


Step 5: Memoization
--
Generic Top-Down Template

vector<int> memo;

int solve(int state) {

    // base case
    if(...)
        return ...;

    // already computed
    if(memo[state] != -1)
        return memo[state];

    // recurrence
    return memo[state] =
           combine(
               solve(nextState1),
               solve(nextState2)
           );
}


Bottom-Up Template

Suppose recursion was:
f(i)=f(i-1)+f(i-2)
Then:

vector<int> dp(n+1);

dp[base] = value;

for(int i=...) {
    dp[i] =
        combine(
            dp[previous states]
        );
}

Space Optimization
Ask:
"Do I really need the entire DP array?"
If only previous states are used:
prev2
prev1

for(...) {
    curr = ...
    prev2 = prev1;
    prev1 = curr;
}


Complete Interview Template
---
Whenever you get a DP question, say:

1. State
I'll define dp[state] as ...

2. Transition
From the current state, I have these choices:
choice 1
choice 2
Therefore,
dp[state] =
    combine(choice1, choice2);

3. Base Cases
When ... we stop recursion.
if(...)
    return ...

4. Memoization
Since overlapping subproblems exist, I'll cache each state.

5. Complexity
Time = number of states × work per state
Space = size of dp table



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

House Robber II
---

class Solution {
public:
    int solve(vector<int>& nums, int start, int end){
        int sum1=0;
        int sum2=0;

        for(int i=end;i>=start;i--){
            int ans = max(nums[i]+sum2,sum1);
            sum2 = sum1;
            sum1 = ans;

        }
        return sum1;
    }
    int rob(vector<int>& nums) {
        int n = nums.size();
        
        if(n==1){
            return nums[0];
        }

        int notLast = solve(nums,0,n-2);
        int notFirst = solve(nums,1,n-1);

        return max(notLast,notFirst);
    }
};

House Robber III
---


class Solution {
public:
    // 2 starting states
    pair<int,int> solve(TreeNode* root){
        if(root == nullptr) return {0,0};

        auto left = solve(root->left);
        auto right = solve(root->right);

        int skipRoot = max(left.first,left.second) +
                       max(right.first,right.second);

        int takeRoot = root->val +
                       left.first +
                       right.first;
        return {skipRoot,takeRoot};               
    }
    int rob(TreeNode* root) {
        auto ans = solve(root);
        return max(ans.first,ans.second);
    }
};


Min Cost Climbing Stairs
---

class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        int first=0;
        int second=0;

        for(int n=cost.size()-1;n>=0;n--){
            int ans = cost[n] + min(first,second);
            second = first;
            first = ans;
        }
        return min(first,second);
    }
};

Fibonacci Number
---

class Solution {
public:
    int fib(int n) {
        // state = dp[i];
        if(n<=1) return n;

        vector<int> dp(n+1);
        dp[0]=0;
        dp[1]=1;

        for(int i=2;i<=n;i++){
            dp[i] = dp[i-1]+dp[i-2];
        }
        return dp[n];
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