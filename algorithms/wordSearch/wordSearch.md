[79. 单词搜索](https://leetcode.cn/problems/word-search/)

 

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/11/04/word2.jpg)

```
输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
输出：true
```



### 1、DFS

```cpp
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        for(int i=0;i<board.size();i++){
            for(int j=0;j<board[0].size();j++){
                if(dfs(board,word,0,i,j))return true;
            }
        }
        return false;
    }
    bool dfs(vector<vector<char>>& board,string word,int u,int i,int j){
        if(board[i][j]!=word[u])return false;
        if(u==word.size()-1)return true;
        char t=board[i][j];
        board[i][j]='.';
        int dx[4]={0,1,0,-1},dy[4]={1,0,-1,0};
        for(int x=0;x<4;x++){
            int a=i+dx[x],b=j+dy[x];
            if(a>=0 && b>=0 && a<board.size() && b<board[0].size()){
                if(dfs(board,word,u+1,a,b))return true;
            }
        }
        board[i][j]=t;
        return false;
    }
};
```

- 时间：O($$m*n*4^L$$)
  - 每次4个方向，单词长度为L，时间复杂度：$$4^L$$
- 空间：L，word长度（用于递归栈）