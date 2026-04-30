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


LeetCode Product of Array Except Self
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

LeetCode Top K Frequent Elements
LeetCode Longest Consecutive Sequence