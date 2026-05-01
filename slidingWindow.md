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


    unordered_set<char> SET;
    int left = 0, longest = 0;

    for (int right = 0; right < s.size(); right++) {
        while (SET.count(s[right])) {
            SET.erase(s[left]);
            left++;
        }

        SET.insert(s[right]);
        longest = max(longest, right - left + 1);
    }

    return longest;
}

Order(n);


Permutation in String
---

class Solution {
public:
    bool checkInclusion(string s1, string s2) {

        
        int n = s2.length();
        if(s1.length() > s2.length()) return false;
        unordered_map<char,int> s1Map;
        unordered_map<char,int> s2Map;

        for(int i=0;i<s1.length();i++){
            s1Map[s1[i]]++;
            s2Map[s2[i]]++;
        }

        if(s1Map == s2Map) return true;

        int left=0;

        for(int right=s1.length();right<n;right++){
            s2Map[s2[right]]++;
            s2Map[s2[left]]--;

            if(s2Map[s2[left]] == 0){
                s2Map.erase(s2[left]);
            }
            left++;

            if(s1Map == s2Map){
                return true;
            }
        }
        return false;
    }
};

Minimum Size Subarray Sum
---

Why:
Amazon OA frequently asks window + hashmap.