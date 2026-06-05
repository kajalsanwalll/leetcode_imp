Basic Template
---

class Solution {
public:
    int solve(string s1, string s2) {

        int n = s1.size();
        int m = s2.size();

        vector<vector<int>> dp(n + 1, vector<int>(m + 1, 0));

        // Base cases
        for(int i = 0; i <= n; i++) {
            dp[i][0] = ?;
        }

        for(int j = 0; j <= m; j++) {
            dp[0][j] = ?;
        }

        // Fill table
        for(int i = 1; i <= n; i++) {
            for(int j = 1; j <= m; j++) {

                if(s1[i-1] == s2[j-1]) {

                    // MATCH CASE
                    dp[i][j] = ?;

                } else {

                    // NO MATCH CASE
                    dp[i][j] = ?;
                }
            }
        }

        return dp[n][m];
    }
};


Minimum/Maximum Problems
---


Edit Distance. 
---

class Solution {
public:
    int minDistance(string word1, string word2) {
        int m = word1.size();
        int n = word2.size();

        vector<vector<int>> dp(m+1, vector<int>(n+1,0));

        for(int i=0; i<=m;i++){
            dp[i][0] = i;
        }
        for(int j=0;j<=n;j++){
            dp[0][j] = j;
        }

        for(int i=1; i<=m;i++){
            for(int j=1;j<=n;j++){

                if(word1[i-1] == word2[j-1]){
                    dp[i][j] = dp[i-1][j-1];
                }
                else{
                    dp[i][j] = 1 + min({
                        dp[i-1][j],
                        dp[i][j-1],
                        dp[i-1][j-1]
                    });
                }
            }
        }
        return dp[m][n];
    }
};


Longest Common Subsequence
---

class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int n = text1.size();
        int m = text2.size();

        vector<vector<int>> dp(n+1,vector<int>(m+1,0));

        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){

                if(text1[i-1] == text2[j-1]){
                    dp[i][j] = 1 + dp[i-1][j-1];
                }
                else{
                    dp[i][j] = max(dp[i-1][j],
                    dp[i][j-1]);
                }
            }
        }
        return dp[n][m];
    }
};

Delete Operation for 2 Strings
---

class Solution {
public:
    int minDistance(string word1, string word2) {
        int n = word1.size();
        int m = word2.size();

        vector<vector<int>> dp(n+1,vector<int>(m+1,0));

        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){
                if(word1[i-1] == word2[j-1]){
                    dp[i][j] = 1 + dp[i-1][j-1];
                }
                else{
                    dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
                }
            }
        }
        int a = dp[n][m];
        return n+m - 2*a;
    }
};

Min ASCII delete sum for 2 strings
---

class Solution {
public:
    int minimumDeleteSum(string s1, string s2) {
        int n = s1.size();
        int m = s2.size();

        vector<vector<int>> dp(n+1,vector<int>(m+1,0));

        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){
                if(s1[i-1] == s2[j-1]){
                    dp[i][j] = s1[i-1] + dp[i-1][j-1];  // s1[i-1] gives ASCII value because of implicit type conversion
                }else{
                    dp[i][j] = max(dp[i-1][j],dp[i][j-1]);
                }
            }
        }
        int a = dp[n][m] ;
        int sm1 = 0, sm2 = 0;
        for(char c : s1){
            sm1 += c;
        }
        for(char c : s2){
            sm2 += c;
        }

        return (sm1 + sm2 - 2*a);
    }
};

Longest Palindromic Subsequence
---

class Solution {
public:
    int longestPalindromeSubseq(string s) {
        int n = s.size();
        string rev = s ;
        reverse(rev.begin(),rev.end());

        vector<vector<int>> dp(n+1,vector<int>(n+1,0));

        for(int i=1;i<=n;i++){
            for(int j=1;j<=n;j++){
                if(s[i-1] == rev[j-1]){
                    dp[i][j] = 1 + dp[i-1][j-1];
                }else{
                    dp[i][j] = max(dp[i-1][j],dp[i][j-1]);
                }
            }
        }

        return dp[n][n];
    }
};

Min Insertion steps to make a string palindrome
---

class Solution {
public:
    int minInsertions(string s) {
        int n = s.size();
        string rev = s;
        reverse(rev.begin(),rev.end());

        vector<vector<int>> dp(n+1,vector<int>(n+1,0));

        for(int i=1;i<=n;i++){
            for(int j=1;j<=n;j++){
                if(s[i-1] == rev[j-1]){
                    dp[i][j] = 1 + dp[i-1][j-1];
                }else{
                    dp[i][j] = max(dp[i-1][j],dp[i][j-1]);
                }
            }
        }
        return n - dp[n][n];
    }
};


Shortest common supersequence
---

class Solution {
public:
    string shortestCommonSupersequence(string str1, string str2) {
        int n = str1.size();
        int m = str2.size();

        vector<vector<int>> dp(n+1,vector<int>(m+1,0));

        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){
                if(str1[i-1] == str2[j-1]){
                    dp[i][j] = 1 + dp[i-1][j-1];
                }else{
                    dp[i][j] = max(dp[i][j-1],dp[i-1][j]);
                }
            }
        }
        int i = n;
        int j = m;
        string ans = "";

        while(i>0 && j>0){

            if(str1[i-1] == str2[j-1]){
                ans += str1[i-1];
                i--;
                j--;
            }
            else if(dp[i-1][j] > dp[i][j-1]){
                ans += str1[i-1];
                i--;
            }else{
                ans += str2[j-1];
                j--;
            }
        }
        while(i>0){
            ans += str1[i-1];
            i--;
        }
        while(j>0){
            ans += str2[j-1];
            j--;
        }
        
        reverse(ans.begin(),ans.end());

        return ans;
    }
};


Counting number of ways Problems:
---

Distinct Subsequences
---

class Solution {
public:
    int numDistinct(string s, string t) {
        int n = s.size();
        int m = t.size();

        vector<vector<unsigned long long>> dp(n+1, vector<unsigned long long>(m+1,0));

        for(int i=0;i<=n;i++){
            dp[i][0] = 1;   // exactly 1 way to empty string
        }

        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){
                if(s[i-1] == t[j-1]){
                    dp[i][j] = dp[i-1][j-1] + dp[i-1][j];
                }else{
                    dp[i][j] = dp[i-1][j];
                }
            }
        }
        return dp[n][m];
    }
};

Distinct Subsequences II
---

class Solution {
public:
    int distinctSubseqII(string s) {
        int n = s.size();
        const int MOD = 1e9 + 7;

        vector<long long> dp(n+1,0);
        vector<int> last(26,-1);

        dp[0] = 1;

        for(int i=1;i<=n;i++){
            dp[i] = (2*dp[i-1])%MOD;

            int c = s[i-1] - 'a';

            if(last[c] != -1){
                dp[i] = (dp[i] - dp[last[c] - 1] + MOD)%MOD;
            }

            last[c] = i;
        }
        return (dp[n] - 1 + MOD)% MOD;
    }
};

Interleaving String
---

class Solution {
public:
    bool isInterleave(string s1, string s2, string s3) {
        int n = s1.size();
        int m = s2.size();

        if(n + m != s3.size()) return false;

        vector<vector<bool>> dp(n+1,vector<bool>(m+1,false));

        dp[0][0] = true;

        for(int i=0;i<=n;i++){
            for(int j=0;j<=m;j++){
                if(i>0 && s1[i-1] == s3[i+j-1] && dp[i-1][j]){
                    dp[i][j] = true;
                }
                if(j>0 && s2[j-1] == s3[i+j-1] && dp[i][j-1]){
                    dp[i][j] = true;
                }
            }
        }
        return dp[n][m];
    }
};