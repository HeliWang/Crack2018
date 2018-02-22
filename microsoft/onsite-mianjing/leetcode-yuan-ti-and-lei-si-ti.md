**Roman to Integer**  用map记录表示

**Integer To Roman** 用map记录表示 注意加入 9 90 900 的符号

**Add String** 这种2个string的loop题，记得判断到头了就为0，其他的可以继续用

**Longest Palindrome Subsequence** **&& Substring **动态规划

**Two Sum** hashmap做

**Tic Tac Toe** 用rows cols array，遇到1就++ 遇到2就--，直到加到N或者-N

**Remove Duplicate in Linked List I && II : **use dummy node and duplicate number for II

**Valid Parenthesis & Generate Parenthesis: **Stack & Backtracking

**Word Search I && II: ** DFS && Trie

**Word Break I && II:** Dynamic Programming && Backtracking 加 DP剪枝

**Combine two BST:** Construct BST by array or linked list

**Merge two linked list & array**

**Regular Expression Match & Wildcard Matching: **Dynamic Programming

Shortest Steps for Knight

**Get Random: **Use hashmap and array, rand\(\) from \#include algorithm

**Reverse String II**

```cpp
for (int i = 0; i <= s.size(); i += 2*k) {
        reverse(s.begin() + i, min(s.begin() + i + k, s.end()));
    }
```

Longest Path in Graph

稀疏向量求内积

Basic Calculator I II III

**Nth end of linked list  & Linked list Has cycle**

**Letter Combinations of a Phone Number: **Backtracking

[Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node) I && II

**Prefix Tree:** TrieNode hasWord, unordered\_map

**Serialize and Deserialize Tree**

**LIS**

**Find minimum in Rotated Array**

[**Largest Number**](https://leetcode.com/problems/largest-number)

**Copy List with Random Pointer && Clone graph**

[**Odd Even Linked List**](https://leetcode.com/problems/odd-even-linked-list)

Malloc function: [http://www.ibm.com/developerworks/linux/library/l-memory](http://www.ibm.com/developerworks/linux/library/l-memory)

[http://johanmabille.github.io/blog/2014/12/06/aligned-memory-allocator/](http://johanmabille.github.io/blog/2014/12/06/aligned-memory-allocator/)

**Spiral Matrix && Rotate Matrix**

**Binary Tree Level Order Travesal**

双向链表 有个next or prev 错了，要求travese一遍

二维矩阵，起点是0，0，终点是最右边一列

**Find in rotated sorted array**

**Lowest common ancestor in binary tree & bst**

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

Simplify Path without stack?

**Get random object from data stream**

**Pow\(x, n\)  && sqrt\(x\)**

Find k closet points

**Valid IP Address**

Delete words start with B

Find shortest distance between two points in matrix

2个长方形相交点

Remove Comments

295 kth largest

Connect leaf node in tree\(stack\)

Can add interval \(more than 3 overlap will be invalid\)

Product except self

**Top k**

**Find celebrity**

Burst Ballons

Multiply Strings

```cpp
int c = res[i+j];
res[i+j] = (a * b + c) % 10;
res[i+j+1] += (a * b + c) / 10;
```

Odd Even Linked List

Odd Even Array

