```
class Trie {
public:
    struct Node{
        Node* son[26];
        bool is_end;
        Node(){
            for(int i=0;i<26;i++)son[i]=NULL;
            is_end=false;
        }
    }*root;
    Trie() {
        root=new Node();
    }
    
    void insert(string word) {
        auto p=root;
        for(auto x:word){
            int i=x-'a';
            if(!p->son[i])p->son[i]=new Node();
            p=p->son[i];
        }
        p->is_end=true;
    }
    
    bool search(string word) {
        auto p=root;
        for(auto x:word){
            int i=x-'a';
            if(!p->son[i])return false;
            p=p->son[i];
        }
        return p->is_end;
    }
    
    bool startsWith(string prefix) {
        auto p=root;
        for(auto x:prefix){
            int i=x-'a';
            if(!p->son[i])return false;
            p=p->son[i];
        }
        return true;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```

 
