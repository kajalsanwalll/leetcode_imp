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
