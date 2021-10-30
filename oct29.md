[814. Binary Tree Pruning - Medium](https://leetcode.com/problems/binary-tree-pruning/)

    Let n be the number of nodes, then O(n) is the time complexity and space complexity because we have to check every node 


```cpp
class Solution {
    bool helper(TreeNode* node){
        bool flag = false; 
        if(node->left){
            flag = helper(node->left);
                if(not flag){
                    delete node->left; 
                    node->left = nullptr; 
            }
        }

        bool flagtwo = false; 
        if(node->right){
            flagtwo = helper(node->right);
            if(not flagtwo){
                delete node->right; 
                node->right = nullptr; 
            }
        }

        if(node->val == 0 and not flag and not flagtwo)
            return false; 
        return true; 
    }
public:
    TreeNode* pruneTree(TreeNode* root) {
       if(not helper(root)){
            delete root; 
            root = nullptr; 
        }   

        return root; 
        
    }
};
```

---
[266. Palindrome Permutation - Easy](https://leetcode.com/problems/palindrome-permutation/)

This approach is O(n) space and O(n) time 

    This is not the one pass approach
    

if len is even 
* then no character must occur an odd number of times 

if len >= 3 and odd
* There should be two of every letter except for one of them
    
    * this exception will be the middle character 

```cpp
class Solution {
std::unordered_map<char, int> counts; 
public:
    bool canPermutePalindrome(string s) {
        for(int i = 0; i < s.size(); ++i){
            counts[s[i]] += 1; 
        }

        int numOdds = 0; 
        bool isEven = (s.size() % 2 == 0);
        for(auto iter = counts.begin(); iter != counts.end(); ++iter){
            if((iter->second) % 2 != 0)
                ++numOdds; 
            if(isEven and numOdds > 0)
                return false; 
            if(not isEven and numOdds > 1)
                return false; 
        }

        return true; 
    }
};
```