12. Backtracking
--

At least these.

LeetCode Subsets
---

class Solution {
public:
    vector<vector<int>> ans;
    void sol(int index,vector<int>&nums, vector<int>& temp){
        
        if(index>= nums.size()){
            ans.push_back(temp);
            return;
        }
        temp.push_back(nums[index]);
        sol(index+1,nums,temp);
        temp.pop_back();
        sol(index+1,nums,temp);
    }

    vector<vector<int>> subsets(vector<int>& nums) {
        vector<int> temp;
        sol(0,nums,temp);
        return ans;


    }
};

TIME O(2^n *n);
space O(n);

LeetCode Combination Sum
---

class Solution {
public:

vector<vector<int>> ans;
    void solve(int index, vector<int>& candidates,int target,vector<int>& temp){
            if(target == 0){
                ans.push_back(temp);
                return;
            }
            if(target < 0 || index>= candidates.size()) return;

            temp.push_back(candidates[index]);
            solve(index,candidates,target-candidates[index],temp);
            temp.pop_back();
            solve(index+1,candidates,target,temp);

        }

    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<int> temp;
        solve(0,candidates,target,temp);
        return ans;
    }
};

Order(2^target); time
Order(target); space



Word Search
---

class Solution {
public:
    bool dfs(vector<vector<char>>& board, string& word, int r, int c, int index){
        if(index == word.size()){
            return true;
        }

        if(r<0 || c<0 || r>= board.size() || c>= board[0].size() || board[r][c] != word[index]){
            return false;
        }

        char temp = board[r][c];
        board[r][c] = '#';

        bool found = dfs(board,word,r+1,c,index+1) || 
            dfs(board,word,r-1,c,index+1) ||
            dfs(board,word,r,c+1,index+1) ||
            dfs(board,word,r,c-1,index+1);

        board[r][c] = temp;
        return found;
    }

    bool exist(vector<vector<char>>& board, string word) {
        int rows = board.size();
        int cols = board[0].size();

        for(int r=0;r<rows;r++){
            for(int c=0; c<cols;c++){
                if(dfs(board,word,r,c,0)){
                    return true;
                }
            }
        }
        return false;
    }
};


Worst case:
O(m×n×4 
k
 )
Space:
O(k)
(recursion stack)

FOLLOW UP APPROACH USING PRUNING

class Solution {
public:
    bool dfs(vector<vector<char>>& board, string& word, int r, int c, int index){
        if(index == word.size()){
            return true;
        }

        if(r<0 || c<0 || r>= board.size() || c>= board[0].size() || board[r][c] != word[index]){
            return false;
        }

        char temp = board[r][c];
        board[r][c] = '#';

        bool found = dfs(board,word,r+1,c,index+1) || 
            dfs(board,word,r-1,c,index+1) ||
            dfs(board,word,r,c+1,index+1) ||
            dfs(board,word,r,c-1,index+1);

        board[r][c] = temp;
        return found;
    }

    bool exist(vector<vector<char>>& board, string word) {
        unordered_map<char,int> boardCount;
        unordered_map<char,int> wordCount;

        for(auto& row : board) {
            for(char ch : row) {
                boardCount[ch]++;
            }
        }

        for(char ch : word) {
            wordCount[ch]++;
        }

        // pruning
        for(auto& it : wordCount) {
            if(boardCount[it.first] < it.second) {
                return false;
            }
        }

        // start from rarer side
        if(boardCount[word[0]] > boardCount[word.back()]) {
            reverse(word.begin(), word.end());
        }

        int rows = board.size();
        int cols = board[0].size();

        for(int r=0;r<rows;r++){
            for(int c=0; c<cols;c++){
                if(dfs(board,word,r,c,0)){
                    return true;
                }
            }
        }
        return false;
    }
};


Letter Combinations of a Phone Number
---

class Solution {
public:

    void backtrack(int index, string& digits, vector<string>& mapping,string& current, vector<string>& result){
        if(index == digits.size()){
            result.push_back(current);
            return;
        }
        string letters = mapping[digits[index] - '0'];

        for(auto c : letters){
            current.push_back(c);
            backtrack(index+1,digits,mapping,current,result);
            current.pop_back();
        }
    }
    vector<string> letterCombinations(string digits) {
        if(digits.empty()) return {};

        vector<string> mapping = {
            "", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"
        };

        vector<string> result;
        string current;
        backtrack(0,digits,mapping,current,result);

        return result;
    }
};

O(4^n) time