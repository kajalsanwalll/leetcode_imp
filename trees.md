9. Trees
--

Very likely interview topic.

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




LeetCode Lowest Common Ancestor of BST
---

