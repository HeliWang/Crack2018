1. Serialize and Deserialize BST
2. Serialize and Deserialize Binary Tree
3. Implement Trie \(Prefix Tree\)
4. LRU Cache

# 1. Serialize and Deserialize BST

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a**binary search tree**. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary search tree can be serialized to a string and this string can be deserialized to the original tree structure.



```cpp

// Encodes a tree to a single string.
string serialize(TreeNode* root) {
    ostringstream os;
    serialize(root, os);
    return os.str(); 
}

void serialize (TreeNode* root, ostringstream& os) {
    if (!root) os << "# ";
    else {
        os << root->val << " ";
        serialize(root->left, os);
        serialize(root->right, os);
    }
}

// Decodes your encoded data to tree.
TreeNode* deserialize(string data) {
    istringstream is(data);
    return deserialize(is);
}

TreeNode* deserialize(istringstream &is) {
    string val = "";
    is >> val;
    if (val == "#") {
        return NULL;
    }
    TreeNode* curr = new TreeNode(stoi(val));
    curr->left = deserialize(is);
    curr->right = deserialize(is);
    return curr;
}
```

# 2. Serialize and Deserialize Binary Tree

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

```cpp
// Encodes a tree to a single string.
string serialize(TreeNode* root) {
    ostringstream os;
    serialize(root, os);
    return os.str();
}

void serialize(TreeNode* root, ostringstream& os) {
    if (!root) os << "# ";
    else {
        os << root->val << " ";
        serialize(root->left, os);
        serialize(root->right, os);
    }
}

// Decodes your encoded data to tree.
TreeNode* deserialize(string data) {
    istringstream is(data);
    return deserialize(is);
}

TreeNode* deserialize(istringstream &is) {
    string val = "";
    is >> val;
    if (val == "#") return NULL;
    TreeNode* node = new TreeNode(stoi(val.c_str()));
    node->left = deserialize(is);
    node->right = deserialize(is);
    return node;
}
```

# 3. Implement Trie \(Prefix Tree\)

Implement a trie with`insert`,`search`, and`startsWith`methods.

```cpp
TrieNode* root;
/** Initialize your data structure here. */
Trie() {
    root = new TrieNode();
}

/** Inserts a word into the trie. */
void insert(string word) {
    TrieNode* curr = root;
    for (int i = 0; i < word.length(); i++) {
        if (curr->children.count(word[i]) == 0) {
            curr->children[word[i]] = new TrieNode();
        } 
        curr = curr->children[word[i]];
    }
    curr->hasWord = true;
}

/** Returns if the word is in the trie. */
bool search(string word) {
    TrieNode* curr = root;
    for (int i = 0; i < word.length(); i++) {
        if (curr->children.count(word[i]) == 0) return false;
        curr = curr->children[word[i]];
    }
    return curr->hasWord;
}

/** Returns if there is any word in the trie that starts with the given prefix. */
bool startsWith(string prefix) {
    TrieNode* curr = root;
    for (int i = 0; i < prefix.length(); i++) {
        if (curr->children.count(prefix[i]) == 0) return false;
        curr = curr->children[prefix[i]];
    }
    return true;
}
```

# 4. LRU Cache

Design and implement a data structure for[Least Recently Used \(LRU\) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU). It should support the following operations:`get`and`put`.

`get(key)`- Get the value \(will always be positive\) of the key if the key exists in the cache, otherwise return -1.  
`put(key, value)`- Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

**Solution:**

```cpp
class Node {
public:
    int key;
    int val;
    Node(int k, int v): key(k), val(v) {};
};

class LRUCache {
private:
    int cap;
    list<Node*> cache;
    unordered_map<int, list<Node*>::iterator> mp;
public:
    
    
    LRUCache(int capacity) {
        cap = capacity;
    }
    
    int get(int key) {
        if (mp.find(key) != mp.end()) {
            // find the index
            auto it = mp[key];
            // create a new node
            Node* newNode = new Node(key, (*it)->val);
            // erase
            cache.erase(it);
            // insert at the begining
            cache.push_front(newNode);
            // set map
            mp[key] = cache.begin();
            
            cout<< 0;
            return newNode->val;
        } else {
            return -1;
        }
    }
    
    void put(int key, int value) {
        if (mp.find(key) != mp.end()) {
            cache.erase(mp[key]); 
        }
        Node* newNode = new Node(key, value);
        cache.push_front(newNode);
        mp[key] = cache.begin();
        if (cache.size() > cap) {
            mp.erase((*cache.rbegin())->key);
            cache.pop_back();  
        }
    }
};
```



