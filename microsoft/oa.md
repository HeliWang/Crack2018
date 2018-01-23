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

# 4. Reverse Linked List II

```cpp
ListNode* reverseBetween(ListNode* head, int m, int n) {
    if (!head || !head->next||(m==n)) return head;
    ListNode* a = NULL;
    ListNode* b = head;
    ListNode* c = NULL;
    int count = 1;
    if (m == 1) {
        while (count <= n) {
            c = b->next;
            b->next = a;
            a = b;
            b = c;
            count++;
        }
        head->next = b;
        return a;
    }
    else {
        ListNode* dummy = head;
        count = 1;
        while (count < m-1) {
            dummy = dummy->next;
            count++;
        }
        count = 0;
        ListNode *start = dummy->next;
        b = start;
        while (count <= n-m) {
            c = b->next;
            b->next = a;
            a = b;
            b = c;
            count++;
        }
        start->next = b;
        dummy->next = a;
        return head;
    }
}
```

# 5. Divide Two Integers

**Idea**:

```
被除数每乘以2，multiple就可以乘以二，比如18 / 2, 那么2乘以了八倍，那么商也应该从1乘以八倍，
最后得到更新的dvd为2，dis还是2，所以8+1 = 9
```

**Solution**:

```cpp
int divide(int dividend, int divisor) {
    if (!divisor || (dividend == INT_MIN && divisor == -1))
        return INT_MAX;
    int sign = ((dividend < 0) ^ (divisor < 0)) ? -1 : 1;
    int res = 0;
    long long dvd = labs(dividend);
    long long dvs = labs(divisor);
    while(dvd >= dvs) {
        long long temp = dvs, multiple = 1;
        while (dvd >= (temp << 1)) {
            temp <<= 1;
            multiple <<= 1;
        }
        dvd -= temp;
        res += multiple;
    }
    return sign * res;
}
```

1. Compare Version Number

Idea:

```
Get the single version number one by one, and also controlled in a big while loop
Let num1 = num2 = 0, then can handle some edge cases: 
    x.y.z > x.y
```

**Solution**:

```cpp
int compareVersion(string version1, string version2) {
    int num1 = 0, num2 = 0;
    int i = 0, j = 0;
    while(i<version1.length() || j < version2.length()) {
        while(version1[i]!='.' && i < version1.length()) {
            num1 = num1*10 + version1[i]-'0';
            i++;
        }
        while(version2[j]!='.' && j < version2.length()) {
            num2 = num2*10 + version2[j]-'0';
            j++;
        }
        if (num1 != num2) return num1>num2?1:-1;
        i++;j++;
        num1 = num2 = 0;
    }

    return 0;
}
```



# 6. Permutation Sequence

The set`[1,2,3,…,n]`contains a total ofn! unique permutations.

By listing and labeling all of the permutations in order,  
We get the following sequence \(ie, for n= 3\):

```
"123"
"132"
"213"
"231"
"312"
"321"
```

Given N and K, return the Kth permutation sequence.

Idea:

```
Use Factorial, 找规律
```

Solution:

```cpp
int fact(int n) {
    if (n == 1) return 1;
    return n * fact(n-1);
}

string getPermutation(int n, int k) {
    string s = "";
    int factorial = fact(n); 
    k = (k-1) % (factorial); 
    vector<int> candidates(n, 0);
    for (int i = 0; i < candidates.size(); i++) {
        candidates[i] = i + 1;
    }
    
    while (n) {
        factorial = factorial / n;  
        int index = k / factorial; 
        s += candidates[index] + '0'; 
        candidates.erase(candidates.begin() + index);
        k = k % factorial;
        n--; 
    }
    return s;
}
```



