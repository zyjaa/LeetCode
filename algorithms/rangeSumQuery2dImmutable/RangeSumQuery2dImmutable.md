### 1、二位前缀和

```
class NumMatrix {
public:
    vector<vector<int>> s;
    NumMatrix(vector<vector<int>>& matrix) {
        int n=matrix.size(),m=matrix[0].size();
        s=vector<vector<int>>(n+1,vector<int>(m+1));
        for(int i=1;i<=n;i++){
            for(int j=1;j<=m;j++){
                s[i][j]=s[i][j-1]+s[i-1][j]-s[i-1][j-1]+matrix[i-1][j-1];
            }
        }
    }
    
    int sumRegion(int a, int b, int c, int d) {
        a++,b++,c++,d++;
        return s[c][d]-s[a-1][d]-s[c][b-1]+s[a-1][b-1];
    }
};
```

