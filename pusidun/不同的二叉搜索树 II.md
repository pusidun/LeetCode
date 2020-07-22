## 思路

递归

/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<TreeNode*> generateTrees(int start, int end) {
        if(start>end) return vector<TreeNode*>{nullptr};
        
        vector<TreeNode*> ans;
        for(int i=start; i<=end; ++i) {
           vector<TreeNode*> lefts = generateTrees(start, i-1); 
           vector<TreeNode*> rights = generateTrees(i+1, end);
           for(auto left:lefts)
            for(auto right:rights) {
                TreeNode* root = new TreeNode(i);
                root->left = left;
                root->right = right;
                ans.push_back(root);
            }
        }
        return ans;
    }
    
    vector<TreeNode*> generateTrees(int n) {
        if(!n) return vector<TreeNode*>{};
        return generateTrees(1, n);
    }
};