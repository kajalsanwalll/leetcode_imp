3. Two Pointers 
--

Simple but frequent.

LeetCode Valid Palindrome ✅
--

class Solution {
public:
    bool isPalindrome(string s) {
        int i=0;
        int j = s.size()- 1;

        while(i<j){
            while(i<j && !isalnum(s[i])){
                i++;
            }
            while(i<j && !isalnum(s[j])){
                j--;
            }

            if(tolower(s[i]) != tolower(s[j])){
                return false;
            }
            i++;j--;
        }
        return true;

    }
};

LeetCode 3Sum ✅
---

class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {

        vector<vector<int>> ans;
        sort(nums.begin(),nums.end());
        int n = nums.size();
        
        for(int i=0;i<n;i++){
            if(i>0 && nums[i] == nums[i-1]){
                continue;
            }

            int j = i+1;
            int k = n - 1;

            while(j<k){
                int total = nums[i] + nums[j]+nums[k];

                if(total>0){
                    k--;
                }
                else if(total < 0){
                    j++;
                }
                else{
                    ans.push_back({nums[i], nums[j], nums[k]});
                    j++;

                    while(j<k && nums[j] == nums[j-1]){
                        j++;
                    }
                }
            }
        }
        return ans;
    }
};

O(n^2);

LeetCode Container With Most Water ✅
--

class Solution {
public:
    int maxArea(vector<int>& height) {
       int n = height.size();
       int area=0;
       int i=0;int j= n-1;

       while(i<j){
         area = max(area, min(height[i], height[j])*(j-i));
         if(height[i]<height[j])i++;
         else j--;
        }
        return area;
    }
};

Order(n);


Trapping Rain Water
---

class Solution {
public:
    int trap(vector<int>& height) {
        
        int left = 0;
        int right = height.size() - 1;

        int leftMax = 0;
        int rightMax = 0;

        int water = 0;

        while(left < right) {

            if(height[left] < height[right]) {

                if(height[left] >= leftMax) {
                    leftMax = height[left];
                }
                else {
                    water += leftMax - height[left];
                }

                left++;
            }
            else {

                if(height[right] >= rightMax) {
                    rightMax = height[right];
                }
                else {
                    water += rightMax - height[right];
                }

                right--;
            }
        }

        return water;
    }
};


Remove Duplicates from a Sorted Array
---

class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.empty()) return 0;

        int i = 1;

        for (int j = 1; j < nums.size(); j++) {
            if (nums[j] != nums[i - 1]) {
                nums[i] = nums[j];
                i++;
            }
        }

        return i;        
    }
};

Reverse words in a string
---

class Solution {
public:
    string reverseWords(string s) {
        reverse(s.begin(), s.end());
        int n = s.size();
        int left=0;
        int right=0;
        int i=0;
        while(i<n){
            while(i<n && s[i] == ' '){
                i++;
            }

            if(i==n) break;

            while(i<n && s[i] != ' '){
                s[right++] = s[i++];
            }
            reverse(s.begin() + left, s.begin() + right);
            s[right++] = ' ';
            left = right;
            i++;
        }
        s.resize(right-1);
        return s;
    }
};