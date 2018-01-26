1. Validate Binary Search Tree \(Use left node as min bound, right node as max bound\)

2. Binary Tree Inorder Traversal \(Recursive or Stack Iterative\)

3. Binary Tree Level Order Traversal \(Queue BFS, push a NULL every level, which means push NULL when meet NULL\)

4. Binary Tree Zigzag Level Order Traversal \(Use a flag as boolean\)

5. Populating Next Right Pointer to Every Node \(Recursive 整理好下一层，然后调用dfs left, dfs right\)

6. Populating Next Right Pointer to Every Node II \(用两个while\(root\) loop, 当做一层一层的traversal, 用一个dummyNode当做leftMost, 每层从leftMost开始, 用一个currNode 来穿针引线, curr-&gt;next = root-&gt;next, curr = curr-&gt;next; \)

7. Lowest Common Ancestor of a Binary Search Tree \(从root向下遍历, 如果跟其中一个相等就返回root, 然后判断大中小三个可能\)

8. Lowest Common Ancestor of a Binary Tree \(Recrusion, 建一个leftNode 是 LCS\(root-&gt;left\)的返回值, 同时建一个rightNode, 根据这两个的返回值来输出结果, 注意recursion的base case是: root与p,q 相等则返回root\) 

PS: 由于是Binary Tree, 所以这里不能用root-&gt;val来做任何判断, 直接判断root和p,q的地址即可

9. Construct Binary Tree from Preorder and Inorder Traversal

