6. Binary Search
--

Amazon asks these a lot.

LeetCode Binary Search
---

class Solution {
public:
    int search(vector<int>& nums, int target) {
        int l = 0;
        int h = nums.size() - 1;

      while(l<=h){
         int mid = l + (h - l) / 2;  // yad rakhna 

        if(nums[mid] == target){
            return mid;
        }
        else if(nums[mid]< target){
            l = mid+1;
        }
        else{
            h = mid -1;
        }
      }
      return -1;
    }
};

Order(n log n);

LeetCode Search in Rotated Sorted Array
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

LeetCode Koko Eating Bananas
---
