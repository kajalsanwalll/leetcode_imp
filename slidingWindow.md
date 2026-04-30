2. Sliding Window
---

Very common in OA.

Maximum Sum of Subarray of Size K
---

int maxSum(vector<int>& nums, int k) {
    
    int windowSum = 0;
    for (int i = 0; i < k; i++) {
        windowSum += nums[i];
    }

    int maxSum = windowSum;

    for (int i = k; i < nums.size(); i++) {
        windowSum += nums[i] - nums[i-k];
        maxSum = max(maxSum, windowSum);
    }

    return maxSum;
}

Order(n);


Best Time to Buy and Sell Stock
--

class Solution {
public:
    int maxProfit(vector<int>& prices) {

        int n = prices.size();
        int i= prices[0]; int profit=0;

        for(int j=1;j<n;j++){
            if(i >prices[j]){
                i = prices[j]; 
            }

            profit = max(profit, prices[j] - i);
        }
        return profit;
    }
};

Order(n);

Longest Substring Without Repeating Characters
--

int lengthOfLongestSubstring(string s) {
    unordered_set<char> seen;
    int left = 0, longest = 0;

    for (int right = 0; right < s.size(); right++) {
        while (seen.count(s[right])) {
            seen.erase(s[left]);
            left++;
        }

        seen.insert(s[right]);
        longest = max(longest, right - left + 1);
    }

    return longest;
}

Order(n);


Permutation in String
---

Minimum Size Subarray Sum
---

Why:
Amazon OA frequently asks window + hashmap.