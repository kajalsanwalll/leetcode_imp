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
    int search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size()-1;

        while(left <=right){
            int mid = left + (right-left)/2;

            if(nums[mid] == target) return mid;

            if(nums[left] <= nums[mid]){
                if(nums[left]<= target && target <nums[mid]){
                    right = mid-1;
                }else{
                    left = mid +1 ;
                }
            }
            else{
                if(nums[right] >= target && target > nums[mid]){
                    left = mid+1;
                }else{
                    right = mid -1 ;
                }
            }
        }
        return -1;
    }
};

O(log n);


LeetCode Koko Eating Bananas
---

class Solution {
public:
    int minEatingSpeed(vector<int>& piles, int h) {
        int low=1;
        int high = *max_element(piles.begin(),piles.end());

        while(low<high){
            int mid = low + (high - low)/2;
            long long hours =0;

            for(int p : piles){
                hours += (p+ mid - 1)/mid;
            }

            if(hours <= h){
                high = mid;
            }else{
                low=mid+1;
            }
        }
        return low;
    }
};

Order(n logM);



Find Minimum in Rotated Sorted Array
---


class Solution {
public:
    int findMin(vector<int>& nums) {
        int left =0;
        int right = nums.size() - 1;

        while(left<right){
            int mid = left + (right - left)/2;
            
            if(nums[mid] > nums[right]){
                left = mid +1;
            }else{
                right = mid;
            }
        }
        return nums[left];
    }
};

O(log n); time


Time Based Key-Value Store
---


class TimeMap {
public:
    unordered_map<string, vector<pair<int,string>>> mp;
    TimeMap() {
        
    }
    
    void set(string key, string value, int timestamp) {
        mp[key].push_back({timestamp,value});
    }
    
    string get(string key, int timestamp) {
        if(mp.find(key) == mp.end()) return "";

        vector<pair<int,string>>& arr = mp[key];

        int left=0;
        int right = arr.size()-1;
        string ans ="";

        while(left<=right){
            int mid = left + (right-left)/2;

            if(arr[mid].first <= timestamp){
                ans = arr[mid].second;
                left = mid+1;
            }else{
                right = mid-1;
            }
        }
        return ans;
    }
};


Order(log n); time
Order(1); space


Median of two sorted arrays
---
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int m = nums1.size(); int n = nums2.size();
        if(m>n){
            return findMedianSortedArrays(nums2,nums1);
        }
        int k = m+n;
        int left = (m+n+1)/2; 
        int low = 0, high = m;

        while(low<=high){
            int mid1 = (low+high) >> 1;
            int mid2 = left - mid1;

            int l1= INT_MIN, l2= INT_MIN, r1= INT_MAX, r2= INT_MAX;

            if(mid1 < m) r1 = nums1[mid1];
            if(mid2 < n) r2 = nums2[mid2];
            if(mid1 -1 >= 0) l1 = nums1[mid1 - 1];
            if(mid2 - 1 >= 0) l2 = nums2[mid2 - 1];

            if(l1 <= r2 && l2 <= r1){
                if(k%2 == 1) {
                    return max(l1,l2);
                }
                else{
                    return ((double)(max(l1,l2) + min(r1,r2)))/2.0;
                }
            }
            else if(l1 > r2){
                high = mid1 - 1;
            }
            else{
                low = mid1+1;
            }
        }
        return 0;
    }
};

O(log m+n);time
O(1); space


Search Insert Position
---

class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int l=0; int h = nums.size()-1;

        while(l<=h){
            int mid = l+ (h-l)/2;

            if(nums[mid] == target){
                return mid;
            }
            else if(nums[mid] < target){
                l = mid+1;
            }
            else{
                h = mid-1;
            }
        }
        return l;
    }
};

O(log n);


First Bad Version
---

// The API isBadVersion is defined for you.
// bool isBadVersion(int version);

class Solution {
public:
    int firstBadVersion(int n) {
        int l = 1;
        int r = n;

        while(l<r){

            int mid = l + (r-l)/2;

            if(isBadVersion(mid)){
                r = mid;
            }
            else{
                l = mid + 1;
            }
        }
        return l;
    }
};