1. Validate Binary Search Tree \(Use left node as min bound, right node as max bound\)

2. Binary Tree Inorder Traversal \(Recursive or Stack Iterative\)

3. Binary Tree Level Order Traversal \(Queue BFS, push a NULL every level, which means push NULL when meet NULL\)

4. Binary Tree Zigzag Level Order Traversal \(Use a flag as boolean\)

5. Populating Next Right Pointer to Every Node \(Recursive 整理好下一层，然后调用dfs left, dfs right\)

6. Populating Next Right Pointer to Every Node II \(用两个while\(root\) loop, 当做一层一层的traversal, 用一个dummyNode当做leftMost, 每层从leftMost开始, 用一个currNode 来穿针引线, curr-&gt;next = root-&gt;next, curr = curr-&gt;next; \)

7. Lowest Common Ancestor of a Binary Search Tree \(从root向下遍历, 如果跟其中一个相等就返回root, 然后判断大中小三个可能\)

8. Lowest Common Ancestor of a Binary Tree \(Recrusion, 建一个leftNode 是 LCS\(root-&gt;left\)的返回值, 同时建一个rightNode, 根据这两个的返回值来输出结果, 注意recursion的base case是: root与p,q 相等则返回root\)

PS: 由于是Binary Tree, 所以这里不能用root-&gt;val来做任何判断, 直接判断root和p,q的地址即可

1. Construct Binary Tree from Preorder and Inorder Traversal

# 1. Validate Binary Search Tree

Given a binary tree, determine if it is a valid binary search tree \(BST\).

Solution:

```cpp
bool isValidBST(TreeNode* root) {
    return validBSTHelper(root, NULL, NULL);
}

bool validBSTHelper(TreeNode* root, TreeNode* minNode, TreeNode* maxNode) {
    if (!root) return true;
    if (minNode && minNode->val >= root->val || maxNode && maxNode->val <= root->val) {
        return false;
    }
    else return validBSTHelper(root->left, minNode, root) && validBSTHelper(root->right, root, maxNode);
}
```



# 2. Binary Tree In-order Traversal

Given a binary tree, return theinordertraversal of its nodes' values.

For example:  
Given binary tree`[1,null,2,3]`,

```
   1
    \
     2
    /
   3
```

return`[1,3,2]`.

**Solution:**

```cpp
vector<int> inorderTraversal(TreeNode* root) {
    vector<int> res;
    dfs(res, root);
    return res;
}
void dfs(vector<int> &res, TreeNode* root) {
    if (!root) return;
    dfs(res, root->left);
    res.push_back(root->val);
    dfs(res, root->right);
}
```



# 3. Binary Tree Level Order Traversal

**Solution:**

```cpp
vector<vector<int>> levelOrder(TreeNode* root) {
    queue<TreeNode*> q;
    vector<vector<int>> res;
    if (!root) return res;
    q.push(root);
    q.push(NULL);
    vector<int> line;
    while (!q.empty()) {
        TreeNode* curr = q.front();
        q.pop();
        if (!curr) {
            res.push_back(line);
            if (q.empty()) return res;
            line.clear();
            q.push(NULL);
        } else {
            if (curr->left) q.push(curr->left);
            if (curr->right) q.push(curr->right);
            line.push_back(curr->val);
        }
    }
    return res;
}
```



# 4. Binary Tree Zigzag Level Order Traversal

Given a binary tree, return the

zigzag level order

traversal of its nodes' values. \(ie, from left to right, then right to left for the next level and alternate between\).

```cpp
vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
    queue<TreeNode*> q;
    vector<vector<int>> res;
    bool flag = true;
    if (!root) return res;
    q.push(root);
    q.push(NULL);
    vector<int> line;
    while (!q.empty()) {
        TreeNode* curr = q.front();
        q.pop();
        if (!curr) {
            res.push_back(line);
            if (q.empty()) return res;
            line.clear();
            q.push(NULL);
            flag = !flag;
        } else {
            if (curr->left) q.push(curr->left);
            if (curr->right) q.push(curr->right);
            if (flag) line.push_back(curr->val);
            else line.insert(line.begin(), curr->val);
        }
    }
    return res;
}
```



# 5. Populating Next Right Pointers in Each Node

```cpp
void connect(TreeLinkNode *root) {
    if (!root || !root->left) return;
    root->left->next = root->right;
    if (root->next) {
        root->right->next = root->next->left;
    }
    connect(root->left);
    connect(root->right);
}
```



# 6. Populating Next Right Pointers in Each Node II

Follow up for problem "Populating Next Right Pointers in Each Node".

What if the given tree could be any binary tree? Would your previous solution still work?

```cpp
void connect(TreeLinkNode *root) {
    // use two while loop, loop every level
    if (!root) return;
    TreeLinkNode* leftMost = new TreeLinkNode(0);
    while (root) {
        TreeLinkNode* curr = leftMost;
        while (root) {
            if (root->left) {
                curr->next = root->left;
                curr = curr->next;
            } 
            if (root->right) {
                curr->next = root->right;
                curr = curr->next;
            }
            root = root->next;
        }
        
        root = leftMost->next;
        leftMost->next = NULL;
    }
    return;
}
```

# 7. Lowest Common Ancestor of a Binary Search Tree



Given a binary search tree \(BST\), find the lowest common ancestor \(LCA\) of two given nodes in the BST.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes v and w as the lowest node in T that has both v and w as descendants \(where we allow**a node to be a descendant of itself**\).”

```cpp
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (!p) return q;
    if (!q) return p;
    if (p->val == q->val) return p;
    while (root->val != p->val && root->val != q->val) {
        if (root->val > p->val && root->val > q->val) root = root->left;
        else if (root->val < p->val && root->val < q->val) root = root->right;
        else return root;
    }
    return root;
}
```

# 8. Lowest Common Ancestor of a Binary Tree

Given a binary tree, find the lowest common ancestor \(LCA\) of two given nodes in the tree.

```cpp
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (!root) return NULL;
    if (root == p || root == q) return root;
    TreeNode* left = lowestCommonAncestor(root->left, p, q);
    TreeNode* right = lowestCommonAncestor(root->right, p, q);
    if (left && right) return root;
    else return !left ? right : left;
}
```

# 9. Construct Binary Tree from Preorder and Inorder Traversal

```cpp
TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        if (preorder.size()==0 || inorder.size()==0 || preorder.size()!=inorder.size()) return NULL;
        TreeNode* root = buildTreeHelper(preorder,0,preorder.size()-1,inorder,0,inorder.size()-1);
        return root;
    }
    TreeNode* buildTreeHelper(vector<int>& preorder, int preStart, int preEnd,vector<int>& inorder, int inStart, int inEnd) {
        if (preStart <= preEnd) {
            TreeNode* root = new TreeNode(preorder[preStart]);
            if (preStart == preEnd) return root;
            int i = 0;
            for(i = 0; i < inorder.size(); i++){  
                if (inorder[inStart + i] == root->val)  break;  
            }

            root->left = buildTreeHelper(preorder,preStart+1,preStart+i,inorder,inStart,inStart+i-1);
            root->right = buildTreeHelper(preorder,preStart+i+1,preEnd,inorder,inStart+i+1,inEnd);
            return root;
        }
        else return NULL;
    }
```

# 10. Number of islands

Given a 2d grid map of`'1'`s \(land\) and`'0'`s \(water\), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

```cpp
int numIslands(vector<vector<char>>& grid) {
    if (grid.size() == 0 || grid[0].size() == 0) return 0;
    int res = 0;
    for (int i = 0; i < grid.size(); i++) {
        for (int j = 0; j < grid[0].size(); j++) {
            if (grid[i][j] == '1') {
                res++;
                clearSurrounding(grid, i, j);
            }
        }
    }
    return res;
}

void clearSurrounding(vector<vector<char>>& grid, int i, int j) {
    grid[i][j] = '0';
    if (i > 0 && grid[i-1][j] == '1') clearSurrounding(grid, i-1, j);
    if (j > 0 && grid[i][j-1] == '1') clearSurrounding(grid, i, j-1);
    if (i < grid.size() - 1 && grid[i+1][j] == '1') clearSurrounding(grid, i+1, j);
    if (j < grid[0].size() - 1 && grid[i][j + 1] == '1') clearSurrounding(grid, i, j + 1);
}
```

# 11. Clone Graph

```cpp
UndirectedGraphNode *cloneGraph(UndirectedGraphNode *node) {
    if (!node) return NULL;
    unordered_map<UndirectedGraphNode*, UndirectedGraphNode*> mp;
    UndirectedGraphNode* copynode = new UndirectedGraphNode(node->label);
    mp[node] = copynode;
    queue<UndirectedGraphNode*> q;
    q.push(node);
    while(!q.empty()) {
        UndirectedGraphNode* curr = q.front();
        q.pop();
        for (int i = 0; i < curr->neighbors.size(); i++) {
            UndirectedGraphNode* neighbor = curr->neighbors[i];
            if (mp.count(neighbor) == 0) {
                UndirectedGraphNode* copyneighbor = new UndirectedGraphNode(neighbor->label);
                mp[neighbor] = copyneighbor;
                mp[curr]->neighbors.push_back(copyneighbor);
                q.push(neighbor);
            } else {
                mp[curr]->neighbors.push_back(mp[neighbor]);
            }
        }
    }
    return copynode;
}
```



