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
LeetCode Validate Binary Search Tree
LeetCode Lowest Common Ancestor of BST