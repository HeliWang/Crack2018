# 1. Leetcode 285

Given a binary search tree and a node in it, find the in-order successor of that node in the BST.

\`\`\`**Note**: If the given node has no in-order successor in the tree, return`null`

Idea:

```
找successor只有两种情况：
如果有右child，那么就是右child的最左孩子
如果没有右child，那么就是他的第一个左父亲

所以二分法向下查找，出现向左走，就mark一下root，因为我们要留下最后一个右父亲
如果succ出现在该点的右孩子，那么p.val会小于这个rightChild.val，从而又实现一次向左走，并留下succ

综上所述，用二分法左转存值，可以得到inorder successor
```

Solution:

```cpp
TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
    if (!root || !p) return NULL;
    TreeNode* succ = NULL;
    while(root) {
        if (p->val < root->val) {
            succ = root;
            root = root->left;
        } else {
            root = root->right;
        }
    }
    return succ;
}
```

# 2. Reverse Fibonacci:

Solution:

```cpp
// Fibonacci & Reverse Fibnonacci
int fib(int n) {
    if (n == 0) return 0;
    if (n == 1) return 1;
    if (n == 2) return 1;
    return fib(n-1) + fib(n-2);
}

int a = 99, b = 55;
void printReverseFib(int n) {
    vector<int> dp;
    dp.push_back(a);
    dp.push_back(b);
    while (n > 2) {
        if (dp[dp.size() - 2] < dp[dp.size() - 1]) {
            dp.pop_back();
            break;
        }
        dp.push_back(dp[dp.size() - 2] - dp[dp.size() - 1]);
        n--;
    }
    for (auto x: dp) {
        cout << x << " ";
    }
}
```

# 3. Reverse Linked List

Iteration:

```cpp
ListNode* reverseList(ListNode* head) {
    ListNode* prev = NULL;
    ListNode* curr = head;
    ListNode* post = NULL;
    while (curr) {
        post = curr->next;
        curr->next = prev;
        prev = curr;
        curr = post;
    }
    return prev;
}
```

Recursion:

```cpp
ListNode* reverseList(ListNode* head) {
    ListNode* prev = NULL;
    return reverseListHelper(head, prev);
}

ListNode* reverseListHelper(ListNode* head, ListNode* prev) {
    if (!head) return prev;
    ListNode* post = head->next;
    head->next = prev;
    return reverseListHelper(post, head);
}
```



