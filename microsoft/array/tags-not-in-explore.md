**Hard:**

Dungeon Game

Basic Calculator

Binary Tree Maximum Path Sum

Design Search Autocomplete System

Design Excel Sum Formula

Merge K Sorted Lists

Reverse Nodes in k-Group

**Medium:**

Battleships in a Board

Permutations I & II

Find Bottom Left Tree Value

Minimum Number of Arrows to Burst Ballons: Meeting Rooms II

Water and Jug Problem

Product of Array Except Self: 从左到右 从右到左

House Robber I & II

2 Keys Keyboard & 4 Keys Keyboard : DP

Find Peak Element

Binary Search Tree Iterator

```cpp
class BSTIterator {
public:
    BSTIterator(TreeNode *root) {
        pushAll(root);
    }

    /** @return whether we have a next smallest number */
    bool hasNext() {
        return !s.empty();
    }

    /** @return the next smallest number */
    int next() {
        TreeNode* temp = s.top();
        s.pop();
        if (temp->right) {
            pushAll(temp->right);
        }
        return temp->val;
    }
    
    void pushAll(TreeNode *root) {
        while(root) {
            s.push(root);
            root = root->left;
        }
    }
    
private:
    stack<TreeNode*> s;
};
```

Flatten Binary Tree to Linked Lis

```cpp
void flatten(TreeNode* root) {
    if (!root || !root->left && !root->right) return;
    TreeNode* curr = root;
    while(curr) {
        TreeNode* ri = curr->right;
        if (curr->left) {
            TreeNode* le = curr->left;
            while(le->right) {
                le = le->right;
            }
            le->right = ri;
            curr->right = curr->left;
            curr->left = NULL;
        }
        curr = curr->right;
    }
}
```

Merge Intervals

Simplify Path

```cpp
string simplifyPath(string path) {
    string res, tmp;
    vector<string> stk;
    stringstream ss(path);
    while (getline(ss,tmp,'/')) {
        if (tmp == "" || tmp == ".") continue;
        else if (tmp == "..") {
            if (!stk.empty()) stk.pop_back();
        }
        else if (tmp != "..") stk.push_back(tmp);
    }
    for (auto elem : stk) {
        res += '/' + elem;
    }
    return res.empty() ? "/" : res;
}
```

Decode Ways

[Bulb Switcher](https://leetcode.com/problems/bulb-switcher/discuss/77112/Share-my-o%281%29-solution-with-explanation) & Bulb Switcher II

Jump Game & Jump Game II







