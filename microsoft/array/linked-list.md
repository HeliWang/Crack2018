1. Reverse Linked List: recursive & iterative

2. Linked List Cycle: fast & slow pointer

3. Add Two Numbers: new list l3

4. Add Two Numbers II: reverse and using \#3, or use two stacks

5. Merge Two Sorted Lists: just merge

6. Merge K Sorted Lists: minHeap \(cmp is larger &gt;\)

7. Intersection of Two Linked Lists: a + b = b + a,

8. Copy List with Random Pointer: insert into the middle, then copy random, then cut those link



# 1. Reverse Linked List

**Solution: **

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

# 2. Linked List Cycle

**Solution:**

```cpp
bool hasCycle(ListNode *head) {
    if (!head || !head->next) return false;
    ListNode* first = head;
    ListNode* second = head->next;
    while(second && second->next) {
        if (first == second) return true;
        first = first->next;
        second = second->next->next;
    }
    return false;
}
```

# **3. Add Two Numbers**

**Solution:**

```cpp
ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    ListNode* l3 = new ListNode(0);
    ListNode* dummyNode = l3;
    int sum = 0, carry = 0;
    while (l1 != NULL && l2 != NULL) {
        sum = (l1->val + l2->val + carry) % 10;
        carry = (l1->val + l2->val + carry) / 10;
        l3->next = new ListNode(sum);
        l1 = l1->next;
        l2 = l2->next;
        l3 = l3->next;
    }
    ListNode* l4 = l1 != NULL ? l1 : l2;
    while (l4 != NULL) {
        sum = (l4->val + carry) % 10;
        carry = (l4->val + carry) / 10;
        l3->next = new ListNode(sum);
        l4 = l4->next;
        l3 = l3->next;
    }
    if (carry != 0) {
        l3->next = new ListNode(carry);
    }
    return dummyNode->next;
}
```

# 4. **Add Two Numbers II**

You are given two**non-empty**linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Follow up:**  
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

```cpp
ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
    if (!l1) return l2;
    if (!l2) return l1;
    stack<int> s1;
    stack<int> s2;
    while (l1) {s1.push(l1->val); l1 = l1->next;}
    while (l2) {s2.push(l2->val); l2 = l2->next;}

    ListNode* l3 = new ListNode(0);
    int sum = 0;
    while (!s1.empty() || !s2.empty()) {
        if (!s1.empty()) {sum += s1.top(); s1.pop();}
        if (!s2.empty()) {sum += s2.top(); s2.pop();}
        l3->val = sum % 10;
        ListNode* head = new ListNode(sum/10);
        head->next = l3;
        l3 = head;
        sum = sum / 10;
    }
    return l3->val == 0 ? l3->next : l3;
}
```

# 5. Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

**Solution:**

```cpp
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    if (!l1) return l2;
    if (!l2) return l1;
    ListNode* l3 = new ListNode(0);
    ListNode* dummy = l3;
    while (l1 && l2) {
        if (l1->val <= l2->val) {
            l3->next = new ListNode(l1->val);
            l1 = l1->next;
        } else {
            l3->next = new ListNode(l2->val);
            l2 = l2->next;
        }
        l3 = l3->next;
    }
    if (l1) l3->next = l1;
    if (l2) l3->next = l2;
    return dummy->next;
}
```

# 6. Merge k Sorted Lists

**Solution:**

```cpp
struct cmp {
    bool operator() (ListNode* a, ListNode* b) {
        return a->val > b->val;
    }  
};
ListNode* mergeKLists(vector<ListNode*>& lists) {
    priority_queue<ListNode*, vector<ListNode*>, cmp> minHeap;
    for (auto l: lists) {
        if (l) minHeap.push(l);
    }
    if (minHeap.empty()) return NULL;
    ListNode* result = minHeap.top();
    minHeap.pop();
    ListNode* curr = result;
    if (result->next) minHeap.push(result->next);
    
    while (!minHeap.empty()) {
        curr->next = minHeap.top();
        curr = curr->next;
        minHeap.pop();
        if (curr->next) minHeap.push(curr->next);
    }
    return result;
}
```

# 7. Intersection of Two Linked Lists

Write a program to find the node at which the intersection of two singly linked lists begins.

For example, the following two linked lists:

```
A:          a1 → a2
                   ↘
                     c1 → c2 → c3
                   ↗            
B:     b1 → b2 → b3
```

**Solution:**

```cpp
ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
    ListNode* l1 = headA;
    ListNode* l2 = headB;
    while (l1 != l2) {
        if (!l1) l1 = headB;
        else l1 = l1->next;
        if (!l2) l2 = headA;
        else l2 = l2->next;
    }
    return l1;
}
```

# 8. Copy List with Random Pointer

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

```cpp
RandomListNode *copyRandomList(RandomListNode *head) {
    if (!head) return NULL;
    RandomListNode* dummyHead = head;
    while (head) {
        RandomListNode* nextHead = head->next;
        head->next = new RandomListNode(head->label);
        head->next->next = nextHead;
        head = head->next->next;
    }
    head = dummyHead;
    while(head && head->next) {
        if (head->random) {
             head->next->random = head->random->next;
        }
        head = head->next->next;
    }
    head = dummyHead;
    RandomListNode* res = head->next;
    while(head && head->next) {
        RandomListNode* copycurr = head->next;
        head->next = copycurr->next;
        if (head->next) {
            copycurr->next = head->next->next;
        }
        head = head->next;
    }
    return res;
}
```



