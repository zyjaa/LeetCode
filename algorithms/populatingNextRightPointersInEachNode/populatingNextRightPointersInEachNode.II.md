[117. 填充每个节点的下一个右侧节点指针 II](https://leetcode.cn/problems/populating-next-right-pointers-in-each-node-ii/)

二叉树



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
        auto cur=root;
        while(cur){
            auto head=new Node(),tail=head;
            for(auto p=cur;p;p=p->next){
                if(p->left)tail=tail->next=p->left;
                if(p->right)tail=tail->next=p->right;
            }
            cur=head->next;
        }
        return root;
    }
};
```

- 时间：n
- 空间：1
  - head、tail是虚拟头结点，用完一层就没了，再想用就再创建
  - next指针之所以还在就是因为tail->next是一个左子树或者右子树的节点，是真实存在的