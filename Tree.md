# Tree Cheat Sheet in C++

## 1. Basic Structure of a Binary Tree Node
```cpp
struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};
```
## 2. Tree Traversals
### Preorder Traversal (Root, Left, Right)
```cpp
void preorder(TreeNode* root) {
    if (root == NULL) return;
    cout << root->val << " ";
    preorder(root->left);
    preorder(root->right);
}

```
### Inorder Traversal (Left, Root, Right)
```cpp
void inorder(TreeNode* root) {
    if (root == NULL) return;
    inorder(root->left);
    cout << root->val << " ";
    inorder(root->right);
}

```
### Postorder Traversal (Left, Right, Root)
```cpp
void postorder(TreeNode* root) {
    if (root == NULL) return;
    postorder(root->left);
    postorder(root->right);
    cout << root->val << " ";
}

```
### Level Order Traversal (BFS)
```cpp
void levelOrder(TreeNode* root) {
    if (root == NULL) return;
    queue<TreeNode*> q;
    q.push(root);
    while (!q.empty()) {
        TreeNode* node = q.front();
        q.pop();
        cout << node->val << " ";
        if (node->left) q.push(node->left);
        if (node->right) q.push(node->right);
    }
}

```
## 3. Insert a Node in a Binary Search Tree (BST)

```cpp
TreeNode* insertBST(TreeNode* root, int val) {
    if (root == NULL) return new TreeNode(val);
    if (val < root->val) 
        root->left = insertBST(root->left, val);
    else if (val > root->val) 
        root->right = insertBST(root->right, val);
    return root;
}

```
## 4. Search in a Binary Search Tree (BST)
```cpp
TreeNode* searchBST(TreeNode* root, int val) {
    if (root == NULL || root->val == val) return root;
    if (val < root->val)
        return searchBST(root->left, val);
    else
        return searchBST(root->right, val);
}

```
## 5. Delete a Node in a Binary Search Tree (BST) 
```cpp
TreeNode* findMin(TreeNode* root) {
    while (root->left) root = root->left;
    return root;
}

TreeNode* deleteNode(TreeNode* root, int key) {
    if (root == NULL) return root;
    if (key < root->val)
        root->left = deleteNode(root->left, key);
    else if (key > root->val)
        root->right = deleteNode(root->right, key);
    else {
        if (!root->left) return root->right;
        if (!root->right) return root->left;
        TreeNode* temp = findMin(root->right);
        root->val = temp->val;
        root->right = deleteNode(root->right, temp->val);
    }
    return root;
}

```
## 6. Maximum Depth of a Binary Tree 
```cpp
int maxDepth(TreeNode* root) {
    if (!root) return 0;
    int leftDepth = maxDepth(root->left);
    int rightDepth = maxDepth(root->right);
    return max(leftDepth, rightDepth) + 1;
}

```
## 7. Validate a Binary Search Tree (BST) 
```cpp
bool validateBST(TreeNode* root, TreeNode* minNode = NULL, TreeNode* maxNode = NULL) {
    if (!root) return true;
    if ((minNode && root->val <= minNode->val) || (maxNode && root->val >= maxNode->val)) return false;
    return validateBST(root->left, minNode, root) && validateBST(root->right, root, maxNode);
}

```
## 8. Lowest Common Ancestor (LCA) in BST 
```cpp
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (!root) return NULL;
    if (root->val > p->val && root->val > q->val)
        return lowestCommonAncestor(root->left, p, q);
    if (root->val < p->val && root->val < q->val)
        return lowestCommonAncestor(root->right, p, q);
    return root;
}

```
## 9. Diameter of a Binary Tree (Longest Path Between Two Nodes) 
```cpp
int diameterOfBinaryTree(TreeNode* root, int& diameter) {
    if (!root) return 0;
    int left = diameterOfBinaryTree(root->left, diameter);
    int right = diameterOfBinaryTree(root->right, diameter);
    diameter = max(diameter, left + right);
    return max(left, right) + 1;
}

int diameter(TreeNode* root) {
    int diameter = 0;
    diameterOfBinaryTree(root, diameter);
    return diameter;
}

```
## 10. Check if Two Trees are Identical 
```cpp
bool isIdentical(TreeNode* p, TreeNode* q) {
    if (!p && !q) return true;
    if (!p || !q) return false;
    return (p->val == q->val) && isIdentical(p->left, q->left) && isIdentical(p->right, q->right);
}

```
## 11. Symmetric Tree Check
```cpp
bool isMirror(TreeNode* t1, TreeNode* t2) {
    if (!t1 && !t2) return true;
    if (!t1 || !t2) return false;
    return (t1->val == t2->val) && isMirror(t1->left, t2->right) && isMirror(t1->right, t2->left);
}

bool isSymmetric(TreeNode* root) {
    return isMirror(root, root);
}

```
## 12. Path Sum in a Binary Tree
```cpp
bool hasPathSum(TreeNode* root, int sum) {
    if (!root) return false;
    if (!root->left && !root->right) return sum == root->val;
    return hasPathSum(root->left, sum - root->val) || hasPathSum(root->right, sum - root->val);
}

```
## 13. Invert/Flip a Binary Tree 
```cpp
TreeNode* invertTree(TreeNode* root) {
    if (!root) return NULL;
    swap(root->left, root->right);
    invertTree(root->left);
    invertTree(root->right);
    return root;
}

```
## 14. Flatten a Binary Tree to a Linked List
```cpp
void flatten(TreeNode* root) {
    TreeNode* curr = root;
    while (curr) {
        if (curr->left) {
            TreeNode* prev = curr->left;
            while (prev->right) prev = prev->right;
            prev->right = curr->right;
            curr->right = curr->left;
            curr->left = NULL;
        }
        curr = curr->right;
    }
}

```
## 15. Construct a Binary Tree from Inorder and Preorder Traversal
```cpp
TreeNode* buildTreeHelper(vector<int>& preorder, vector<int>& inorder, int preStart, int inStart, int inEnd, unordered_map<int, int>& inMap) {
    if (preStart > preorder.size() - 1 || inStart > inEnd) return NULL;
    TreeNode* root = new TreeNode(preorder[preStart]);
    int inIndex = inMap[root->val];
    root->left = buildTreeHelper(preorder, inorder, preStart + 1, inStart, inIndex - 1, inMap);
    root->right = buildTreeHelper(preorder, inorder, preStart + inIndex - inStart + 1, inIndex + 1, inEnd, inMap);
    return root;
}

TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
    unordered_map<int, int> inMap;
    for (int i = 0; i < inorder.size(); i++) inMap[inorder[i]] = i;
    return buildTreeHelper(preorder, inorder, 0, 0, inorder.size() - 1, inMap);
}

```
