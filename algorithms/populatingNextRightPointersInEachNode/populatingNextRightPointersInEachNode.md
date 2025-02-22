[116. 填充每个节点的下一个右侧节点指针](https://leetcode.cn/problems/populating-next-right-pointers-in-each-node/)

**完美二叉树**

### 1、模拟

```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/

class Solution {
public:
    Node* connect(Node* root) {
        if(!root)return NULL;
        auto dummy=root;
        while(root->left){
            for(auto p=root;p;p=p->next){
                p->left->next=p->right;
                if(p->next)p->right->next=p->next->left;
            }
            root=root->left;
        }
        return dummy;
    }
};
```

- 时间：n
- 空间：1