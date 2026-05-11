1. Arrays / Hashing
---

LeetCode Two Sum  ✅
--
FIRST APPROACH

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {

       int n = nums.size();

       for(int i=0; i<n-1;i++){

        for(int j=i+1;j<n;j++){

            if(nums[i]+nums[j] == target){
                return {i,j};
            }
        }
       }  
       return {};     
    }
};
Order of n^2


SECOND APPROACH

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {

       int n = nums.size();

       unordered_map<int,int> map;

        for(int i=0;i<n;i++){
            int diff = target - nums[i];
            if(map.count(diff)){
                return {map[diff],i};
            }
            map[nums[i]] = i;
        }
        return {};

    }
};

Order of n using hash map


LeetCode Contains Duplicate ✅
--

class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        
        int n = nums.size();
        unordered_map<int, int> map;

        for(int i=0;i<n;i++){
            
            if(map.count(nums[i])){
                return true;
            }
            map[nums[i]] = i;
        }
        return false;
    }
};

Order of n


LeetCode Product of Array Except Self ✅
---

FIRST APPROACH

class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {


        int n = nums.size();
        vector<int> arr(n,1);

        int left = 1;
        for(int i=0;i<n;i++){
            arr[i] *= left;
            left *= nums[i];
        }

        int right = 1;
        for(int i=n-1;i>=0;i--){
            arr[i] *= right;
            right *= nums[i];
        }
        return arr;

    }
};

Order of n time and order of 1 space

LeetCode Top K Frequent Elements ✅
---
 
FIRST APPROACH (heap,priority queue)

class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        
        int n = nums.size();

        if(n==1){
            return nums;
        }

        unordered_map<int,int> freq;

        for(int i=0;i<n;i++){

            freq[nums[i]]++;
        }
        
        priority_queue<pair<int,int>> pq;

        for(auto x : freq){
            pq.push({x.second,x.first});
        }

        vector<int> ans;

        while(k--){
            ans.push_back(pq.top().second);
            pq.pop();
        }

        return ans;
    }
};

order (n log n);


SECOND APPROACH (bucket sort) order n

class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        
        int n = nums.size();

        if(n==1){
            return nums;
        }

        unordered_map<int,int> freq;

        for(int i=0;i<n;i++){

            freq[nums[i]]++;
        }
        
        vector<vector<int>> bucket(n+1);

        for(auto x : freq){
            bucket[x.second].push_back(x.first);
        }

        vector<int> ans;

        for(int i = n; i>=0 && ans.size()<k;i--){

            for(int num : bucket[i]){
                ans.push_back(num);
                if(ans.size() == k){
                    return ans;
                }
            }
        }

        return ans;
    }
};

order (n);

LeetCode Longest Consecutive Sequence ✅
---

class Solution {
public:
    int longestConsecutive(vector<int>& nums) {

        
       unordered_set<int> s(nums.begin(), nums.end());

       int longest = 0;

       for(int num : s){
         if(s.find(num-1) == s.end()){
            int length = 1;

            while(s.find(num+1) != s.end()){
                num++;
                length++;
            }
            longest = max(longest,length);
         }
       }
       return longest;
    }
};

order(n) using unordered set

Group Anagrams ✅
---

class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        unordered_map<string,vector<string>> ans;

        for(string& s : strs){
            string key = s;
            sort(key.begin(),key.end());
            ans[key].push_back(s);
        }

        vector<vector<string>> result;
        for(auto& c : ans){
            result.push_back(c.second);
        }
        return result;
    }
};

Order (n klog k);


Valid Anagram ✅
---


class Solution {
public:
    bool isAnagram(string s, string t) {
        unordered_map<char,int> counter;

        if(s.length() != t.length()){
            return false;
        }

        for(char c : s){
            counter[c]++;
        }

        for(char c : t){
            if(counter.find(c) == counter.end() || counter[c]==0){
                return false;
            }
            counter[c]--;
        }
        return true;
    }
};

Order(n);


Encode and decode string ✅
---

class Codec {
public:

    // Encodes a list of strings to a single string.
    string encode(vector<string>& strs) {
        string res = "";

        for (string s : strs) {
            res += to_string(s.size()) + "#" + s;
        }
        
        return res;
    }

    // Decodes a single string to a list of strings.
    vector<string> decode(string s) {
        vector<string> res;
        int i = 0;

        while (i < s.size()) {
            int j = i;

            // find '#'
            while (s[j] != '#') {
                j++;
            }

            // length of string
            int len = stoi(s.substr(i, j - i));

            // move to start of actual string
            j++;

            // extract string
            string word = s.substr(j, len);
            res.push_back(word);

            // move i to next segment
            i = j + len;
        }

        return res;
    }
};

Missing and Repeated value
---

class Solution {
public:
    vector<int> findMissingAndRepeatedValues(vector<vector<int>>& grid) {
        int n = grid.size();
        unordered_map<int,int> freq;

        int repeated = -1, missing = -1;

        // Count frequency
        for(auto &row : grid){
            for(int num : row){
                freq[num]++;
            }
        }
        // Check from 1 to n^2
        for(int i = 1; i <= n*n; i++){
            if(freq[i] == 2){
                repeated = i;
            }
            if(freq[i] == 0){
                missing = i;
            }
        }

        return {repeated, missing};
    }
};

