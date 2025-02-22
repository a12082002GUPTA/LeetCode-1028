# LeetCode-1028

# C++

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
    TreeNode* recoverFromPreorder(string traversal) {
        map<int,TreeNode*>mp;
        int i=0,n=traversal.length();
        TreeNode *head=NULL;
        while(i<n)
        {
            int c=0;
            while(traversal[i]=='-')
            {
                c++;
                i++;
            }
            int a=0;
            while(i<n&&traversal[i]!='-')
            {
                a*=10;
                a+=(traversal[i]-48);
                i++;
            }
            TreeNode *q=new TreeNode(a);
            if(c==0)
            {
                head=q;
                mp[c]=q;
            }
            else
            {
                TreeNode *dup=mp[c-1];
                 if(!dup->left)
                 {
                    dup->left=q;
                 }
                 else
                 {
                    dup->right=q;
                 }
                 mp[c]=q;
            }
        }
        return head;
    }

};

# Java

class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    
    TreeNode(int val) {
        this.val = val;
        this.left = null;
        this.right = null;
    }
}

class Solution {
    public TreeNode recoverFromPreorder(String traversal) {
        Map<Integer, TreeNode> nodeMap = new HashMap<>();
        int i = 0, n = traversal.length();
        TreeNode head = null;
        
        while (i < n) {
            int depth = 0;
            while (i < n && traversal.charAt(i) == '-') {
                depth++;
                i++;
            }
            
            int value = 0;
            while (i < n && Character.isDigit(traversal.charAt(i))) {
                value = value * 10 + (traversal.charAt(i) - '0');
                i++;
            }
            
            TreeNode node = new TreeNode(value);
            
            if (depth == 0) {
                head = node;
            } else {
                TreeNode parent = nodeMap.get(depth - 1);
                if (parent.left == null) {
                    parent.left = node;
                } else {
                    parent.right = node;
                }
            }
            
            nodeMap.put(depth, node);
        }
        
        return head;
    }
}
