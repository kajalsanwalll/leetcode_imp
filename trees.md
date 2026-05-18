9. Trees
--

Very likely interview topic.

Inorder Traversal Skeleton
---

while (root != NULL || !stack.empty()) {
    while (root != NULL) {
        stack.push(root);
        root = root->left;
    }

    root = stack.top();
    stack.pop();

    //  DO SOMETHING HERE

    root = root->right;
}

LeetCode Maximum Depth of Binary Tree
---

class Solution {
public:
    int maxDepth(TreeNode* root) {


        if(root == 0){
            return 0;
        }

        return 1 + max(maxDepth(root->left), maxDepth(root->right));
    }
};


LeetCode Binary Tree Level Order Traversal
---

class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> ans;
        queue<TreeNode*> q;

        if(!root) return {};
        q.push(root);

        while(!q.empty()){
            int size = q.size();
            vector<int> level;

            while(size--){
                TreeNode* node = q.front();
                q.pop();
                level.push_back(node->val);

                if(node->left) q.push(node->left);
                if(node->right) q.push(node->right);

            }
            ans.push_back(level);
        }
        return ans;
    }
};

Order(n);


LeetCode Validate Binary Search Tree
----

class Solution {
public:
    bool isValidBST(TreeNode* root) {
        stack<TreeNode*> st;
        TreeNode* prev = NULL;

        while (root != NULL || !st.empty()) {
            while (root != NULL) {
                st.push(root);
                root = root->left;
            }

            root = st.top();
            st.pop();

            if (prev != NULL && root->val <= prev->val)
                return false;

            prev = root;

            root = root->right;
        }

        return true;
    }
};


LeetCode Lowest Common Ancestor of BST
---

class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        while(root != NULL){
            if(p->val < root->val && q->val < root->val){
                root = root->left;
            }
            else if(p->val > root->val && q->val > root->val){
                root = root->right;
            }
            else{
                return root;
            }
        }
        return NULL;
    }
};


Binary tree Right side view
---

class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        vector<int> ans;
        if(root == NULL) return ans;

        queue<TreeNode*> q;
        q.push(root);

        while(!q.empty()){
            int size = q.size();

            for(int i=0; i< size;i++){
                TreeNode* node = q.front();
                q.pop();

                if(i==size -1){
                    ans.push_back(node->val);
                }

                if(node->left) q.push(node->left);
                if(node->right) q.push(node->right);

            }
        }
        return ans;
    }
};

Order(n); time and space


Count good nodes in binary tree
---


class Solution {
public:

    int dfs(TreeNode* root, int maxSoFar){
        if(root == NULL) return 0; 
        int good = 0;

        if(root->val >= maxSoFar){
            good = 1;
        }

        maxSoFar = max(maxSoFar, root->val);

        return good 
          +dfs(root->left,maxSoFar)
          +dfs(root->right,maxSoFar);
        
    }
    int goodNodes(TreeNode* root) {
        return dfs(root, root->val);
    }
};

time O(n);
space O(height);


Kth smallest element in BST
---

class Solution {
public:
    int ans = 0;
    int count = 0;

    void inorder(TreeNode* root, int k){
        if(root == NULL) return;

        inorder(root->left,k);
        count++;

        if(count == k){
            ans = root->val;
            return;
        }

        inorder(root->right,k);
    }

    int kthSmallest(TreeNode* root, int k) {
        inorder(root, k);

        return ans;
    }
};

time : O(n);
space O(height);


