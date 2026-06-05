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