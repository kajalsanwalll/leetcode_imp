5. Stack
--

Important for OA.

LeetCode Valid Parentheses ✅
---

class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        unordered_map<char,char> mp = {
            {')','('},
            {']','['},
            {'}','{'}
        };

        for(char c : s){
            if(mp.find(c) == mp.end()){
                st.push(c);
            }
            else{
                if(st.empty() || st.top()!= mp[c]){
                    return false;
                }
                st.pop();
            }
        }
        return st.empty();
    }
};

LeetCode Longest Valid Parentheses ✅

class Solution {
public:
    int longestValidParentheses(string s) {
        stack<int> st;
        st.push(-1);

        int maxlen=0;
        
        for(int i=0;i<s.size();i++){
            if(s[i] == '('){
                st.push(i);
            }else{
                st.pop();

                if(st.empty()){
                    st.push(i);
                }else{
                    maxlen = max(maxlen, i - st.top());
                }
            }
        }
        return maxlen;
    }
};


Order(n);

LeetCode Daily Temperatures ✅
---

class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) {

        int n = temperatures.size();
        vector<int> answer(n,0);
        stack<int> st;
        
        for(int i=0 ; i <n;i++){
            while(!st.empty() && temperatures[st.top()] < temperatures[i]){
                answer[st.top()] = i - st.top();
                st.pop();
            }
            st.push(i);
        }
        return answer;
    }
};

Order(n);


LeetCode Evaluate Reverse Polish Notation ✅
---

class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> st;

        for(string token : tokens){
            if(token == "+" || token == "-" || token == "*" || token == "/"){
                int a = st.top(); st.pop();
                int b = st.top(); st.pop();

                if(token == "+") st.push(b + a);
                else if(token == "-") st.push(b - a);
                else if(token == "*") st.push(b * a);
                else st.push(b / a);
            }
            else{
               st.push(stoi(token));
            }
            
        }
        return st.top();
    }
};

Order(n);


Min Stack
---


class MinStack {
public:

    stack<int> st;
    stack<int> minSt;

    MinStack() {
        
    }
    
    void push(int val) {

        st.push(val);

        if(minSt.empty() || val <= minSt.top()){
            minSt.push(val);
        }
    }
    
    void pop() {

        if(st.top() == minSt.top()){
            minSt.pop();
        }

        st.pop();
    }
    
    int top() {
        return st.top();
    }
    
    int getMin() {
        return minSt.top();
    }
};

O(1);


Largest Rectangle in Histogram
---

basically push in stack jab tak height is taller, pop when height is shorter

class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        stack<int> st;
        int n = heights.size();
        int maxArea=0;

        for(int i=0; i<=n; i++){
            while(!st.empty() && (i==n || heights[i] < heights[st.top()])){
                int height = heights[st.top()];
                st.pop();

                int right = i;
                int left;
                if(st.empty()) left = -1;
                else left = st.top();

                int width = right - left - 1;
                maxArea = max(maxArea, height*width);
            }
            st.push(i);
        }
        return maxArea;
    }
};

O(n);