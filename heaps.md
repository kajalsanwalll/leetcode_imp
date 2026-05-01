7. Heap / Priority Queue
--

Super high priority.

LeetCode Kth Largest Element in an Array
---

class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        if(nums.size() == 1){
            return nums[0];
        }
        int ans = 0;
        priority_queue<int> pq;
        
        for(int i=0; i<nums.size()-1;i++){
            while(i< nums.size()){
                pq.push(nums[i]);
                i++;
            }

            while(k--){
                
                ans = pq.top();
                pq.pop();
                if(k == 0){
                    return ans;
                }
            }
        }
        return ans;
    }
};

Order(n);

LeetCode K Closest Points to Origin
---


LeetCode Task Scheduler
LeetCode Find Median from Data Stream

Amazon really likes heaps.